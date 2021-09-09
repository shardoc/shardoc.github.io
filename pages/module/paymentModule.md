[<- to **content**](https://github.com/shardoc/shardoc.github.io)
> [<- to **specification**](https://github.com/shardoc/shardoc.github.io/blob/dev/pages/specification.md)
## Payment Module


<details>
  <summary>Payment</summary>

### Endpoints
We expose one endpoint for payment on price shared data.

#### 1. Payment
   * Path: */payment*
   * Http method: *POST*
   * PATH parameters: *shareId* - id of share data 
   * Body type: *JSON*
   * Body example: *{"shareId":"s67s"}*
   * Response type: JSON
   * Response example: 
      * success: *{ "status" : "success", "body" : {"id" : "l93k7df8"} }*
      * failed: *{ "status" : "failed", "error":"incorrect shareId value"}*
	  
</details>

### Classes

  <summary>Payment Class</summary>
  
  * Purpose: keep information about payment on share data payment request
  * Fields:
    * id 
	* ownerId
	* shareId
    * price 
	  * amount" 
	  * currency
	* status - possible values: *pending*, *failed*, *paid*
    * createTime
    * updateTime
  * Methods:
    * findById
	* findAll
    * update
    * insert
    * delete

    </details>
	

	

