<template>
  <div :id="divId" :style="{width:width , height: height }">
  {{ width }} and {{ height }}
  </div>
</template>

<script>
/*global AdobeDC*/

/* supported modes: FULL_WINDOW, SIZED_CONTAINER, IN_LINE, LIGHT_BOX */

export default {
  name: "PDFEmbed",
  props: {
    adobeKey: { type: String, required: true},
    divId: { type: String, required: true },
    url: { type: String, required: true },
    width: { type: String, default: "500px" },
    height: { type: String, default: "500px" },
    mode: { type: String, default: "FULL_WINDOW" }
  },
  data() {
    return {
      pdfAPIReady:false,
      adobeDCView:null
    }
  },
  mounted() {
    if(!window.AdobeDC) {
      console.log('need to load lib');
      //https://stackoverflow.com/a/47002863/52160
      let adobeScript = document.createElement('script')
      adobeScript.setAttribute('src', 'https://documentcloud.adobe.com/view-sdk/main.js');
      document.head.appendChild(adobeScript);
      document.addEventListener("adobe_dc_view_sdk.ready", () => { 
        console.log('PDF lib loaded');
        this.pdfAPIReady = true;
      });
    }
  },
  methods: {
    displayPDF() { 
      this.adobeDCView.previewFile({
        content: { location: { url: this.url }},
        metaData: {fileName: this.url.split('/').pop() }, 
      }, { embedMode: this.mode })
    }
  },
  watch: {
    pdfAPIReady(val) {
      // should only be called when true, but be sure
      if(val) {
        this.adobeDCView = new AdobeDC.View({
          clientId: this.adobeKey, 
          divId: this.divId
        });
        this.displayPDF();
      }
    }
  }
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
