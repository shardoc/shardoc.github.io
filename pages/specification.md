[<- to **content**](https://github.com/shardoc/shardoc.github.io)

# Modules

## Account Module

### Authentication & Authorization


<details>
  <summary>Registration flow</summary>
  
![Registration flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/registration.png)

##### Endpoints
We expose two endpoints for registration flow

###### 1. Check if login is available
   * Path: */check*
   * Http method: *POST*
   * Body type: JSON
   * Body fileds:
     * ***login*** - **mandatory** parameter, must be valid email
   * Body example: *{"login" : "user@email.com"}*
   * Response type: JSON
   * Response example: 
      * available: *{ "status" : "success" }*
      * not available: *{ "status" : "failed" }*
   
###### 2. Create account
   * Path: */register*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***login*** - **mandatory** parameter, must be valid email
     * ***password*** - **mandatory** parameter
     * *fullName* - optional parameter
   * Body example: {"login" : "user@email.com", "password" : "wuy8632k!h89sd#"}
   * Response type: JSON
   * Response example:  
      * success: *{ "status" : "sucess", "body" : {"accountId" : "l93kdf8"}}*
      * failed:  *{ "status" : "failed", "body" : ""}*
   
##### Steps
* User executes request on */check* url 
with required json body. 
It allows to be sure there is no user 
with the same login. If login is available 
then go to the next step
*  User executes request on */register* 
and creates account. 
*  Password must be encrypted on db.

</details>
<details>
  <summary>Login flow</summary>

![Login flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/login.png)

##### Endpoints
We expose one endpoint for login flow

###### 1. Login user
   * Path: */login*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***login*** - **mandatory** parameter
     * ***password*** - **mandatory** parameter
   * Body example: *{"login" : "user@email.com", "password" : "wuy8632k!h89sd#"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

  </details>
<details>
  <summary>Reset password</summary>

![Reset password flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/resetPassword.png)

##### Endpoints
We expose one endpoint for reset password flow

###### 1. Reset password
   * Path: */resetPassword*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***login*** - **mandatory** parameter
   * Body example: *{"login" : "user@email.com"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
##### Steps
* User executes request on */resetPassword* url 
with required json body. Application checks if there is such user. If there is no such user we should send positive response 
on request and stop execution otherwise proceed to the next steps
*  Application generates jwt token with expiration period 24 hours
*  Application sends email to user with reset password url which leads to [changePassword API](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md#1-change-password-flow)
*  Send positive response on initial request
*  To change pasword user should proceed with [changePassword API](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md#1-change-password-flow) with the help of url from email
  </details>
<details>
  <summary>Logout flow</summary>

Implemented on UI
  </details>


### Profile management

<details>
  <summary>Change password flow</summary>

![Change password flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/changePassword.png)


##### Endpoints
We expose one endpoint for change password flow

###### 1. Change password
   * Path: */changePassword*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***oldPassword*** - **mandatory** parameter
     * ***new password*** -  **mandatory** parameter
   * Body example: *{"oldPassword" : "hi&7hh4+", "new password" : "jd7_g2$hj"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */changePassword* url 
with required json body and jwt token on headers/parameters. Application checks if there is such user with given old password. If there is no such user we should send failed response 
on request and stop execution otherwise proceed to the next step.
*  Update user profile with new password
*  Send confirmation email to user

  </details>
  <details>
  <summary>Update profile flow</summary>

![Update profile flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/updateProfile.png)

##### Endpoints
We expose one endpoint for profile updating

###### 1. Update profile
   * Path: */updateProfile*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * *fullName* - optional parameter
   * Body example: *{"fullName" : "John Smith"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */updateProfile* url 
with required json body and jwt token on headers
*  Update user profile with required fields

  </details>
  <details>
  <summary>Update spaces</summary>

![Update spaces flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/updateSpaces.png)

##### Endpoints
We expose one endpoint for joining required spaces

###### 1. Update spaces
   * Path: */updateSpaces*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * *spaces* - mandatory parameter
   * Body example: *{"spaces" : ["hd5h46gh", "hz5h57h"]}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */updateSpaces* url 
with required json body and jwt token on headers. Body field ***spaces*** 
is array  and could contain between 1 and 5 different spaces (more for paid accounts)
*  Update user profile with required spaces id

  </details>
  <details>
  <summary>Close account</summary>

![Close account flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/closeAccount.png)

We expose two endpoints for closing account

###### 1. Close account request
   * Path: */closeAccount*
   * Http method: *DELETE*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

###### 2. Confirm account closing
   * Path: */closeAccountConfirmation/{yes/no}*
   * Http method: *DELETE*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */closeAccount* url
* Application changes account status to *suspended*
and send confirmation email with confirmation and rejection urls 
* User either confirm or reject closing account
* If user confirmed closing account then application delete all account information
* If user rejected closing account status should be changed back to active
* If user ignores confirmation email... What should we do?

  </details>
  <details>
  <summary>Classes</summary>

1. Class **AccountModel**
  * Purpose: structure and keep info about user
  * Fields:
    * id 
    * fullName
    * login
    * password
    * spaces[] - by default this list contains only *global* space, max number of spaces is 5
    * status - possible values: pending, active, suspended, closed
    * createTime
    * updateTime
  * Methods:
    * findByLogin
    * update
    * insert
    * delete
    
2. Class **AuthController**
  * Purpose: describe authentication API
  * Methods:
    * checkLogin
    * registerAccount
    * login

3. Class **AccountController**
  * Purpose: describe authentication API
  * Methods:
    * updatePassword
    * updateProfile
    * updateSpaces
    * closeAccount
</details>

## File Module

### File storage

### File analyzer

### File search & advices

### File sharing

## Communication Module

## Payment Module

