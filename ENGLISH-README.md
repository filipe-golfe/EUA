- For all endpoints, use the POST method. The body must be in JSON format, and you must send the header "imagine-exhibitions-authorization" with the value "hwsYKmkBA1d0fYdojOmVcH9TSmeeHB6V".

---

# Base Urls:

### Base API Urls:

- homolog: https://app.homolog.clippfacil.com.br
- production: https://api.zetaweb.com.br

### Base WEB Urls (for browser access):

- homolog: https://homolog.zetaweb.com.br/#
- production: https://zetaweb.com.br/#

---

# Product Registration

Endpoint -> {{base_api_url}}/rpc/v2/integrations.imagine-exhibitions-register-product

Example JSON:
```
{
	"description": "product description",
	"active": true,
	"quantity": 1.52,
	"price": 0.01,
	"cost": 0,
	"averageCost": 0,
	"unitOfMeasure": {
		"id": 46991
	},
	"group": {
		"id": 1169
	},
	"reference": "reference",
	"barCode": "6973094271349",
	"weight": 0,
	"liquidWeight": 0,
	"observation": "observation",
	"fiscal": {
		"produto": {
			"origem": {
				"id": 9
			},
			"CST": {
				"id": 11
			},
			"CSTNaoContribuinte": {
				"id": 11
			},
			"NCM": {
				"id": 10513
			},
			"tributacao": {
				"id": 27029
			},
			"tributacaoNaoContribuinte": {
				"id": 27029
			},
			"FCP": {
				"id": 27029
			},
			"PIS": 0.0666,
			"CSTPIS": {
				"id": 33
			},
			"COFINS": 0.0666,
			"CSTCOFINS": {
				"id": 33
			},
			"FCI": "999"
		}
	}
}
```

The payload contains only the main fields. If additional specific data needs to be provided, please consult with accounting and inform us.

## Non-Fiscal Fields

### description
(string)
(required)
(maxLength: 255)

### active
(boolean)
(true if not informed)

### quantity
(float)
(zero if not informed)

### price
(float)
(zero if not informed)

### cost
(float)
(zero if not informed)

### averageCost
(float)
(zero if not informed)

### unitOfMeasure
(object)
(defaults to "Unit" if not specified)

Provide the ID of the unit of measure. To retrieve the list of units of measure, call the endpoint {{base_api_url}}/rpc/v2/inventory.get-unit-of-measure-paginate with the following example JSON:

```
{
	"page": 1,
	"maxResults": 30
}
```

To register units of measure in the system, access the URL in your browser: {{base_web_url}}/register/stock/unit-of-measure

### group
(object)
(defaults to null if not specified)

Provide the ID of the group registered in the account. To retrieve the list of groups, call the endpoint {{base_api_url}}/rpc/v2/inventory.get-group-paginate with the following example JSON:

```
{
	"page": 1,
	"maxResults": 30
}
```

To register groups in the system, access the URL in your browser: {{base_web_url}}/register/stock/group

### reference
(string)
(not required)
(maxLength: 30)

### barCode
(string)
(not required)
(maxLength: 18)

### weight
(float)
(not required)

### liquidWeight
(float)
(not required)

### observation
(text)
(not required)

## Fiscal Fields (for tax calculations, consult accounting to understand each parameter and what to provide)

### origem
(object)
(required)

Provide the ID of the origin according to the table below:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/ac14a926-7274-4660-bb31-1924bf337944)

### CST
(object)
(required)

