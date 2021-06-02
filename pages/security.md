
[<- to **content**](https://github.com/shardoc/shardoc.github.io)

## Security
Security is implemented based on jwt token.
Each http request to backend 
contains authentication header except those processed on AuthController

Header name: Authentication

Value: Bearer xxxxxx

where xxxxxx is jwt token 
which is generated on successful 
login request. More information on this [topic](https://flask-jwt-extended.readthedocs.io/en/stable/basic_usage/)
