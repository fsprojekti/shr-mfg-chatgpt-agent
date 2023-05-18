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
{ "offerId": id,
  "price": int,
  "endDate": timestamp,
  "type": string ("direct" or "pool")
}
```
* **Manufacturing plant occupancy**

This field should include data about all the packages being processed in the plant. Packages are stacked in several docks, and each dock should be defined in a separate array. Each array must include JSON objects with data for every package in the dock. The order of the JSON objects corresponds to the order of the packages in the dock, with the package at the bottom of the dock being the first one in the array, and so on.

The data should be formatted as a JSON object with one key (storage). The value of the storage key is an array of arrays, where each array represents a dock in the manufacturing plant and contains data about the stored packages.
```json
{"storage": [
		[
			{"packageId": id1,
	  		"processingEndDate": timestamp1,
	  		"dispatchDuration": int (seconds1)
			}, 
			{"packageId": id2,
	  		"processingEndDate": timestamp2,
	  		"dispatchDuration": int (seconds2)
			},
			...
		], 
		[
			{"packageId": id3,
	  		"processingEndDate": timestamp3,
	  		"dispatchDuration": int (seconds3)
			}, 
			{"packageId": id4,
	  		"processingEndDate": timestamp4,
	  		"dispatchDuration": int (seconds4)
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
{"offersOpen": ["offerId": id,
		"price": int,
		"endDate": timestamp,], 
"offersClosed": ["offerId": id,
		"price": int,
		"endDate": timestamp,
		"manufacturerId": id]]
}
```

* **Current balance**

This field should include the current state of the manufacturer's balance. **Note that ChatGPT should only be asked to assist with the decision regarding offers that can realistically be fulfilled**.
```json
{"balance": int
}
```

