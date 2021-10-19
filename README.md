# Getting Started

Welcome to the GiveWorx API documentation!

> If you just want to preview your widget, you can do it [here](https://main.d285tagm1r2kq6.amplifyapp.com/).

## Usage of the GiveWorx Widget (default integration)

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
| `CampaignId`   | Yes      | integer | Campaign ID                              |
| `CampaignName` | Yes      | string  | Campaign Name                            |
| `Merchant`     | Yes      | object  | Merchant properties                      |
| `Merchant.Id`  | Yes      | integer | Merchant ID                              |
| `IsAtWork`     | No       | boolean | Only required if used via AtWork website |

```javascript
window.giveworxWidget.init({
  CampaignId: ID,
  CampaignName: CAMPAIGN_NAME,
  Merchant: {
    Id: MERCHANT_ID,
  },
  DonationDetails: {
    DonorCardDetails: {},
  }
});
```

**Other ways of integration:**

* [Username/password](username-password-integration.md) ⚠️ deprecated
* [AtWork](atwork-integration.md)


If you're willing to create your own custom integration, follow the specifications below.

# API Specifications (custom integration)

`API_URL`: **production**: https://donate.giveworx.com | **qc**: https://qcdonate.giveworx.com


> `POST` API_URL/Transaction/Initiate

**JSON Schema**

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "Token": {
      "type": "string"
    },
    "transactionStatus": {
      "type": "boolean"
    },
    "languageId": {
      "type": "integer"
    },
    "username": {
      "type": "string"
    },
    "merchant": {
      "type": "object",
      "properties": {
        "id": {
          "type": "integer"
        }
      },
      "required": [
        "id"
      ]
    },
    "donationDetails": {
      "type": "object",
      "properties": {
        "donorBillingAddressLine2": {
          "type": "string"
        },
        "donorBillingAddressCity": {
          "type": "string"
        },
        "donorBillingAddressLine1": {
          "type": "string"
        },
        "donorBillingAddressState": {
          "type": "string"
        },
        "donorPhoneNumber": {
          "type": "string"
        },
        "donorBillingAddressCountry": {
          "type": "string"
        },
        "donorBillingAddressPostalCode": {
          "type": "string"
        },
        "donorCardDetails": {
          "type": "object",
          "properties": {
            "donorCardExpiryDate": {
              "type": "string"
            },
            "cardNumber": {
              "type": "string"
            }
          },
          "required": [
            "donorCardExpiryDate",
            "cardNumber"
          ]
        },
        "donationOptInFlag": {
          "type": "boolean"
        },
        "donorLastName": {
          "type": "string"
        },
        "donorFirstName": {
          "type": "string"
        },
        "donoremailid": {
          "type": "string"
        }
      },
      "required": [
        "donorBillingAddressLine2",
        "donorBillingAddressCity",
        "donorBillingAddressLine1",
        "donorBillingAddressState",
        "donorPhoneNumber",
        "donorBillingAddressCountry",
        "donorBillingAddressPostalCode",
        "donorCardDetails",
        "donationOptInFlag",
        "donorLastName",
        "donorFirstName",
        "donoremailid"
      ]
    }
  },
  "required": [
    "Token",
    "transactionStatus",
    "languageId",
    "username",
    "merchant",
    "donationDetails"
  ]
}
```
Response object:

**JSON Schema**

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "requestID": {
      "type": "guid"
    },
    "isRedirect": {
      "type": "boolean"
    },
    "redirectURL": {
      "type": "string"
    },
    "returnURL": {
      "type": "string"
    },
    "merchantJSURL": {
      "type": "string"
    },
    "languageID": {
      "type": "integer"
    },
    "merchantID": {
      "type": "integer"
    },
    "responseType": {
      "type": "integer"
    },
    "transactionStatusTypes": {
      "type": "integer"
    },
    "landingPageResponseDisplayText": {
      "type": "string"
    },
    "errorCode": {
      "type": "string"
    },
    "errorMessage": {
      "type": "string"
    },
    "campaignId": {
      "type": "integer"
    }
  },
  "required": [
    "requestID",
    "isRedirect",
    "redirectURL",
    "returnURL",
    "merchantJSURL",
    "languageID",
    "merchantID",
    "responseType",
    "transactionStatusTypes",
    "landingPageResponseDisplayText",
    "errorCode",
    "errorMessage",
    "campaignId"
  ]
}
```
