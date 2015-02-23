meteor-accounts-stripe-connect
-----

**DO NOT USE - STILL IN DEVELOPMENT**

A package for Stripe Connect, with a particular bias towards marketplaces.

This is an update to @khamoud's most excellent [meteor-stripe-connect package](https://github.com/khamoud/meteor-accounts-stripe). Unlike the original package, this package assumes you are NOT using accounts-ui.

* * *
## Usage

#### Redirect URIs
Development
`http://localhost:3000/_oauth/stripe?close`

Production
`https://yourdomain.com/_oauth/stripe?close`

#### Config
Add your client_id to settings.json
```
"client_id": "ca_ABCDEFGHIJ1234567890"
```

Add the accounts config info (e.g. /server/accounts.js)
```javascript
Accounts.loginServiceConfiguration.insert({
      service: 'stripe',
      appId: Meteor.settings.stripe.client_id,
      secret: Meteor.settings.stripe.stripe_secret_api_key,
      scope: 'read_write', //or read_only
    });
```
Add options to your login button event handler (e.g. client/sometemplate.js)
```javascript
'click #sign-in-stripe-register': function(e, tmpl){
    Meteor.loginWithStripe({
      stripe_landing: 'register',
      newAccountDetails: {
        'stripe_user[business_type]': 'non_profit',
        'stripe_user[product_category]': 'charity'
      }
    }, function (err) {
        if (err){
          console.log('ERROR: ' + err); //error handling
        } else {
          console.log('NO ERROR ON LOGIN'); //show an alert
        }
    });
  },
```
* * *

## TODOs
DRY up / improve registration options handling


## License

The MIT License (MIT)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
