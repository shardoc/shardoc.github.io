[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Document Module


<details>
  <summary>Document storing</summary>

### Endpoints
We expose two endpoints for Document storing

#### 1. Create Document
   * Path: */document/create/force* and */document/create*
   * Http method: *POST*
   * Body type: *FormData*
   * Body example: *document:{"tags":["healthcare","sale"], "spaces" : ["hw7wh34"]},
                    document_file :<fileData>*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8"} }*
      * failed: *{ "status" : "failed", "error":"duplicates", "body" : {"documents" : [{id:"l93k7df8", "title":"Some other doc"}] }*
	  
#####	 Scenario 1: Create Document without flag force. Success flow.
![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/createDocumentForceFalseSuccess.png)
	  
###### Steps
* User executes request on */document/create* url
* Application checks if there is no already files with the same name attached to other documents

* If file with the same name is found list of documents which could be duplicates and response 
"failed: { "status" : "failed", "error":"duplicates", "body" : {"documents" : [{id:"l93k7df8", "title":"Some other doc"}] }"
is returned.

* If theres in no file with the same name
* Application creates document based on JSON from field document
* Application saves file on the file system

#####	 Scenario 2: Create Document with flag force.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/createDocumentForceTrue.png)
	  
###### Steps
* User executes request on */document/create/force* url
* Application checks if there is no already files with the same name attached to other documents 
* There are files with the same name

* Rename file with help of proper ending line file_1.pdf, file_2.pdf
* Application creates document based on JSON from field document
* Application saves files on the file system

</details>

<details>
  <summary>Update Document</summary>

### Endpoints

We expose one endpoint for updating field on document

#### 3. Update Field
   * Path: */document/{document_id}/update*
   * Http method: *POST*
   * PATH parameters: *document_id* - value any valid id
   * Body type: *JSON*
   * Body example: *{"title":"Updated Title"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess" }
      * failed: *{ "status" : "failed", "error":"Cannot update field [title]" }*

#####	 Scenario 1: Update field.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/updateDocumentField.png)

###### Steps
* User executes request on */document/{document_id}/update* url and pass proper body
* Application validates data (user can update only visible fields like *title*, *tags*, etc. Except field *document_file*, that filed has dedicate API method)
* Application updates field

</details>
<details>
  <summary>Replace Files in Document</summary>

### Endpoints

We expose two endpoints for replacing file in existing document

#### 3. Replace files
   * Path: */document/{document_id}/attach/force* and */document/{document_id}/attach*
   * Http method: *POST*
   * PATH parameters: *document_id* - value any valid id
   * Body type: *FormData*
   * Body example: *document_file :<fileData>*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess", "body" : {"filename" : "file_1.pdf"} }
      * failed: *{ "status" : "failed", "error":"duplicates", "body" : {"documents" : [{id:"l93k7df8", "title":"Some other doc"}] }*

#####	 Scenario 1: Replace file with flag force equals false. Success flow.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/attachFileForceFalseSuccess.png)

###### Steps
* User executes request on */document/{documentId}/attach* url
* Application checks if there is no already files with the same name attached to other documents
* No files with the same name
* Application saves files on the file system
* Each user should have own folder with files
* File size should be limited, size of file storage should be limited as well depends on user subscription ?
* Application updates field *files* on document with given *documentId* 

	  
#####	 Scenario 2: Replace file with flag force equals false. Failed flow.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/attachFileForceFalseFail.png)

###### Steps
* User executes request on */document/{documentId}/attach* url
* Application checks if there is no already files with the same name attached to other documents
* There are files with the same name
* Application finds documents with attached files with the same name
* Application returns fail response with list of documents which could be duplicates


#####	 Scenario 3: Replace file with flag force equals true.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/attachFileForceTrue.png)

###### Steps
* User executes request on */document/{documentId}/attach/force* url
* Application checks if there is no already files with the same name attached to other documents
* There are files with the same name
* Rename file with help of proper ending line file_1.pdf, file_2.pdf
* Application creates document based on JSON from field ***document***
* Application saves files on the file system
* Application updates field *files* on document with given *documentId* 



***Additional Info***
[upload file in flask](https://pythonbasics.org/flask-upload-file/)
  </details>
  <details>
  <summary>Get Document</summary>

### Endpoints

We expose two endpoints for a fetching documents

#### 1. Get document by id
   * Path: */document/{documentId}*
   * Http method: *GET*
   * PATH parameters: *documentId* - value *any valid document id*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "jsd98sd", "files":["fileName", "some_cv.pdf"], "tags":["healthcare","sale"], "spaces" : ["global"]}}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
	  
#### 2. Get all own documents
   * Path: */document?p={page}&s={size}*
   * Http method: *GET*
   * Query parameters: *page* - page number, value *positive number*; *size* - page size, value *positive number* 
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"id" : "jsd98sd", "files":["fileName" : "some_cv.pdf"], "tags":["healthcare","sale"], "spaces" : ["global"]}]}*
      * failed: *{ "status" : "failed", "error":"unknown" }*

