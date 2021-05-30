# Shardoc documentation pages

https://guides.github.com/features/mastering-markdown/

## Idea
Shardoc allows you creating shared spaces 
where you and colleagues could find required
files.
User can share files within own circle,
 make it fully public or keep it private.
Use can share file for free or ask payment.

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
login request. More information on this topic https://codeburst.io/jwt-authorization-in-flask-c63c1acf4eeb

##### Registration
![Registration flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/registration.png)

###### We expose two endpoints for registration flow

**1. Check if login is available**
   * Path: */check*
   * Http method: *POST*
   * Body type: JSON
   * Body value: *{"email" : "user@email.com"}*
   * Response type: JSON
   * Response example: 
      * available: *{ "status" : "success" }*
      * not available *{ "status" : "failed" }*
   
**2. Create account**
   * Path: */register*
   * Http method: *POST*
   * Body type: JSON
   * Body example: 
      * success *{ "status" : "sucess", "body" : {"email" : "user@email.com", "password" : "wuy8632k!h89sd#"}}*
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
    * firstName
    * lastName
    * login
    * password
    * email
    * createTime
    * updateTime
2. 
  * Name: **AuthController**
  * Purpose: describe authentication API
  * Methods:
    * checkLogin
    * registerAccount

##### Login flow
![Login flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/login.png)
##### Logout flow
Implemented on UI
##### Roles
For now it's flat structure. No roles introduced

#### User profile

### File

#### File storage

#### File analyzer

#### File search & advices

#### File sharing

### Communication

### Payment flow
