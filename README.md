# AngularJS Social Login (socialLogin)
AngularJS Social Login Module is a simple client side authentication module which helps to authenticate your application using Google/Facebook/LinkedIN. It doesn't maintain any session, session between client application and server should be maintained by yourself after receiving user details from the provider.

Supported sites:
- Google
- Facebook
- LinkedIN

## Installation

### via bower

```shell
bower install angularjs-social-login --save
```

### configure installation

Include JS files:

```html
<script src="bower_components/angular-cookies/angular-cookies.js"></script>
<script src="bower_components/angularjs-social-login/angularjs-social-login.js"></script>
```

Then include `socialLogin` as a dependency for your app:

```javascript
angular.module('myApp', ['socialLogin']);
```

## Configuration

### Example

```javascript
app.config(function(socialProvider){
	socialProvider.setGoogleKey("YOUR GOOGLE CLIENT ID");
  socialProvider.setLinkedInKey({clientId: "CLIENT ID", authType: "<jsdk OR oauth>", scope: "r_basicprofile,r_emailaddress", state: "STATE", redirectUrl: "http://localhost:9000/oauth/linked_in"});
  //authType - 'jsdk' for static webpages where there is no backend, for simple authentication. 'oauth' for accessing various permissions from the user 
  //state - some number which helps to prevent from CSRF attacks. It is must for 'oauth'
  //redirectUrl - After successful authentication user will be redirected to this url.
  //For more information https://developer.linkedin.com/docs/oauth2
  socialProvider.setFbKey({appId: "YOUR FACEBOOK APP ID", apiVersion: "API VERSION"});
});
```

## Usage
There are total three directives for handling Google, Facebook, LinkedIn authentication.
- fbLogin (For Facebook)
- gLogin (For Google)
- linkedIn (For LinkedIn)

### Methods

- `socialProvider.setGoogleKey("YOUR GOOGLE CLIENT ID")`
- `socialProvider.setLinkedInKey("YOUR LINKEDIN CLIENT ID")`
- `socialProvider.setFbKey("YOUR FACEBOOK APP ID")`
- `$rootScope.$on('event:social-sign-in-success', function(event, userDetails){})` 
   Braodcast event which will be triggered after successful authentication. `userDetails` is an `Object` consists of `{name: <user_name>, email: <user_email>, uid: <UID by social vendor>, provider: <Google/Facebook/LinkedIN>, token: <Google ID token (only for google)>}` 
- `socialLoginService.logout()`
   For logout
- `$rootScope.$on('event:social-sign-out-success', function(event, logoutStatus){})`
   Braodcast event which will be triggered after successful logout.

### Example
```html
<button g-login type="button">Google Login</button>
<button linked-in type="button">LinkedIn Login</button>
<button fb-login type="button">facebook Login</button>
```

