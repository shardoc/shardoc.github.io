[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Space Module


<details>
  <summary>Space storing</summary>

### Endpoints
We expose one endpoint for Space storing. Any user could create own space and invite any other user.

#### 1. Create Space
   * Path: */space/create*
   * Http method: *POST*
   * Body type: *JSON*
   * Body example: *{"title":"Lviv group", "note":[{"id":"1", "created for a reason"}], "visibility":"searchable", "accessibility":"public"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8"} }*
      * failed: *{ "status" : "failed", "error":"title should be unque"}*
	  
</details>

<details>
  <summary>Update Space</summary>

### Endpoints

We expose one endpoint for updating field on space

#### 3. Update Field
   * Path: */space/{spaceId}/update*
   * Http method: *POST*
   * PATH parameters: *spaceId* - value any valid id
   * Body type: *JSON*
   * Body example: *{"title":"Updated Title"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess" }
      * failed: *{ "status" : "failed", "error":"Cannot update field [title]" }*

#####	 Comments

* owner cannot extend *visibility*
* owner cannot change *accessibility*

</details>

  <details>
  <summary>Delete Space</summary>

### Endpoints

It's not possible to delete space. Space belongs to all space members
	
</details>
<details>
  <summary>List Spaces</summary>

### Endpoints
We expose one endpoint for Space storing. Any user could create own space and invite any other user.

#### 1. Create Space
   * Path: */space*
   * Http method: *GET*
   
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : [{"id" : "l93k7df8", "title" :"mySpace1"}, {"id" : "f93kvc7df8", "title" :"mySpace2"}]}*
      * failed: *{ "status" : "failed", "error":"unknown"}*
	  
</details>

<details>
  <summary>Get Space be id</summary>

### Endpoints
We expose one endpoint for Space storing. Any user could create own space and invite any other user.

#### 1. Create Space
   * Path: */space/spaceId*
   * Http method: *GET*
   * PATH parameters: *spaceId* - value any valid id
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8", "title" :"mySpace1"}}*
      * failed: *{ "status" : "failed", "error":"unknown"}*
	  
</details>

### Classes

   <details>
  <summary>Space Class</summary>
  
  * Purpose: keep document info structure and corresponding db methods
  * Fields:
    * id 
	* ownerId
	* title
    * notes[] - id values of corresponding note records
	* visibility - possible values: *searchable* (space memebers could find document by keywords but content and attachment are not visible), *visible*  (space memebers have full access to document)
	* accessibility - possible values: *public* (anybody could join space), *private* - (only invited user could join space)
    * createTime
    * updateTime
  * Methods:
    * findById
	* findAll
    * update
    * insert
    * delete

    </details>
	

	
