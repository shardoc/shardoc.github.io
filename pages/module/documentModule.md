[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Document Module


<details>
  <summary>Document storing</summary>

### Endpoints
We expose one endpoint for Document storing

#### 1. Create Document
   * Path: */document/create/{force}*
   * Http method: *POST*
   * PATH parameters: *force* - value *true/false*
   * Body type: *FormData*
   * Body example: *document:{"files":\["fileName" : "some_cv.pdf"\], "notes":\["given file requires postprocessing"\], "tags":\["healthcare","sale"\], "spaces" : \["global"\]},
                    files :<fileData>*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8"} }*
      * failed: *{ "status" : "failed", "error":"duplicates", "body" : {"documents" : [{id:"l93k7df8", "title":"Some other doc"}] }*
	  
#####	 Scenario 1: Create Document with flag force equals false. Success flow.
![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/createDocumentForceFalseSuccess.png)
	  
###### Steps
* User executes request on */document/create/false* url
* Application checks if there is no already files with the same name attached to other documents
* No files with the same name
* Application creates document based on JSON from field ***document***
* Application saves files on the file system

#####	 Scenario 2: Create Document with flag force equals false. Fail flow.
![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/createDocumentForceFalseSuccess.png)
	  
###### Steps
* User executes request on */document/create/false* url
* Application checks if there is no already files with the same name attached to other documents
* There are files with the same name
* Application finds documents with attached files with the same name
* Application returns fail response with list of documents which could be duplicates

#####	 Scenario 3: Create Document with flag force equals true.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/createDocumentForceTrue.png)
	  
###### Steps
* User executes request on */document/create/true* url
* Application checks if there is no already files with the same name attached to other documents
* There are files with the same name
* Rename file with help of proper ending line file_1.pdf, file_2.pdf
* Application creates document based on JSON from field ***document***
* Application saves files on the file system
</details>

<details>
  <summary>Update Document</summary>

### Endpoints

We expose one endpoint for updating field on document

#### 3. Update Field
   * Path: */document/{documentId}/update*
   * Http method: *POST*
   * PATH parameters: *documentId* - value any valid id
   * Body type: *JSON*
   * Body example: *{"title":"Updated Title"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess" }
      * failed: *{ "status" : "failed", "error":"Cannot update field [title]" }*

#####	 Scenario 1: Update field.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/updateDocumentField.png)

###### Steps
* User executes request on */document/{documentId}/update* url and pass proper body
* Application validates data (user can update only visible fields like *title*, *tags*, etc. Except field *files*, that filed has dedicate API method)
* Application updates field

</details>
<details>
  <summary>Attach Files to Document</summary>

### Endpoints

We expose one endpoint for attaching file to existing document

#### 3. Attach files
   * Path: */document/{documentId}/attach/{force}*
   * Http method: *POST*
   * PATH parameters: *documentId* - value any valid id; *force* - value *true/false*
   * Body type: *FormData*
   * Body example: *files :<fileData>*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess", "body" : {"filename" : "file_1.pdf"} }
      * failed: *{ "status" : "failed", "error":"duplicates", "body" : {"documents" : [{id:"l93k7df8", "title":"Some other doc"}] }*

#####	 Scenario 1: Attach file with flag force equals false. Success flow.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/attachFileForceFalseSuccess.png)

###### Steps
* User executes request on */document/{documentId}/attach/false* url
* Application checks if there is no already files with the same name attached to other documents
* No files with the same name
* Application saves files on the file system
* Each user should have own folder with files
* File size should be limited, size of file storage should be limited as well depends on user subscription ?
* Application updates field *files* on document with given *documentId* 

	  
#####	 Scenario 2: Attach file with flag force equals false. Failed flow.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/attachFileForceFalseFail.png)

###### Steps
* User executes request on */document/{documentId}/attach/false* url
* Application checks if there is no already files with the same name attached to other documents
* There are files with the same name
* Application finds documents with attached files with the same name
* Application returns fail response with list of documents which could be duplicates


#####	 Scenario 3: Attach file with flag force equals true.

![Document storing flow sequence diagram](https://github.com/shardoc/shardoc.github.io/blob/dev/images/attachFileForceTrue.png)

###### Steps
* User executes request on */document/{documentId}/attach/true* url
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
      * success: *{ "status" : "success", "body" : {"files":\["fileName" : "some_cv.pdf"\], "notes":\["given file requires postprocessing"\], "tags":\["healthcare","sale"\], "spaces" : \["global"\]}}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
	  
#### 2. Get all own documents
   * Path: */document/{page}/{size}*
   * Http method: *GET*
   * PATH parameters: *page* - page number, value *positive number*; *size* - page size, value *positive number* 
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"files":\["fileName" : "some_cv.pdf"\], "notes":\["given file requires postprocessing"\], "tags":\["healthcare","sale"\], "spaces" : \["global"\]}]}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
   * Notes: Pay attention rpaging should be implemented on repository request

</details>
  <details>
  <summary>Delete Document</summary>

### Endpoints

We expose two endpoints for a removing documents

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
   * Path: */document/search/{page}/{size}*
   * Http method: *POST*
   * PATH parameters: *page* - page number, value *positive number*; *size* - page size, value *positive number* 
   * Body type: *JSON*
   * Body example: *{"value":"Lviv Java"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"files":\["fileName" : "some_cv.pdf"\], "notes":\["given file requires postprocessing"\], "tags":\["healthcare","sale"\], "spaces" : \["global"\]}]}*
      * failed: *{ "status" : "failed", "error":"unknown" }*
   * Notes: Pay attention rpaging should be implemented on repository request
	  
#### 2. Advice documents by title or tags in global area
   * Path: */document/advice/{page}/{size}*
   * Http method: *POST*
   * PATH parameters: *page* - page number, value *positive number*; *size* - page size, value *positive number* 
   * Body type: *JSON*
   * Body example: *{"value":"Lviv Java"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"owner":{"id":"otherUserId", "fullName": "otherUserFullName"}, "title":"masked title"},{"owner":{"id":"otherUserId2", "fullName": "otherUserFullName2"}, "title":"masked title2"}]*
      * failed: *{ "status" : "failed", "error":"unknown" }*
   * Notes: Pay attention rpaging should be implemented on repository request
			  
#####	 Scenario 1: Advice documents

![Advice documents](https://github.com/shardoc/shardoc.github.io/blob/dev/images/adviceDocuments.png)

###### Steps
* User executes request on */document/advice* url
* Application get user's spaces
* Application search for documents on allowed spaces
* Application prepares documents depends on space visibility rules
</details>

### Document sharing

### Document analyzer

### Classes

   <details>
  <summary>Document Class</summary>
  
  * Purpose: keep document info structure and corresponding db methods
  * Fields:
    * id 
	* owner
	* title
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
	
	<details>
  <summary>File Class</summary>
  
  * Nested class without own id
  * Purpose: describe attached file
  * Fields:
	* fileName
    * createTime
    </details>
