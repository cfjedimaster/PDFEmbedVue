# PDF Embed Vue.js Component

A work in progress on a Vue component for the Adobe [PDF Embed API](https://www.adobe.io/apis/documentcloud/dcsdk/pdf-embed.html). Requires a free(!) key to use, although the one included will work on localhost. Basic usage is:

```
<PDFEmbed :adobeKey="adobeKey" 
	divId="unique ID" 
	url="url to PDF"
	width="800px" height="800px"
	mode="embed mode, see docs and optional"
	>
</PDFEmbed>
```

