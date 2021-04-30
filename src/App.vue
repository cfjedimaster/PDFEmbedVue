<template>
  <div id="app">

    <PDFEmbed :adobeKey="adobeKey" 
      divId="pdf1" 
      url="/e19-aces.pdf"
      width="800px" height="800px"
      mode="LIGHT_BOX"
      >
    </PDFEmbed>

  </div>
</template>

<script>
import PDFEmbed from "./components/PDFEmbed";

const ADOBE_KEY = '14adb260cc474728855586b67b90c543';

export default {
  name: "App",
  data() {
    return {
      adobeKey: ADOBE_KEY,
    };
  },
  components: {
    PDFEmbed,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
