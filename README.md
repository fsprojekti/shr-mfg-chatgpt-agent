# shr-mfg-chatgpt-agent


manufacturing:

* dobi offer od paketa (sendOffer)
	odločitev: accept, reject, to pool? --> ChatGPT
* preverjanje pool-a za nove ponudbe
	odločitev: accept? ChatGPT
	
	
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