Provide the ID of the CST according to the table below:
![image](https://github.com/user-attachments/assets/2463d84d-1a70-44fe-92dd-623d3fb1c18a)

### CSTNaoContribuinte
(object)
(required)

Provide the ID of the CST according to the table below:
![image](https://github.com/user-attachments/assets/2463d84d-1a70-44fe-92dd-623d3fb1c18a)

### NCM
(object)
(required)

Provide the ID of the NCM according to the table:
[fiscalncm_202402201112.csv](https://github.com/filipe-golfe/EUA/files/14345583/fiscalncm_202402201112.csv)

### tributacao
(object)
(not required)

Provide the ID of the tax registration in the account. To check the list of tax registrations, call the endpoint {{base_api_url}}/rpc/v1/fiscal.get-tributacao with the following example JSON:

```
{
	"page": 1,
	"maxResults": 30
}
```

To register taxes in the system, access the URL in your browser: {{base_web_url}}/#/fiscal/configurations/tributacao

### tributacaoNaoContribuinte
(object)
(not required)

Provide the ID of the tax registration in the account. To check the list of tax registrations, call the endpoint {{base_api_url}}/rpc/v1/fiscal.get-tributacao with the following example JSON:

```
{
	"page": 1,
	"maxResults": 30
}
```

To register taxes in the system, access the URL in your browser: {{base_web_url}}/#/fiscal/configurations/tributacao

### FCP
(object)
(not required)

Provide the ID of the tax registration in the account. To check the list of tax registrations, call the endpoint {{base_api_url}}/rpc/v1/fiscal.get-tributacao with the following example JSON:

```
{
	"page": 1,
	"maxResults": 30
}
```

To register taxes in the system, access the URL in your browser: {{base_web_url}}/#/fiscal/configurations/tributacao

### PIS
(float)
(not required)

Indicates the PIS percentage for the product.

Values should be between 0 and 1 (where 1 = 100%).

### CSTPIS
(object)
(not required)

Provide the ID of the CSTPIS according to the screenshot below:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### COFINS
(float)
(not required)

Indicates the COFINS percentage for the product.

Values should be between 0 and 1 (where 1 = 100%).

### CSTCOFINS
(object)
(not required)

Provide the ID of the CSTCOFINS according to the screenshot below:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### FCI
(string)
(not required)

# Product Update

Endpoint -> {{base_api_url}}/rpc/v2/Integrations.imagine-exhibitions-patch-product

You can update up to 50 products per request.

It uses the same payload as the product registration, the only difference is that in this case, an array is sent and you must specify the product ID you want to update (use the Zetaweb ID).

It is not necessary to send all parameters; you should only send the "id" and the properties you want to update.

Example JSON:
```
[
	{
		"id": 413803,
		"description": "new description 112",
		"active": true,
		"quantity": 15,
		"price": 115,
		"cost": 50,
		"averageCost": 30,
		"unitOfMeasure": {
			"id": 46991
		},
		"group": {
			"id": 1169
		},
		"reference": "reference",
		"barCode": "6973094271349",
		"weight": 1,
		"liquidWeight": 2,
		"observation": "observation",
		"fiscal": {
			"produto": {
				"origem": {
					"id": 2
				},
				"CST": {
					"id": 1
				},
				"CSTNaoContribuinte": {
					"id": 2
				},
				"NCM": {
					"id": 10513
				},
				"tributacao": {
					"id": 27033
				},
				"tributacaoNaoContribuinte": {
					"id": 27033
				},
				"FCP": {
					"id": 27033
				},
				"IPI": 0.05,
				"CSTIPI": {
					"id": 10
				},
				"CENQ": {
					"id": 1
				},
				"PIS": 0.04,
				"CSTPIS": {
					"id": 33
				},
				"COFINS": 0.04,
				"CSTCOFINS": {
					"id": 33
				},
				"FCI": "a"
			}
		}
	}
]
```

---

# Product Removal

Endpoint -> {{base_api_url}}/rpc/v1/inventory.delete-product

Only the IDs of the products you want to delete should be passed in the payload.

Use zetaweb product ID.

Example JSON:
```
{
	"ids": [
		7606712
	]
}
```

---

# Product Listing

Endpoint -> {{base_api_url}}/rpc/v2/inventory.get-product-paginate

Returns a paginated list of products with basic data.

Example JSON:
```
{
	"page": 1,
	"maxResults": 30
}
```

---

# Product Search

Endpoint -> {{base_api_url}}/rpc/v1/inventory.get-product

Returns a single product located by ID with detailed information.

Use zetaweb product ID.

Example JSON:
```
{
	"id": "7606643"
}
```
