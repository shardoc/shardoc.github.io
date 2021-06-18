[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Document Module


<details>
  <summary>Document storing (in process)</summary>

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/createDocument.png)

We expose one endpoint for Document storing

###### 1. Create record
   * Path: */createDocument*
   * Http method: *POST*
   * Body type: *FormData*
   * Body example: *document:{"files":\["fileName" : "some_cv.pdf"\], "notes":\["given file requires postprocessing"\], "tags":\["healthcare","sale"\], "spaces" : \["global"\]},
                    files :<fileData>*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8"} }*
      * failed: *{ "status" : "failed" }*
	  ##### Steps
* User executes request on */createDocument* url
* 
</details>
<details>
  <summary>Attach File</summary>

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/attachFile.png)
We expose one endpoint for attaching file to existing document
###### 1. Attach file
   * Path: */upload/{documentId}*
   * Http method: *POST*
   * Body type: *FormData*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess"}
      * failed: *{ "status" : "failed" }*

##### Steps
* xxx

***Additional Info***
[upload file in flask](https://pythonbasics.org/flask-upload-file/)
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
    * files[] - list of attached files
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
