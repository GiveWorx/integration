# Username/password integration

> ⚠️ The username and password method will no longer be supported in the near future. Use ✅  [Token integration](README.md) instead.

## Usage of the GiveWorx Widget

If you're looking to integrate with your website:

| ENVIRONMENT | TOKEN            |
| ----------- | ---------------- |
| `prod`      | Production Token |
| `qc`        | QC Token         |

**Setup**

```javascript
<script type="text/javascript">
    !function(w, d, t, e, s){if(!w[s]){for(var di=w[s]=[],a=["init", "openDonationForm"],c=0;c<a.length;c++){var ia=a[c];di[ia]=di[ia]||function(newItemFromArray){return function(){var t=Array.prototype.slice.call(arguments);di.push([newItemFromArray,t])}}(ia)}di.SNIPPET_VERSION="1.0.1";var scriptDomTag=d.createElement("script");scriptDomTag.type="text/javascript",scriptDomTag.async=!0,
  scriptDomTag.src=`giveworxWidget.js?env=${e}&token=${t}`;
          var p=d.getElementsByTagName("script")[0];p.parentNode.insertBefore(scriptDomTag,p)
        }
      }(window, document, "TOKEN", "ENVIRONMENT", "giveworxWidget");
</script>
```

**For initialisation**

| Key            | Required | Type    | Description                              |
| -------------- | -------- | ------- | ---------------------------------------- |
| `Username`     | Yes      | string  | Backoffice account                       |
| `Password`     | Yes      | string  | Backoffice accoun password               |
| `Merchant`     | Yes      | object  | Merchant properties                      |
| `Merchant.Id`  | Yes      | integer | Merchant ID                              |

```js
{	
    "Username": "USERNAME",
    "Password": "PASSWORD",
    "Merchant": {"Id":"MERCHANT_ID"},
    "DonationDetails": {
        "DonorCardDetails":{}
    }
}
```

```js
window.giveworxWidget.init({
  Merchant: {
    Id: MERCHANT_ID,
  },
  DonationDetails: {
    DonorCardDetails: {},
  }
});
```
