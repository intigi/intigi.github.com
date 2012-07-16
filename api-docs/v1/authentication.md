---
layout: default
---

## API Authentication

We offer two ways of authentication to the API:

### Basic Auth with Username and Password

You can use HTTP Basic Authentication with your own login info:

`curl -u username:password https://intigi.com/api/v1/...`

### Basic Auth with Authentication Token

You can use HTTP Basic Authentication with your account's authentication token by replacing the username with your authentication token:

`curl -u [token goes here]:auth_token https://intigi.com/api/v1/...`

You can find your account's authentication token in the Intigi web app's user profile page. Navigate there by signing in to the web app and clicking on your email address in the top bar.

Make sure to keep your authentication token confidential, just like you do with your password. You can reset your token at any time by going to your user profile page in the Intigi web app and click "Reset My Authentication Token".
