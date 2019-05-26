# What is Blockstack?
Blockstack's architecture Is built to prevent behaviour that is harmful to consumers, like:
-  Selling data
- Allowing data breaches
- Data lock-in
#### We longer have to trust large companies to respect and protect our personal data.  

Rather than trying to treat blockchains as general purpose databases or general purpose computers, Blockstack uses blockchain as a Decentralized mechanism to establish trust and shared state while pushing the majority of code and data storage"to the edges", or off-chain

Blockstack  architecture results in not having to deal with scalability and complexity constraints coming from having to store everything on chain. 

### Apps built with Blockstack can:
- Leverage commodity web infrastructure
- Scale to levels comparable to centralized web services that exist today

## Blockstack.js - Authentication 
Code block that represents signin behavioural logic:
```javascript
import blockstack from 'blockstack'
document.getElementById('signIn').oneClick = () => {
  blockstack.redirectToSignIn()
}
```

### Requesting additional permissions
```javascript
blockstack.redirectToSignIn(
  // redirectURI - default value
  window.location.origin,
  // manifestURI - default value
  window.location.origin + '/manifest.json',
  // permissions - ask for user's email
  ['store_write', 'email']
)
```

### Blockstack Browser: 
Blockstack browser is just a client-side web application where the user can manage their blockstack id.

All private user data, like private keys and emails, are all stored client-side in local storage.

All authetnication logic (all logic) is performed client-side, nothing is on centralized servers.

For decentralization purposes, users are recommended to download the Blockstack Browser locally.
The Blockstack 

Blockstack Mobile (iOS and Android) are WIPs

##### Blockstack apps are required to host a manifest.json file
E.g. *helloblockstack.com/manifest.json*

```javascript
{
  "name": "Hello, Blockstack",
  "start_url": "helloblockstack.com",
  "description": "A simple demo of Blockstack auth and storage",
  "icons": [{
    "src": "http://helloblockstack.com/carrot.png",
    "sizes": "160x160",
    "type": "image/png"
  }]
}
```

Manifest file is where you can customize, or 'brand', your App description, which is shown in the blockstack browser sign-in prompt.
The manifest.json file is also necessary to validate domain name ownership, which is useful for preventing malicious actors from forging authentication requests on behald of other apps.

Location of manifest file must be on the same origin as the app requesting authentication.
This is to prevent malicious apps from making auth requests on behalf of other apps.

#### Complete the auth flow after user is redirected back to your app
```javascript
// Check for the auth response token in the URL, provided by the browser redirect.
if (blockstack.isSignInPending()) {
  // Decode the token and retrieves user data
  blockstack.handlePendingSignIn().then( () => {
    window.location = window.origin // refresh main page once signed in
  })
}
```

Get user data after sign in 
```javascript
if (blockstack.isUserSignedIn()) {
  var profile = blockstack.loadUserData().profile
  // Do something with user profile data...
  showProfile(profile)
}
```
