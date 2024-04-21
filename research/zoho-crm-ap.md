# Zoho CRM AP

### Refresh Access Token:&#x20;

How does authentication work on our project? When pressing login, we are redirected to the login url from Zoho. After the user accepts he gets redirected back to the LoginRedirect and gets the access token in the url which gets sent to the authContext. SetToken, which saves the token to local storage.

{% embed url="https://www.zoho.com/accounts/protocol/oauth/js-apps/access-token.html" %}

The explanation says that for a client-based application, you need to request the authentication token through a link just like we were doing. Upon logging in to Zoho authentication, they will be redirected back to the application. Example :\
<mark style="background-color:orange;">https://accounts.zoho.com/oauth/v2/auth? client\_id=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx& response\_type=token& scope=AaaServer.profile.Read& redirect\_uri=https://www.zylker.com/oauthredirect</mark>

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

To refresh a token is pretty easy all we need to do is redirect the user to a zoho refresh URL that immediately sends a redirects back to your project together with a new URL Example : <mark style="background-color:orange;">https://accounts.zoho.com/oauth/v2/auth/refresh? client\_id=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx& response\_type=token& scope=AaaServer.profile.Read& scope=AaaServer.profile.Read& redirect\_uri=https://www.zylker.com/oauthredirect</mark>

#### Things to keep in mind :

1. The authentication token gets updated each time the user does a refresh If u try to refresh a token while the your logged out of your zoho account, u won't get a authentication token back.
2. If u try to refresh a token in a different session u wont get a authentication token back.
3. a refresh can happen even after a hour if its in the same sassion
4. And only 10 authentications in a span of 10min( on the same device and account ).
5. One authentication key can be used across browser tabs
6. U need to give acces for the whole session otherwise u want be able to refresh



<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

#### technical explanation of how il try to implement the auth refresh

It save a timestamp of the moment we get the timestamp in local storage.

It save the expires in that gets send back as a response.

It check each time the app is loaded to see when we last obtained a token. If it's less than an hour, the program will schedule a refresh according to the remaining time. For instance, if we have 30 minutes left before the token expires it will schedule a refresh for 20 minutes from the current time.

<figure><img src="../.gitbook/assets/Schermafbeelding 2024-03-25 152153.png" alt=""><figcaption></figcaption></figure>

flowcharts extra info :

* this flow repeats at each login refresh and when a tab is opened when you still have a valid auth token
* refresh = 50 // minutes&#x20;

### get currently logged in user&#x20;

{% embed url="https://www.zoho.com/crm/developer/docs/api/v6/get-users.html" %}

this was quit straight forward&#x20;

basically we do a  get and get back the currently logged in user,

We can request users by id or by type.&#x20;

example of a request `https://www.zohoapis.com/crm/v6/users?type=AllUsers`

list of all the type of users we can get :

* **AllUsers** - To list all users in your organization (both active and inactive users).
* **ActiveUsers** - To get the list of all the Active Users.
* **DeactiveUsers** - To get the list of all the users who were deactivated.
* **ConfirmedUsers** - To get the list of all the confirmed users.
* **NotConfirmedUsers** - To get the list of all the non-confirmed users.
* **DeletedUsers** - To get the list of deleted users.
* **ActiveConfirmedUsers** - To get the list of active users who are also confirmed.
* **AdminUsers** - To get the list of admin users.
* **ActiveConfirmedAdmins** - To get the list of active users with the administrative privileges who are also confirmed.
* **CurrentUser**: To get the current CRM user.

### getting images from zoho

To get a user image, add it on top of this link. Keep in mind that a user must be logged in to retrieve his image.

[https://accounts.zoho.eu/file?fs=thumb\&ID=](https://accounts.zoho.eu/file?fs=thumb\&ID=)

to get a product image, u will need to have the product id and the image id the product id needs to be added after the **entityId=** and the image id needs to be added after the **fileId=**

[https://crm.zoho.eu/crm/EntityImageAttach.do?action\_module=CustomModule2\&entityId=\&actionName=readImage\&fileId=](https://crm.zoho.eu/crm/EntityImageAttach.do?action\_module=CustomModule2\&entityId=\&actionName=readImage\&fileId=)





### loading data (will be added in the future)

currently were only getting 200 records wel need to add logic that keeps fetching data till all the data is fetched &#x20;

This wont be that had we just have to keep doing request till the more-records value is false.

[https://www.zoho.com/crm/developer/docs/api/v6/get-records.html](https://www.zoho.com/crm/developer/docs/api/v6/get-records.html)

[https://www.bigin.com/developer/docs/apis/get-records.html](https://www.bigin.com/developer/docs/apis/get-records.html)

### Refresh data when someone updates the data <mark style="color:red;">(will be added in the future)</mark>

Originally, I had an idea to add a timestamp value within the Zoho CRM. This timestamp would be updated whenever a user adds a PUT, enabling all devices accessing our website to compare the timestamps. Depending on the value, they could proceed with a refresh.

But after some research,it i found out they already have a similar feature. where they store the last updated time.

[https://www.zoho.com/crm/developer/docs/api/v6/modules-api.htm](https://www.zoho.com/crm/developer/docs/api/v6/modules-api.html)



<figure><img src="../.gitbook/assets/Schermafbeelding 2024-03-08 105759.png" alt=""><figcaption></figcaption></figure>

I am researching and also am doing research into stale data&#x20;

### search function in our project<mark style="color:red;">(will be added in the future)</mark> 

We have two options for implementing a search feature. First, we could opt for a local search within the data we already possess. Alternatively, we could utilize the search records functionality of the Zoho API.

If we choose to implement a local search, we'll gain greater search flexibility since we can ignore case sensitivity and utilize the include function, allowing users to search for partial matches. On the other hand, implementing the Zoho API search will require us to manage less data but we will get a worce responce

[https://www.zoho.com/crm/developer/docs/api/v6/search-records.html](https://www.zoho.com/crm/developer/docs/api/v6/search-records.html)



### quick way to switch between logged in users:&#x20;

Ive searched around and found that Zoho Chat Cliq has a similar feature, but it's only accessible within their internal products.&#x20;

[https://help.zoho.com/portal/en/kb/zoho-cliq/user-guides/getting-started/create-a-cliq-account/articles/multi-account-login-support-for-the-cliq-desktop-application#Managing\_Accounts](https://help.zoho.com/portal/en/kb/zoho-cliq/user-guides/getting-started/create-a-cliq-account/articles/multi-account-login-support-for-the-cliq-desktop-application#Managing\_Accounts)

There is no mention in Zoho's documentation about similar functionality for switching between multiple users. Someone has already attempted something similar, but they haven't received a response from Zoho yet. https://help.zoho.com/portal/en/kb/accounts/faqs-troubleshooting/faqs/oneauth/articles/how-to-switch-between-multiple-zoho-accounts

Approach 1: the best way is if we kept all users logged in and refresh their tokens to keep them logged in unfortunately this wont work for us because each time a user login the previous user gets logged out which makes that users authentication key invalid.

Approach 2: I have a different idea for solving this problem. What if we create a fake user? This user would have access to all the information from the accounts. Then, we can call up the accounts and let the user choose from them. Once the choice is made, we can store the account's ID in the local storage.

