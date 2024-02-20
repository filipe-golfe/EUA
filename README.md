- Documentação para empresas Optantes do Simples Nacional, nessa documentação, destaca-se apenas impostos e valores obrigatórios para emissão de NFCe, caso for necessário emitir NFe, pode ser necessário informar mais impostos.

- Em todos os endpoints, deve-se usar o método POST.

- Em todos os endpoints (exceto o de autorização), deve-se informar o header Authorization-Compufacil com o token de autorização da conta (resetado diariamente)

---

# Autenticação

Endpoint -> http://app.clippfacil.local/rpc/v1/application.authenticate

Esse endpoint é responsável por logar na conta e trazer o access_token, o qual é usado como "Header" nas requisições HTTP do sistema, conforme explicado acima.

JSON de exemplo:
```
{
	"login": "account_email_example@gmail.com",
	"password": "securePasswordExample"
}
```

---

# Cadastro de Produtos

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.post-product

JSON de exemplo:
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

## Discriminação dos campos a serem alterados

### description/barCode/reference/observation
Informar os valores (string)

### price/cost/quantity
Informar os valores (float)

### group
Informar o id do grupo cadastrado na conta. Para buscar a listagem de grupos, deve-se chamar o endpoint https://api.clippfacil.com.br/rpc/v2/inventory.get-group-paginate enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

### PIS/COFINS
Informar os percentuais do PIS/COFINS, valores devem ser de 0 à 1 (sendo 1 = 100%).

### CSTPIS/CSTCOFINS
Informar o ID do CSTPIS ou CSTCOFINS conforme print abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### tributacao/tributacaoNaoContribuinte
Informar o id da tributação cadastrada na conta. Para verificar a lista de tributações, deve-se chamar o endpoint https://api.clippfacil.com.br/rpc/v1/fiscal.get-tributacao enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

### origem
Informar o id da origem conforme tabela abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/ac14a926-7274-4660-bb31-1924bf337944)

### CSOSN/CSOSNNaoContribuinte
Informar o id do CSOSN conforme tabela abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/b7c56576-f74b-465e-8ff1-34c70f602da2)

### NCM
Informar o ID do NCM conforme tabela:
[fiscalncm_202402201112.csv](https://github.com/filipe-golfe/EUA/files/14345583/fiscalncm_202402201112.csv)

- O Restante dos campos manter igual o JSON de exemplo

---

# Atualização de produtos

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.put-product

Enviar mesmo payload do cadastro de produto, informando o ID do mesmo.

---

# Remoção de produtos

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.delete-product

Endpoint responsável pela exclusão de itens, deve-se passar apenas os ids que deseja deletar no payload.

JSON de exemplo:
```
{
	"ids": [
		7606712
	]
}
```

---

# Listagem de produtos

Endpoint -> https://api.clippfacil.com.br/rpc/v2/inventory.get-product-paginate

Traz uma lista paginada de produtos com dados superficiais.

JSON de exemplo:
```
{
	"page": 1,
	"maxResults": 30
}
```

---

# Busca de produto

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.get-product

Traz um único produto localizado pelo ID trazendo dados detalhados do mesmo.

JSON de exemplo:
```
{
	"id": "7606643"
}
```
