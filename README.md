# Shared Manufacturing Platform - ChatGPT Agent

## Manufacturing plant offers management

ChatGPT will be utilized in two scenarios:
* the plant receives an offer from the package and need to decide what to do, the options are:
	* accept the offer
	* reject the offer
	* redirect the offer to the pool with an adapted price and its fee
* the plant will periodically check the pool for new offers and will need to decide:
	* accept the offer or not

## ChatGPT request data and format

The request to the ChatGPT tool should include:
* The offer currently processed
This field must include the basic data about the request (id, price and endDate) as well as the type of the offer: whether it was received directly from the packaget or it was taken from the pool.

The data must be formatted as a simple JSON object:
```json
{ "offerId": id,
  "price": int,
  "endDate": timestamp,
  "type": direct / pool
}
```
* Manufacturing plant occupancy
This field must include data about all the packages that are being processed in the plant. Packages are stacked in several docks and each dock should be defined in a separated array. Each array must include JSON objects with data for every package in the dock. The order of the JSON objects correspond to the order of the package in the dock, with the package at the bottom of the dock being the first one in the array and so on.

The data must be formated as a JSON object with one property (storage). The value of the storage property is an array of arrays, where each array represents a dock in the manufacturing plant and contains data about the stored packages.
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

* pool; trenutni in pretekli offerji (acceptani ali da je pretekel rok offerja)
{
	"offersOpen": ["offerId": id,
					"price": int,
					"endDate": timestamp,], 
	"offersClosed": ["offerId": id,
					"price": int,
					"endDate": timestamp,
					"manufacturerId": id]
	]
}

* trenuten balance (v chatgpt se pošlje samo poziv k odločitvi za ponudbe, ki se lahko takoj izvedejo)

