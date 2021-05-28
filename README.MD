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
login request. Mo reinformation othis topic https://codeburst.io/jwt-authorization-in-flask-c63c1acf4eeb

##### Registration
##### Login flow
![Login flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/auth.png)
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
