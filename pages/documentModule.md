[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Document Module


<details>
  <summary>Document storing</summary>

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/documentStoring.png)

We expose two endpoints for Document storing

###### 1. Create record
   * Path: */createDocument*
   * Http method: *POST*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8"} }*
      * failed: *{ "status" : "failed" }*

###### 2. Upload file
   * Path: */upload/{documentId}*
   * Http method: *POST*
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
### Document search & advices

### Document sharing

### Document analyzer

### Classes
   <details>
  <summary>Document Class</summary>
  
  * Purpose: keep document info structure and corresponding db methods
  * Fields:
    * id 
    * fileName
    * notes[] - id values of corresponding note records
    * tags[] - string values
    * spaces[] - by default this list contains only *global* space, max number of spaces is 5
    * content
    * createTime
    * updateTime
  * Methods:
    * findById
    * update
    * insert
    * delete

    </details>
