[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Account Module

### Authentication & Authorization


<details>
  <summary>Registration flow</summary>
  
![Registration flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/registration.png)

##### Endpoints
We expose two endpoints for registration flow

###### 1. Check if login is available
   * Path: */auth/check*
   * Http method: *POST*
   * Body type: JSON
   * Body fileds:
     * ***email*** - **mandatory** parameter, must be valid email
   * Body example: *{"email" : "user@email.com"}*
   * Response type: JSON
   * Response example: 
      * available: *{ "status" : "success"}*
      * not available: *{ "status" : "failed" }*
   
###### 2. Create account
   * Path: */auth/register*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***email*** - **mandatory** parameter, must be valid email
     * ***password*** - **mandatory** parameter
     * *first* - optional parameter - first name
     * *last* - optional parameter - last name
   * Body example: {"email" : "user@email.com", "password" : "wuy8632k!h89sd#"}
   * Response type: JSON
   * Response example:  
      * success: *{ "status" : "sucsess", "body" : {"accountId" : "l93kdf8"}}*
      * failed:  *{ "status" : "failed"}*
  
###### 3. Confirm account registration
   * Path: */account/confirm*
   * Http method: *POST*
   * Body type: EMPTY
   * Response type: JSON
   * Response example:  
      * success: *{ "status" : "success"}*
      * failed:  *{ "status" : "failed"}*
  
###### 4. Decline account registration
   * Path: */account/decline*
   * Http method: *POST*
   * Body type: EMPTY
   * Response type: JSON
   * Response example:  
      * success: *{ "status" : "success"}*
      * failed:  *{ "status" : "failed"}*
   
##### Steps
* User executes request on */account/check* url 
with required json body. 
It allows to be sure there is no user 
with the same login. If login is available 
then go to the next step
*  User executes request on */account/register* 
and creates account. 
*  Password must be encrypted on db.
* User receives email with confirmation url
* User executes call on confirmation or declining url */account/{accountId}/confirm*

</details>
<details>
  <summary>Login flow</summary>

![Login flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/login.png)

##### Endpoints
We expose one endpoint for login flow

###### 1. Login user
   * Path: */auth/login*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***email*** - **mandatory** parameter
     * ***password*** - **mandatory** parameter
   * Body example: *{"email" : "user@email.com", "password" : "wuy8632k!h89sd#"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"token" : "lkjdsf6si7fd987fgh867sduoi3k3b"} }*
      * failed: *{ "status" : "failed" }*

  </details>
<details>
  <summary>Reset password</summary>

![Reset password flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/resetPassword.png)

##### Endpoints
We expose one endpoint for reset password flow

###### 1. Reset password
   * Path: */auth/password/reset*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***email*** - **mandatory** parameter
   * Body example: *{"email" : "user@email.com"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
##### Steps
* User executes request on */account/password/reset* url 
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


### Account management

<details>
  <summary>Change password flow</summary>

![Change password flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/changePassword.png)


##### Endpoints
We expose one endpoint for change password flow

###### 1. Change password
   * Path: */account/password/change*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * ***new_password*** -  **mandatory** parameter
   * Body example: *{"new_password" : "jd7_g2$hj"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */account/password/change* url 
with required json body and jwt token on headers/parameters. Application checks if there is such user. If there is no such user we should send failed response 
on request and stop execution otherwise proceed to the next step.
*  Update user profile with new password
*  Send confirmation email to user

  </details>
  <details>
  <summary>Update account flow</summary>

![Update profile flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/updateProfile.png)

##### Endpoints
We expose one endpoint for profile updating

###### 1. Update profile
   * Path: */account/update*
   * Http method: *POST*
   * Body type: JSON
   * Body fields:
     * *fullName* - optional parameter
   * Body example: *{"first" : "John", "last":"Smith"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */account* url 
with required json body and jwt token on headers
*  Update user profile with required fields

  </details>
  <details>
  <summary>Join space</summary>

![Join space flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/ imp should be updated updateSpaces.png)

##### Endpoints
We expose one endpoint for joining required space

###### 1. Join space
   * Path: */account/space/{space_id}/join*
   * Http method: *POST*
   * Body type: EMPTY
   * Path params:
     * *space_id* - mandatory parameter
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */account/space/join/{space_id}* url 
with required path parameter *spaceId* and jwt token on headers. User could join up to 5 different spaces (more for paid accounts)
*  Update user profile with required space id

  </details>
  <details>
  <summary>Leave space</summary>

![Leave space flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/ imp should be updated updateSpaces.png)

##### Endpoints
We expose one endpoint for leaving required space

###### 1. Leave space
   * Path: */account/space/{space_id}/leave*
   * Http method: *POST*
   * Body type: EMPTY
   * Path params:
     * *space_id* - mandatory parameter
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */account/space/{space_id}/leave* url 
with required path parameter *spaceId* and jwt token on headers. 
*  Update user profile and remove requested space id

  </details>
  <details>
  <summary>Close account</summary>

![Close account flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/closeAccount.png)

We expose two endpoints for closing account

###### 1. Close account request
   * Path: */account/close*
   * Http method: *POST*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

###### 2. Confirm account closing
   * Path: */account/close/confirm*
   * Http method: *POST*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*
###### 3. Confirm account closing
   * Path: */account/close/decline*
   * Http method: *POST*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

##### Steps
* User executes request on */account/close* url
* Application changes account status to *suspended*
and send confirmation email with confirmation and rejection urls 
* User either confirm or reject closing account
* If user confirmed closing account then application delete all account information
* If user rejected closing account status should be changed back to active
* If user ignores confirmation email... What should we do?

  </details>
  
  ### Classes
  <details>
    <summary>Account Class</summary>
 
  #### Model Description
  * Purpose: keep user info structure and corresponding db methods
  * Fields:
    * id 
    * first
    * last
    * email
    * password
    * spaces[] - by default this list contains only *global* space, max number of spaces is 5
    * status - possible values: pending, active, suspended, closed
    * create_time
    * update_time    
  </details>
 
 