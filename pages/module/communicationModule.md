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
   * Body example: *{"recipientId":"ds678s79s", "message":"Hello, it's me"}*
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
   * Path: */message/{messageId}*
   * Http method: *DELETE*
   * PATH parameters: *messageId* - value any valid message id
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
   * Path: */message/{recipientId}*
   * Http method: *GET*
   * PATH parameters: *recipientId* - value any valid message recipient id
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "sucess", "body" : [{"recipientId":"ds678s79s","senderId":"dfr45tr", "message":"Hello, it's me"},{"recipientId":"ds678s79s", "senderId" : "sfsf98dfld9", "message":"How are you"}] }
      * failed: *{ "status" : "failed", "error":"Cannot update message" }*

</details>


### Classes

   <details>
  <summary>Message Class</summary>
  
  * Purpose: describe messages sent by user
  * Fields:
    * id 
	* ownerId
	* recipientId
    * message - max 160 characters
	* status - possible values: *sent*, *failed*, *read*
    * createTime
    * updateTime
  * Methods:
    * findById
	* findAll
    * update
    * insert
    * delete

    </details>
	

	

