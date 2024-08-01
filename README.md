- Em todos os endpoints, deve-se usar o método POST.

- Em todos os endpoints (exceto o de login), deve-se informar o header Authorization-Compufacil com o token da conta (resetado diariamente)

---

# Base Urls:

### Base API Urls:

- homolog: https://app.homolog.clippfacil.com.br
- produção: https://api.zetaweb.com.br

### Base WEB Urls (para acessar no browser):

- homolog: https://homolog.zetaweb.com.br/#
- produção: https://zetaweb.com.br/#

---

# Autenticação

Endpoint -> {{base_api_url}}/rpc/v1/application.authenticate

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

Endpoint -> {{base_api_url}}/rpc/v1/inventory.post-product

JSON de exemplo:
```
{
	"colorCollection": [],
	"sizeCollection": [],
	"price": 100,
	"active": true,
	"cost": 80,
	"averageCost": 80,
	"quantity": 10,
	"reserved": 0,
	"variationCollection": [],
	"productType": {
		"id": 0,
		"name": "Mercadoria para revenda"
	},
	"fiscal": {
		"produto": {
			"origem": {
				"id": 1
			},
			"CST": {
				"id": 2
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
			"PIS": 0.02,
			"CSTPIS": {
				"id": 33
			},
			"COFINS": 0.02,
			"CSTCOFINS": {
				"id": 33
			},
			"IAT": "T",
			"IPPT": "T"
		}
	},
	"type": {},
	"unitOfMeasure": {
		"id": 40168
	},
	"description": "product description 2",
	"group": 1169,
	"reference": "product reference",
	"observation": "product observation",
	"barCode": "7898307491309",
	"commissionInCash": 0,
	"commissionInstallment": 0,
	"commissionCard": 0
}
```

## Discriminação dos campos a serem alterados

### description/reference/observation
(string)

### barcode
(string/null)

### price/cost/averageCost/quantity
(float)

### group
(integer)

Informar o ID do grupo cadastrado na conta. Para buscar a listagem de grupos, deve-se chamar o endpoint {{base_api_url}}/rpc/v2/inventory.get-group-paginate enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

Caso não desejar informar um grupo, remover o parâmetro do payload.

Para cadastrar grupos no sistema, acessar a URL no browser: {{base_web_url}}/register/stock/group

### PIS/COFINS
(float)
Valores devem ser de 0 à 1 (sendo 1 = 100%).

### CSTPIS/CSTCOFINS
(object)

Informar o ID do CSTPIS ou CSTCOFINS conforme print abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### tributacao/tributacaoNaoContribuinte
(object)

Informar o ID da tributação cadastrada na conta. Para verificar a lista de tributações, deve-se chamar o endpoint {{base_api_url}}/rpc/v1/fiscal.get-tributacao enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

Caso não desejar informar uma tributação, remover o parâmetro do payload.

Para cadastrar tributações no sistema, acessar a URL no browser: {{base_web_url}}/#/fiscal/configurations/tributacao

### origem
(object)

Informar o ID da origem conforme tabela abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/ac14a926-7274-4660-bb31-1924bf337944)

### CST/CSTNaoContribuinte
(object)

Informar o ID do CST conforme tabela abaixo:
![image](https://github.com/user-attachments/assets/2463d84d-1a70-44fe-92dd-623d3fb1c18a)

### NCM
(object)

Informar o ID do NCM conforme tabela:
[fiscalncm_202402201112.csv](https://github.com/filipe-golfe/EUA/files/14345583/fiscalncm_202402201112.csv)

- O Restante dos campos pode manter igual o JSON de exemplo

---

# Atualização de produtos 1

Endpoint -> {{base_api_url}}/rpc/v1/inventory.put-product

Enviar mesmo payload do cadastro de produto, informando o ID do mesmo. (precisa informar todos os parâmetros).

---

# Atualização de produtos 2

Endpoint -> {{base_api_url}}/

JSON de exemplo:
```
{
	
}
```

---

# Remoção de produtos

Endpoint -> {{base_api_url}}/rpc/v1/inventory.delete-product

Deve-se passar apenas os ids que deseja deletar no payload.

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

Endpoint -> {{base_api_url}}/rpc/v2/inventory.get-product-paginate

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

Endpoint -> {{base_api_url}}/rpc/v1/inventory.get-product

Traz um único produto localizado pelo ID trazendo dados detalhados do mesmo.

JSON de exemplo:
```
{
	"id": "7606643"
}
```
