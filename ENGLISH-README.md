- Documentation for companies opting for Simple National (Optante do Simples Nacional), in this documentation, only required taxes and values for the transmission of NFCe are highlighted. If it is necessary to transmit NFe, more taxes may need to be informed.

- In all endpoints, the POST method must be used.

- In all endpoints (except the authorization one), the "Authorization-Compufacil" header must be provided with the account's authorization token (reset daily).

---

# Authentication

Endpoint -> http://app.clippfacil.local/rpc/v1/application.authenticate

This endpoint is responsible for logging into the account and retrieving the access_token, which is used as a "Header" in the system's HTTP requests, as explained above.

Example JSON:
```
{
	"login": "account_email_example@gmail.com",
	"password": "securePasswordExample"
}
```

---

# Product register

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.post-product

Example JSON:
```
{
	"colorCollection": [],
	"sizeCollection": [],
	"id": null,
	"sequence": null,
	"uuid": null,
	"description": "produto eua final 1",
	"hasZhubIntegration": false,
	"price": 100,
	"cost": 55,
	"averageCost": 0,
	"barCode": "",
	"quantity": 10,
	"reserved": 0,
	"active": true,
	"favorite": false,
	"reference": "referencia",
	"image": null,
	"observation": "obs",
	"originPersistence": null,
	"importationCode": null,
	"lastSellDate": null,
	"lastSupplierName": null,
	"purchaseNfeNumber": null,
	"weight": null,
	"liquidWeight": null,
	"minimumQuantity": null,
	"canCalculateCommission": false,
	"hasVariations": false,
	"commissionInCash": 0,
	"commissionInstallment": 0,
	"commissionCard": 0,
	"variationCollection": [],
	"productType": {
		"id": 0,
		"name": "Mercadoria para revenda"
	},
	"profitPercent": null,
	"created": null,
	"deleted": null,
	"hasMovimentation": false,
	"fiscal": {
		"produto": {
			"productUuid": null,
			"excecaoFiscal": null,
			"FCI": null,
			"PIS": 0.05,
			"COFINS": 0.05,
			"vBCSTRet": null,
			"vICMSSTRet": null,
			"vBCST": null,
			"vICMSST": null,
			"isICMSSTRet": null,
			"pGLP": null,
			"pImportedGas": null,
			"pNationalGas": null,
			"GLPStartValue": null,
			"GLPTributeQuantity": null,
			"adRemICMS": null,
			"pBio": null,
			"pOrig": null,
			"id": null,
			"deleted": null,
			"CST": null,
			"CSTNaoContribuinte": null,
			"CSTPIS": {
				"id": 33
			},
			"tributacao": {
				"id": 405439
			},
			"tributacaoNaoContribuinte": {
				"id": 405439
			},
			"CSTCOFINS": {
				"id": 33
			},
			"origem": {
				"id": 1
			},
			"CSOSN": {
				"id": 2
			},
			"CSOSNNaoContribuinte": {
				"id": 2
			},
			"CFOPNFE": null,
			"CFOPNFCE": null,
			"NCM": {
				"id": 10513
			},
			"FCP": null,
			"IAT": "T",
			"IPPT": "T"
		}
	},
	"type": {},
	"group": 97962,
	"totalPrice": null,
	"quantityPurchased": null,
	"unitOfMeasureTribut": null
}
```

## Detailing of the fields to be changed

### description/barCode/reference/observation
Inform the values (string)

### price/cost/quantity
Inform the values (float)

### group
Provide the ID of the group registered in the account. To search for the group listing, the endpoint https://api.clippfacil.com.br/rpc/v2/inventory.get-group-paginate should be called by sending the example JSON below:

```
{
	"page": 1,
	"maxResults": 30
}
```

### PIS/COFINS
Inform the PIS/COFINS percentages, values must be from 0 to 1 (where 1 = 100%).

### CSTPIS/CSTCOFINS
Provide the ID for CSTPIS or CSTCOFINS as shown in the print below:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### tributacao/tributacaoNaoContribuinte
Provide the ID of the taxation registered in the account. To check the list of taxations, the endpoint https://api.clippfacil.com.br/rpc/v1/fiscal.get-tributacao should be called by sending the example JSON below:

```
{
	"page": 1,
	"maxResults": 30
}
```

### origem
Provide the ID of the origin as shown in the table below:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/ac14a926-7274-4660-bb31-1924bf337944)

### CSOSN/CSOSNNaoContribuinte
Provide the ID of the CSOSN as shown in the table below:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/b7c56576-f74b-465e-8ff1-34c70f602da2)

### NCM
Provide the ID of the NCM as shown in the table:
[fiscalncm_202402201112.csv](https://github.com/filipe-golfe/EUA/files/14345583/fiscalncm_202402201112.csv)

- Keep the rest of the fields the same as the example JSON

---

# Product update

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.put-product

Send the same payload as the product registration, providing its ID.

---

# Product delete

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.delete-product

Endpoint responsible for the deletion of items. Only the IDs that are intended to be deleted should be passed in the payload.

Example JSON:
```
{
	"ids": [
		7606712
	]
}
```

---

# Product list

Endpoint -> https://api.clippfacil.com.br/rpc/v2/inventory.get-product-paginate

Brings a paginated list of products with superficial data.

Example JSON:
```
{
	"page": 1,
	"maxResults": 30
}
```

---

# Product Get

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.get-product

Retrieves a single product identified by its ID, providing detailed data about it.

Example JSON:
```
{
	"id": "7606643"
}
```