</details>
  <details>
  <summary>Delete Document</summary>

### Endpoints

We expose one endpoint for a removing documents

#### 1. Delete documents by list of id
   * Path: */document*
   * Http method: *POST*
   * Body type: *JSON*
   * Body example: *{"idList":["id1", "id2", "id3"]}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"idList":["id1", "id2", "id3"]}}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
	
</details>
<details>
<summary>Document search & advices</summary>
  
### Endpoints

We expose two endpoints for a finding proper documents in user's own document storage or advice apropriate document from other users


#### 1. Search own documents by title or tags
   * Path: */document/search?p={page}&s={size}&q={query}*
   * Http method: *POST*
   * Query parameters: *p as a page* - page number, value *positive number*; *s as a size* - page size, value *positive number*, *q as a query* - user query
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"files":["fileName" : "some_cv.pdf"], "tags":["healthcare","sale"], "spaces" : ["global"]}]}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
	  
#### 2. Advice documents by title or tags in global area
   * Path: */document/advice?p={page}&s={size}&q={query}*
   * Http method: *GET*
   * Query parameters: *p as a page* - page number, value *positive number*; *s as a size* - page size, value *positive number*, *q as a query* - user query
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"owner":{"id":"otherUserId", "fullName": "otherUserFullName"}, "title":"masked title"},{"owner":{"id":"otherUserId2", "fullName": "otherUserFullName2"}, "title":"masked title2"}]*
      * failed: *{ "status" : "failed", "error":"unknown" }*
			  
#####	 Scenario 1: Advice documents

![Advice documents](https://github.com/shardoc/shardoc.github.io/blob/dev/images/adviceDocuments.png)

###### Steps
* User executes request on */document/advice* url
* Application get user's spaces
* Application search for documents on allowed spaces
* Application prepares documents depends on space visibility rules
</details>


<details>
  <summary>Document sharing</summary>
  
  ### Endpoints
  Purpose of current API providing other user access to your document(s). We expose three endpoints: one for requesting document and another two for sharing with or without payment.
  When user shares his/her document in fact that document will be copied and recepient will be assigned as an owner on document copy!!!
  
  
  #### 1. Request document
   * Path: */document/share/request*
   * Http method: *POST*
   * Body type: *JSON*
   * Body example: *{"documentIdList":["id1","id2",...,"idN"]}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "khd65dfkld", "status" :"inprogress"}}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
	  
  #### 2. Share with payment
   * Path: */document/share/{shareId}/payment*
   * PATH parameters: *shareId* - id of share data 
   * Http method: *POST*
   * Body type: *JSON*
   * Body example: *{"price" :{"amount" : "100", "currency" : "usd"}}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "ljldf786sds", "status" :"requested" }*
      * failed: *{ "status" : "failed", "error":"unknown" }*
  
  #### 3. Share without payment
   * Path: */document/share/{shareId}*
   * Http method: *GET*
   * PATH parameters: *shareId* - id of share data 
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "ljldf786sds", "status" :"shared" }*
      * failed: *{ "status" : "failed", "error":"unknown" }*
	  
  #### 4. Reject document sharing request
   * Path: */document/share/{shareId}/reject*
   * Http method: *GET*
   * PATH parameters: *shareId* - id of share data 
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "ljldf786sds", "status" :"rejected" }}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
	  
  #### 5. Cancel document sharing request
   * Path: */document/share/{shareId}/cancel*
   * Http method: *GET*
   * PATH parameters: *shareId* - id of share data 
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success",  "body" : {"id" : "ljldf786sds", "status" :"cancelled" }}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
  
  
  </details>

<details>
<summary>Document analyzer</summary>

TBD:  with the help of AI we will analyze content of uploaded document and build some searchable index
</details>

### Classes

   <details>
  <summary>Document Class</summary>
  
#### Model Description
  * Purpose: keep document info structure and corresponding db methods
  * Fields:
    * id 
	* ownerId
	* title
    * files[] - list of attached files
    * notes[] - notes added by user
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
	
	 <details>
  <summary>Note Class</summary>
  
#### Model Description  
  * Purpose: keep note structure, could be reused on other modules
  * Fields:
    * id 
	* ownerId
	* text
    * createTime
    * updateTime

    </details>
	
	
	
	<details>
 <summary>ShareData Class</summary>
  
#### Model Description
  * Purpose: keep infromation about document sharing
  * Fields:
    * id 
	* ownerId
	* recipientId
	* documentId
	* price 
	  * amount" 
	  * currency
	* status - possible values: *requested*, *canceled*, *priced*, *shared*, *rejected*, *completed*
    * createTime
    * updateTime
    </details>
