# Getting Started

Welcome to the GiveWorx API documentation!
> If you just want to preview your widget, you can do it [here](https://main.d285tagm1r2kq6.amplifyapp.com/).

## Usage of the GiveWorx Widget (default integration)

If you're looking to integrate with your website:

ENVIRONMENT  |  TOKEN
-------------|----------------------
`prod`       | Production Token
`qc`         | QC Token

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

Key            | Required      | Type          | Description
---------------|---------------|---------------|---------------------
`CampaignId`   | Yes           | integer       | Campaign ID
`CampaignName` | Yes           | string        | Campaign Name
`Merchant`     | Yes           | object        | Merchant properties
`Merchant.Id`  | Yes           | integer       | Merchant ID
`IsAtWork`     | No            | boolean       | Only required if used via AtWork website


```javascript
window.giveworxWidget.init({
    CampaignId: ID,
    CampaignName: CAMPAIGN_NAME,
    Merchant: { 
        Id: MERCHANT_ID 
    },
    DonationDetails: {
        DonorCardDetails: {},
    },
    IsAtWork: false,
});
```

If you're willing to create your own custom integration, follow the specifications below.

# API Specifications

Below are examples of request to GiveWorx API using different languages.
The API call generates the

## Examples API request using different programming languages

- [JavaScript](#javascript)
- [Node.js](#nodejs)

## JavaScript

```js

```

## Node.js
