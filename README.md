# Suspicious Login &amp; Threat Detection API
**[Zenlogin](https://zenlogin.co/)** is a security API that helps you secure your login and signup flows. After signing up, you'll be given an API endpoint and secret key. By integrating these into your authentication flow, Zenlogin will then detect any suspicious login attempts and email the user (from an email address you choose) to inform them of the login.

This email is a rich HTML email, including a Google Map showing the approximate location. It also provides them with other metadata including:
- The login device
- The login operating system
- The date &amp; time (relative to that location's timezone)

# Auth0 Integration
If you're using [Auth0](https://auth0.com/) for your authentication, you can now add Zenlogin without touching any code. Our integration can be accessed here:
[https://marketplace.auth0.com/integrations/zenlogin](https://marketplace.auth0.com/integrations/zenlogin)

# Advanced Features
Below are some advanced features available for our users:
- Detailed logs
- Localization
- Custom Rules (e.g. "Always notify users logging in with an @zenlogin.co account")
- Map styling
- Webhooks
- DNS CNAMEs
- DPAs

# Email Preview
Below you can see a sample email that Zenlogin sends:

<img src="https://github.com/zenlogin/suspicious-login-and-threat-detection-api/assets/612938/17f8443a-ad0d-45d2-9628-83076baad5c6" width="400" />

# Integration
The integration process for Zenlogin is straightforward. Below you'l find some examples:

## curl
``` bash
curl https://api.zenlogin.co/v1/applications/appl0123456789/logins/checks \
  --header "X_API_SECRET_KEY: your_secret_key" \
  --data identity_key="usr12345" \
  --data identity_email_address="name@website.com" \
  --data user_agent="Mozilla/5.0 (Windows NT 6.1; rv:74.0) Gecko/20100101 Firefox/74.0" \
  --data ip_address="2607:f2c0:e34c:36b0:ac91:fd58:c9b7:7f03"
```

## PHP
``` php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.zenlogin.co/v1/applications/appl0123456789/logins/checks');
$postData = array();
$postData['identity_key'] = 'usr12345';
$postData['identity_email_address'] = 'name@website.com';
$postData['user_agent'] = 'Mozilla/5.0 (Windows NT 6.1; rv:74.0) Gecko/20100101 Firefox/74.0';
$postData['ip_address'] = '2607:f2c0:e34c:36b0:ac91:fd58:c9b7:7f03';
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($postData));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
  'X_API_SECRET_KEY: your_secret_key'
));
$response = curl_exec($ch);
$response = json_decode($response, true);
curl_close($ch);
```

## Node
``` Node
const axios = require('axios');
const endpoint = 'https://api.zenlogin.co/v1/applications/appl0123456789/logins/checks',
  postData = {},
  options = {};
postData.identity_key = 'usr12345';
postData.identity_email_address = 'name@website.com';
postData.user_agent = 'Mozilla/5.0 (Windows NT 6.1; rv:74.0) Gecko/20100101 Firefox/74.0';
postData.ip_address= '2607:f2c0:e34c:36b0:ac91:fd58:c9b7:7f03';
options.headers = {};
options.headers.X_API_SECRET_KEY = 'your_secret_key';
axios.post(endpoint, postData, options).then(function(response) {
  console.log(response.data);
}).catch(function(error) {
  console.error(error.response.data);
});
```

## Python
``` Python
import requests
url = 'https://api.zenlogin.co/v1/applications/appl0123456789/logins/checks'
postData = {
  'identity_key': 'usr12345',
  'identity_email_address': 'name@website.com',
  'user_agent': 'Mozilla/5.0 (Windows NT 6.1; rv:74.0) Gecko/20100101 Firefox/74.0',
  'ip_address': '2607:f2c0:e34c:36b0:ac91:fd58:c9b7:7f03'
}
headers = {'X_API_SECRET_KEY': 'your_secret_key'}
response = requests.post(url, data=postData, headers=headers)
print response.content
```

## Ruby
``` Ruby
require 'uri'
require 'net/http'

uri = URI('https://api.zenlogin.co/v1/applications/appl0123456789/logins/checks')
req = Net::HTTP::Post.new(uri.path)
req['X_API_SECRET_KEY'] = 'your_secret_key'
postData = {}
postData['identity_key'] = 'usr12345'
postData['identity_email_address'] = 'name@website.com'
postData['user_agent'] = 'Mozilla/5.0 (Windows NT 6.1; rv:74.0) Gecko/20100101 Firefox/74.0'
postData['ip_address'] = '2607:f2c0:e34c:36b0:ac91:fd58:c9b7:7f03'
req.set_form_data(postData);

https = Net::HTTP.new(uri.host, uri.port)
https.use_ssl = true

response = https.request(req)
puts response.body
```
