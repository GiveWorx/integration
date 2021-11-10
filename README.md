# Getting Started

Welcome to the GiveWorx API documentation!

> If you just want to preview your widget, you can do it [here](https://main.d285tagm1r2kq6.amplifyapp.com/).

## Usage of the GiveWorx Widget (token integration)

If you're looking to integrate with your website:

| ENVIRONMENT | TOKEN            | SCRIPT URL
| ----------- | ---------------- |----------------------------------
| `prod`      | Production Token | https://donate.giveworx.com
| `qc`        | QC Token         | https://qcdonate.giveworx.com

**Setup**

```javascript
<script type="text/javascript">
    !function(w, d, t, e, s){if(!w[s]){for(var di=w[s]=[],a=["init", "openDonationForm"],c=0;c<a.length;c++){var ia=a[c];di[ia]=di[ia]||function(newItemFromArray){return function(){var t=Array.prototype.slice.call(arguments);di.push([newItemFromArray,t])}}(ia)}di.SNIPPET_VERSION="1.0.1";var scriptDomTag=d.createElement("script");scriptDomTag.type="text/javascript",scriptDomTag.async=!0,
  scriptDomTag.src=`https://qcdonate.giveworx.com/js/giveworxWidget.js?env=${e}&token=${t}`;
          var p=d.getElementsByTagName("script")[0];p.parentNode.insertBefore(scriptDomTag,p)
        }
      }(window, document, "TOKEN", "ENVIRONMENT", "giveworxWidget");
</script>
```

**For initialisation**

| Key            | Required | Type    | Description                              |
| -------------- | -------- | ------- | ---------------------------------------- |
| `Merchant`     | Yes      | object  | Merchant properties                      |
| `Merchant.Id`  | Yes      | integer | Merchant ID                              |

```javascript
window.giveworxWidget.init({
  Merchant: {
    Id: MERCHANT_ID,
  },
  DonationDetails: {
    DonorCardDetails: {},
  }
});
```

if you want the initialization to take place after the page loads:

```javascript
  const asyncScript = document.querySelector("script[src*=giveworx]");
  
  asyncScript.addEventListener("load", function () {
    // -- window.giveWorx.init({options})
  })
```

**Other ways of integration:**

* [Username/password](username-password-integration.md) ⚠️ deprecated
* [AtWork](atwork-integration.md)


If you're willing to create your own custom integration, follow the specifications below.

# API Specifications (custom integration)

**The integration uses [Two-phase commit protocol](https://en.wikipedia.org/wiki/Two-phase_commit_protocol):**
1. Initiate a transaction: on this call the ~~username&password~~ (deprecated) or the token is validated. If the data is valid, a token is generated and returned (along with other data needed)
2. Initiate a donation transaction using the data received on call #1. If the call is succesfull, the HTML popup will be sent as response.

**Step 1**
ENV                                   | Method  |  Endpoint
--------------------------------------|---------|-------------------------
`PROD` https://donate.giveworx.com    | `POST`  | **/Transaction/Initiate**
`QC` https://qcdonate.giveworx.com    | `POST`  | **/Transaction/Initiate**


**Example request**

Content-Type: application/json
```json
{	
    "Token": "TOKEN",
    "Merchant": {"Id":"MERCHANT_ID"},
    "DonationDetails": {
        "DonorCardDetails":{}
    }
}
```

**Example response**  

```json
{
  "requestID": "9d721756-3f24-401e-b940-23e51ad54286",
  "isRedirect": false,
  "redirectURL": "https://qcdonate.giveworx.com/Donation/Index",
  "returnURL": null,
  "merchantJSURL": "https://qcdonate.giveworx.com/js/merchant.js",
  "languageID": 1,
  "merchantID": 1687,
  "responseType": 0,
  "transactionStatusTypes": 0,
  "landingPageResponseDisplayText": "",
  "errorCode": "00",
  "errorMessage": "Call completed successfully.",
  "campaignId": 155
}
```

<details>
    <summary><strong>Request JSON Schema</strong></summary>
<pre>
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
</pre>
</details>
    
<details>
    <summary><strong>Response JSON Schema</strong></summary>
<pre> 
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
</pre>
</details>

**Properties info:**

| Key             |  Type    | Description                              |
| --------------- |  ------- | ---------------------------------------- |
| `requestID`     |  guid    |   token used for "/Donation/Index" API call. This call return the popup HTML.                       |
| `isRedirect`    |  boolean | true when the redirect is hosted by customer, false otherwise                           |
| `redirectURL`   |  string  | API_URL + "/Donation/Index" - this is the API called to return the donation popup html                    |
| `returnURL`     |  string  | the URL to return after the donation is done                            |
| `merchantJSURL` |  string  | JavaScript library URL. This library is used by widget |
| `languageID`    |  integer | the merchant language if set or the default one. 1 English, 2 French, 3 Spanish|
| `merchantID`    |  integer | the merchant id|
| `responseType`  |  integer |  Sucessfull = 0, SucessMessage = 1, GenericError = -1, BusinessError = -2, UnAuthorized = -3, PasswordExpired = -4, PaymentFailure = -5, SessionTimeOut = -100, PaymentServerExecption = -101|
| `transactionStatusTypes`|  integer| TransactionInitiated = 1, ApplicationLoad = 12, NoThanks = 13, ApplicationError = 14, Recurring = 15, PaymentInitiated = 2, PaymentSuccess = 3, PaymentFailed = 4, PaymentServerExecption = 5|
| `landingPageResponseDisplayText`|  string| a message displayed on Order Confirm Form|
| `errorCode`     |  string | the error code (if any)|
| `errorMessage`  |  string | the error message (if any)|
| `campaignId`    |  integer| the campaign id|


**Step 2**

ENV                                   | Method  |  Endpoint
--------------------------------------|---------|-------------------------
`PROD` https://donate.giveworx.com    | `POST`  | **/Donation/Index**
`QC` https://qcdonate.giveworx.com    | `POST`  | **/Donation/Index**


**Example request**
The values should be taken from the previous call response.

Content-Type: application/json
```json
{	
    "guid": "9d721756-3f24-401e-b940-23e51ad54286",
    "isredirect": false,
    "returnURL": null,
    "languageID": 1,
    "q2CallbackUrl": null,
    "userId": null,
}
```

**Properties info:**

| Key             |  Type    | Description                              |
| --------------- |  ------- | ---------------------------------------- |
| `guid`     |  string    |   the requestID returned from previous call                       |
| `isredirect`     |  boolean    |   the isredirect returned from previous call                       |
| `returnURL`     |  string    |   the returnURL returned from previous call                       |
| `languageID`     |  string    |   the languageID returned from previous call                       |
| `q2CallbackUrl`     |  string    |   this field is used to enable the recurrent transactions. required when recurrent transactions are active, null otherwise                       |
| `userId`     |  string    |   this field is used to enable the recurrent transactions. required when recurrent transactions are active, null otherwise                         |







