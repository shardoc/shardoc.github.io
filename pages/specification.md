[<- to **content**](https://github.com/shardoc/shardoc.github.io)

## Modules

### User

#### Security (registration/login/logout/roles?)

Security is implemented based on jwt token.
Each http request to backend 
contains authentication header

Header name: Authentication

Value: Bearer xxxxxx

where xxxxxx is jwt token 
which is generated on successful 
login request. More information on this [topic](https://flask-jwt-extended.readthedocs.io/en/stable/basic_usage/)
##### Registration flow
![Registration flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/registration.png)

###### We expose two endpoints for registration flow

**1. Check if login is available**
   * Path: */check*
   * Http method: *POST*
   * Body type: JSON
   * Body fileds:
     * ***login*** - **mandatory** parameter
   * Body example: *{"login" : "user@email.com"}*
   * Response type: JSON
   * Response example: 
      * available: *{ "status" : "success" }*
      * not available *{ "status" : "failed" }*
   
**2. Create account**
   * Path: */register*
   * Http method: *POST*
   * Body type: JSON
   * Body fileds:
     * ***login*** - **mandatory** parameter, could be email
     * ***password*** - **mandatory** parameter
     * ***email*** - valid email value in format xxx@xxx.xxx, **mandatory** parameter
     * *fullName* - optional parameter
   * Body example: {"login" : "user@email.com", "password" : "wuy8632k!h89sd#"}
   * Response type: JSON
   * Response example:  
      * success *{ "status" : "sucess", "body" : {"accountId" : "l93kdf8"}}*
      * failed  *{ "status" : "failed", "body" : ""}*
   
###### Steps
1. User executes request on */check* url 
with required json body. 
It allows to be sure there is no user 
with the same login. If login is available 
then go to *step2*
2. User executes request on */register* 
and creates account. 
3. Password must be encrypted on db.

###### Classes
1. 
  * Name: **Account**
  * Purpose: structure and keep info about user
  * Fields:
    * id 
    * fullName
    * login
    * password
    * email
    * createTime
    * updateTime
  * Methods:
    * findByLogin
    *  
2. 
  * Name: **AuthController**
  * Purpose: describe authentication API
  * Methods:
    * checkLogin
    * registerAccount
    * login
    * updatePassword
    * updateProfile

##### Login flow
![Login flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/login.png)


#### Change password flow

#### Update profile flow

##### Logout flow
Implemented on UI
##### Roles
For now it's flat structure. No roles introduced



### File

#### File storage

#### File analyzer

#### File search & advices

#### File sharing

### Communication

### Payment flow
