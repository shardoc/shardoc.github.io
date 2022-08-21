[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Note Module


<details>
  <summary>Note adding</summary>

### Endpoints
We expose one endpoint for Note adding. This feature is used for adding notes on any required entity in a project.

#### 1. Add note
   * Path: */note/create*
   * Http method: *POST*
   * Body type: *JSON*
   * Body example: *{"entityId":"dhkfd", "entityType":"document", "content":"some comment on entity", "visibility':"private"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8"} }*
      * failed: *{ "status" : "failed", "error":"there is no such entity"}*
	  
</details>

<details>
  <summary>Update Note</summary>

### Endpoints

We expose one endpoint for updating field on space

#### 1. Update Field
   * Path: */note/{noteId}*
   * Http method: *POST*
   * PATH parameters: *noteId* - value any valid id
   * Body type: *JSON*
   * Body example: *{"content":"Updated Content"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess" }
      * failed: *{ "status" : "failed", "error":"Cannot update field [content]" }*


</details>

  <details>
  <summary>Delete Note</summary>

### Endpoints
We expose one endpoint for deleting note

#### 1. Delete Note
   * Path: */note/{noteId}*
   * Http method: *DELETE*
   * PATH parameters: *noteId* - value any valid id
   * Body type: *EMPTY*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess" }
      * failed: *{ "status" : "failed", "error":"Cannot delete note" }*
	
</details>
<details>
  <summary>Get Notes for Entity</summary>

### Endpoints
We expose one endpoint for Notes fetching.

#### 1. Get Notes for entity
   * Path: */note/{page}/{size}*
   * Http method: *POST*
   * PATH parameters: *page* - page number, value *positive number*; *size* - page size, value *positive number* 
   * Body type: *JSON*
   * Body example: *{"entityId":"dhkfd", "entityType":"document", "content":"some note on entity"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"id" : "l93k7df8", "content" :"myNote1", "visibililty" : "private", "ownerId" :"dgferdf",  "createdBy":"me", "createTime" : "2022-06-13 20:00:10}, {"id" : "f93kvc7df8", "content" :"note for entity 2", "visibility" : "public", "ownerId" :"dgfdf", "createdBy" : "somebodyelse", "createTime" : "2022-06-13 20:30:10}]}*
      * failed: *{ "status" : "failed", "error":"unknown"}*
	  
</details>

<details>
  <summary>Get Note by id</summary>

### Endpoints
We expose one endpoint for Note fetching.

#### 1. Get Note
   * Path: */note/{noteId}*
   * Http method: *GET*
   * PATH parameters: *noteId* - value any valid id
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8", "content" :"myNote1", "visibility" : "public", "ownerId" :"dgfdf",  "createdBy" : "me", "createTime" : "2022-06-13 20:00:10"}}*
      * failed: *{ "status" : "failed", "error":"unknown"}*
	  
</details>

### Classes

   <details>
  <summary>Note Class</summary>
  
  * Purpose: keep note info structure and corresponding db methods
  * Fields:
    * id 
	* ownerId
	* content
	* visibility - possible values: *searchable* (space memebers could find document by keywords but content and attachment are not visible), *visible*  (space memebers have full access to document)
	* accessibility - possible values: *public* (anybody could join space), *private* - (only invited user could join space)
    * createdBy - full name of owner
    * createTime
    * updateTime
  * Methods:
    * findById
    * findByEntity
    * update
    * insert
    * delete

    </details>
	

	

