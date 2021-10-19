# AtWork integration

This only address to [atwork.giveworx.com](https://atwork.giveworx.com)

**Setup**

| ENVIRONMENT | TOKEN            |
| ----------- | ---------------- |
| `prod`      | Production Token |
| `qc`        | QC Token         |


```javascript
<script type="text/javascript">
    !function(w, d, t, e, s){if(!w[s]){for(var di=w[s]=[],a=["init", "openDonationForm"],c=0;c<a.length;c++){var ia=a[c];di[ia]=di[ia]||function(newItemFromArray){return function(){var t=Array.prototype.slice.call(arguments);di.push([newItemFromArray,t])}}(ia)}di.SNIPPET_VERSION="1.0.1";var scriptDomTag=d.createElement("script");scriptDomTag.type="text/javascript",scriptDomTag.async=!0,
  scriptDomTag.src=`giveworxWidget.js?env=${e}&token=${t}`;
          var p=d.getElementsByTagName("script")[0];p.parentNode.insertBefore(scriptDomTag,p)
        }
      }(window, document, "TOKEN", "ENVIRONMENT", "giveworxWidget");
</script>
```

**Instantiate**

```javascript
window.giveworxWidget.init({
  Merchant: { Id: MERCHANT_ID },
  DonationDetails: {
    DonorCardDetails: {},
  },
  IsAtWork: true
});
```
