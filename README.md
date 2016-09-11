## Install

Install with composer...  `composer require mikemclin/passport-custom-request-grant`

## Setup

* Add `MikeMcLin\Passport\CustomRequestGrantProvider` to your list of providers **after** `Laravel\Passport\PassportServiceProvider`.
* Add `getUserEntityByRequest($request)` method to your `User` model (or whatever model you have configured to work with Passport).
    * The method should accept an `Illuminate\Http\Request` object.
    * You should authorize and retrieve user based on this request
    * If you find that the request met your requirement, return the User model.
    * If the request did not satisfy your requirement, return `null`

## How to use

* Make a **POST** request to `https://your-site.com/oauth/token`, just like you would a **Password** or **Refresh** grant.
* The POST body should contain `grant_type` = `custom_request`.
* The request will get routed to your `User::getUserEntityByRequest()` function, where you will determine if access should be granted or not.
* An `access_token` and `refresh_token` will be returned if successful.