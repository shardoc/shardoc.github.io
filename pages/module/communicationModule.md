[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Communication Module


<details>
  <summary>Send message</summary>

### Endpoints
We expose one endpoint for a sending message. 

#### 1. Send message
   * Path: */message*
   * Http method: *POST*
   * Body type: *JSON*
   * Body example: *{"recipient_id":"ds678s79s", "message":"Hello, it's me"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success" }*
      * failed: *{ "status" : "failed", "error":"cannot send message"}*
	  
</details>

  <details>
  <summary>Delete message</summary>

### Endpoints

We expose one endpoint for deleting message

#### 3. Delete message
   * Path: */message/{message_id}*
   * Http method: *DELETE*
   * PATH parameters: *message_id* - value any valid message id
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess" }
      * failed: *{ "status" : "failed", "error":"Cannot update message" }*
</details>
<details>
  <summary>History</summary>

### Endpoints
We expose one endpoint for a communication history.

#### 3. Get Conversation
   * Path: */message/{recipient_id}?last_id={value}&size={value}*
   * Http method: *GET*
   * PATH parameters: *recipient_id* - value any valid message recipient id
   * Query parameters: *last_id* and *size* paging parameters
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess", "body" : [{"recipient_id":"ds678s79s","owner_id":"dfr45tr", "message":"Hello, it's me"},{"recipient_id":"ds678s79s", "owner_id" : "sfsf98dfld9", "message":"How are you"}] }
      * failed: *{ "status" : "failed", "error":"Cannot update message" }*

</details>


### Classes

   <details>
  <summary>Message Class</summary>
  
  * Purpose: describe messages sent by user
  * Fields:
    * id 
	* owner_id
	* recipient_id
    * message - max 160 characters
	* status - possible values: *sent*, *failed*, *read*
    * createTime
    * updateTime
    </details>
	

	

