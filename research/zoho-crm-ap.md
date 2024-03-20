# Zoho CRM AP

### Refresh Access Token:&#x20;

How does authentication work on our project: When pressing login we redirect to the login url from zoho. After the user accepts he gets redirected back to the LoginRedirect and gets the access token in the url and it gets send to the authContext. SetToken witch saves the token to local storage.

The info in red in irrelevant to our project but was recommended by the bad zoho documentation

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<mark style="color:red;">{Accounts\_URL}/oauth/v2/token?refresh\_token={refresh\_token}\&client\_id={client\_id}\&client\_secret={client\_secret}\&grant\_type=refresh\_token</mark>&#x20;

<mark style="color:red;">If the request is successful, you will receive the following output:</mark>



`{`&#x20;

&#x20;   `"access_token": "{new_access_token}",`&#x20;

&#x20;   `"expires_in": 3600,`&#x20;

&#x20;   `"api_domain": "https://www.zohoapis.com",`&#x20;

&#x20;   `"token_type": "Bearer"`&#x20;

`}`&#x20;

[<mark style="color:red;">https://www.zoho.com/crm/developer/docs/api/v6/refresh.html Refresh</mark>](#user-content-fn-1)[^1] <mark style="color:red;">Token</mark>&#x20;

&#x20;<mark style="color:red;">Refresh tokens do not expire until a user revokes them.</mark>&#x20;

<mark style="color:red;">You can generate a maximum of 10 access tokens from a refresh token in a span of 10 minutes.</mark>&#x20;

<mark style="color:red;">You can generate a maximum of 20 refresh tokens in a span of 10 minutes per client ID.</mark>&#x20;

<mark style="color:red;">When you generate the 21st refresh token, the first created refresh token gets deleted.4</mark>&#x20;

<mark style="color:red;">To generate a refresh token</mark>&#x20;

\
<mark style="color:red;">Make a POST request with the following URL. Replace {Accounts\_URL} with your domain-specific Zoho accounts URL when you make the request. {Accounts\_URL}/oauth/v2/token</mark>&#x20;

<mark style="color:red;">Note:</mark>&#x20;

<mark style="color:red;">For security reasons, pass the below parameters in the body of your request as form-data.</mark>&#x20;

<mark style="color:red;">Request Parameters grant type Enter the value as "authorization\_code". client\_id Specify client-id obtained from the connected app.</mark>&#x20;

<mark style="color:red;">client\_secret Specify client-secret obtained from the connected app.</mark>&#x20;

<mark style="color:red;">redirect\_uri Specify the Callback URL that you registered during the app registration.</mark>&#x20;

<mark style="color:red;">code Enter the grant token generated from previous step. If the request is successful, you would receive the following:</mark>&#x20;

`{`

&#x20;`"access_token": "{access_token}",`&#x20;

`"refresh_token": "{refresh_token}",`&#x20;

`"api_domain": "https://www.zohoapis.com",`&#x20;

`"token_type": "Bearer", "expires_in": 3600`&#x20;

`}`

<mark style="color:red;">Error met de code request</mark>&#x20;

<mark style="color:red;">We encountered errors while attempting to request the code instead of the token because we can utilize the code to request both the access token and refresh token.</mark>

#### conclusion:

After conducting further research, I've come to realize that all the data I've gathered so far is useless.\
It appears that although the documentation didn't explicitly state it, the process they outlined is intended for a server-based application, but we are trying to develop a client-based application so its natulal that we encounter errors.

https://www.zoho.com/accounts/protocol/oauth/js-apps/access-token.html[^2]

The explanation says that for a client-based application, you need to request the authentication token through a link just like we where doing. Upon logging in to the Zoho authentication, they will be redirected back to the application. Example :\
<mark style="background-color:orange;">https://accounts.zoho.com/oauth/v2/auth? client\_id=1000.GMB0YULZHJK411248S8I5GZ4CHUEX0& response\_type=token& scope=AaaServer.profile.Read& redirect\_uri=https://www.zylker.com/oauthredirect</mark>

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

To refresh a token is pretty easy all we need to do is redirect the user to a zoho refresh URL that immediately sends a redirects back to your project together with a new URL Example : <mark style="background-color:orange;">https://accounts.zoho.com/oauth/v2/auth/refresh? client\_id=1000.GMB0YULZHJK411248S8I5GZ4CHUEX0& response\_type=token& scope=AaaServer.profile.Read& scope=AaaServer.profile.Read& redirect\_uri=https://www.zylker.com/oauthredirect</mark>

#### Things to keep in mind :

1. The authentication token gets updated each time the user does a refresh If u try to refresh a token while the your logged out of your zoho account u won't get a authentication token back.
2. If u try to refresh a token in a different session u wont get a authentication token back.
3. U can only do 20 refreshments if a span of 20min.
4. And only 10 authentications in a span of 10min.
5. If u alter a authentication token u wont be able to refresh.
6. One authentication key can be used across browser tabs
7. U need to give acces for the whole session otherwise u want be able to refresh

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### quick way to switch between logged in users:&#x20;

Ive searched around and found that Zoho Chat Cliq has a similar feature, but it's only accessible within their internal products.&#x20;

https://help.zoho.com/portal/en/kb/zoho-cliq/user-guides/getting-started/create-a-cliq-account/articles/multi-account-login-support-for-the-cliq-desktop-application#Managing\_Accounts

There is no mention in Zoho's documentation about similar functionality for switching between multiple users. Someone has already attempted something similar, but they haven't received a response from Zoho yet. https://help.zoho.com/portal/en/kb/accounts/faqs-troubleshooting/faqs/oneauth/articles/how-to-switch-between-multiple-zoho-accounts

Approach 1: the best way is if we kept all users loged in and refresh their tokens to keep them logged in unfortunately this wont work for us because each time a user logges in the previose user gets logged out which makes that users authentication key invalid.

Approach 2: I have a different idea for solving this problem. What if we create a fake user? This user would have access to all the information from the accounts. Then, we can call up the accounts and let the user choose from them. Once the choice is made, we can store the account's ID in the local storage.

Getting user from CRM may be useful in the future:\
https://help.zoho.com/portal/en/community/topic/how-to-get-user-id-from-crm[^3]

[^1]: 

[^2]: 

[^3]: 
