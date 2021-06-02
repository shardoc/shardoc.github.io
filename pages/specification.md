[<- to **content**](https://github.com/shardoc/shardoc.github.io)

# Modules

## User

### Authentication & Authorization (registration/login/logout/roles?)


#### 1. Registration flow
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
   * Body fileds:
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



#### 2. Login flow
![Login flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/login.png)

##### Endpoints
We expose one endpoint for login flow

###### 1. Login user
   * Path: */login*
   * Http method: *POST*
   * Body type: JSON
   * Body fileds:
     * ***login*** - **mandatory** parameter
     * ***password*** - **mandatory** parameter
   * Body example: *{"login" : "user@email.com", "password" : "wuy8632k!h89sd#"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed" }*

#### 3. Reset password

![Reset password flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/resetPassword.png)

##### Endpoints
We expose one endpoint for login flow

###### 1. Reset password
   * Path: */resetPassword*
   * Http method: *POST*
   * Body type: JSON
   * Body fileds:
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

#### 4. Logout flow
Implemented on UI

#### 5. Roles
For now it's flat structure. No roles introduced

### Profile management

#### 1. Change password flow

![Change password flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/changePassword.png)

#### 2. Update profile flow

![Update profile flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/updateProfile.png)

### Classes
1. Class **AccountModel**
  * Purpose: structure and keep info about user
  * Fields:
    * id 
    * fullName
    * login
    * password
    * spaces[]
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
    * joinSpace

### File

#### File storage

#### File analyzer

#### File search & advices

#### File sharing

### Communication

### Payment flow
