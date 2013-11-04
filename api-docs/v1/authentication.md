---
layout: default
---

## API Authentication

You can use HTTP Basic Authentication with your account's authentication token by replacing the username with your authentication token and the password with an arbitrary value:

`curl -u authentication_token:foo https://contentgems.com/api/v1/...`

You can find your account's authentication token in the ContentGems web app's user profile page. Navigate there by signing in to the web app and click 'Profile' in the top bar.

Make sure to keep your authentication token confidential, just like your password.
