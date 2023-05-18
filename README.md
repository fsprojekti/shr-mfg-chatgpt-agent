# Shared Manufacturing Platform - ChatGPT Agent

## Manufacturing plant offers management

ChatGPT will be utilized in two scenarios:
* The plant receives an offer from the package and needs to decide what to do. The options are:
	* Accept the offer.
	* Reject the offer.
	* Redirect the offer to the pool with an adjusted price and fee.
* The plant periodically checks the pool for new offers and needs to make a decision:
	* Accept or reject the offer.

## ChatGPT request data and format

The request to the ChatGPT tool should include the following: 
* **The offer currently being processed**

This field should include the basic data about the request (ID, price, and end date), as well as the type of the offer: whether it was received directly from the package or taken from the pool.

The data should be formatted as a simple JSON object:
```json
{ 
	"offerId": id,
  	"price": 10,
  	"endDate": 1684407772,
  	"type": "direct or pool"
}
```
* **Manufacturing plant occupancy**

This field should include data about all the packages being processed in the plant. Packages are stacked in several docks, and each dock should be defined in a separate array. Each array must include JSON objects with data for every package in the dock. The order of the JSON objects corresponds to the order of the packages in the dock, with the package at the bottom of the dock being the first one in the array, and so on.

The data should be formatted as a JSON object with one key (storage). The value of the storage key is an array of arrays, where each array represents a dock in the manufacturing plant and contains data about the stored packages.
```json
{"storage": [
		[
			{
				"packageId": 111,
				"processingEndDate": 1684407772,
				"dispatchDuration": 30
			}, 
			{
				"packageId": 222,
				"processingEndDate": 1684407772,
				"dispatchDuration": 30
			},
			...
		], 
		[
			{
				"packageId": 333,
				"processingEndDate": 1684407772,
				"dispatchDuration": 30
			}, 
			{
				"packageId": 444,
				"processingEndDate": 1684407772,
				"dispatchDuration": 30
			},
			...
		], ...
   	]
}
```

* **Content of the pool**

This field should include the data about all the offers currently in the pool and those that were previously in the pool but are no longer open (either accepted or expired).

The data should be formatted as a JSON object with separate fields for open and closed offers:

```json
{
"offersOpen": [
			{	
				"offerId": 1,
				"price": 5,
				"endDate": 1684407772
			},
			...
		], 
"offersClosed": [
			{
				"offerId": 2,
				"price": 3,
				"endDate": 16844075272,
				"manufacturerId": 151353
			}
			...
		]
}
```

* **Current balance**

This field should include the current state of the manufacturer's balance. **Note that ChatGPT should only be asked to assist with the decision regarding offers that can realistically be fulfilled**.
```json
{
"balance": 100
}
```

