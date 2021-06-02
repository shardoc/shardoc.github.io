[<- to **content**](https://github.com/shardoc/shardoc.github.io)

# Modules

## User

### Security (registration/login/logout/roles?)

Security is implemented based on jwt token.
Each http request to backend 
contains authentication header

Header name: Authentication

Value: Bearer xxxxxx

where xxxxxx is jwt token 
which is generated on successful 
login request. More information on this [topic](https://flask-jwt-extended.readthedocs.io/en/stable/basic_usage/)
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
then go to *step2*
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



#### 4. Logout flow
Implemented on UI

#### 5. Roles
For now it's flat structure. No roles introduced

### Profile management

#### 1. Change password flow

#### 2. Update profile flow

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