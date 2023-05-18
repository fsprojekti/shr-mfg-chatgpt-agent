# Shared Manufacturing Platform - ChatGPT Agent

## Manufacturing plant offers management

ChatGPT will be utilized in two scenarios:
* the plant receives an offer from the package and need to decide what to do, the options are:
 * accept the offer
 * reject the offer
 * redirect the offer to the pool with an adapted price and its fee
* the plant will periodically check the pool for new offers and will need to decide:
	* accept the offer or not

	
request na ChatGPT:
* trenuten offer: ali direkten ali iz pool-a (glede na zgornja 2 eventa)

{ "offerId": id,
  "price": int,
  "endDate": timestamp,
  "type": direct / pool
}

* zasedenost tovarne; trenutno stanje paketov, čas zaključka obdelave, čas dispatcha (od konca obdelave do nalaganja na prevoz)

{
	"storage": [[{"packageId": id,
				  "processingEndDate": timestamp,
				  "dispatchDuration": int (seconds)
				}, ...
				], ...
			   ]
}

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

