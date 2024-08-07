- Em todos os endpoints, usar o método POST, o body deve ser em formato JSON e deve-se enviar o header "imagine-exhibitions-authorization" com o valor "hwsYKmkBA1d0fYdojOmVcH9TSmeeHB6V".

---

# Base Urls:

### Base API Urls:

- homolog: https://app.homolog.clippfacil.com.br
- produção: https://api.zetaweb.com.br

### Base WEB Urls (para acessar no browser):

- homolog: https://homolog.zetaweb.com.br/#
- produção: https://zetaweb.com.br/#

---

# Cadastro de Produtos

Endpoint -> {{base_api_url}}/rpc/v2/integrations.imagine-exhibitions-register-product

JSON de exemplo:
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

Payload possui apenas os principais campos, caso for necessário informar outros dados específicos, favor consultar contabilidade e nos informar.

## Campos não fiscais

### description
(string)
(required)
(maxLength: 255)

### active
(boolean)
(true se não informado)

### quantity
(float)
(zero se não informado)

### price
(float)
(zero se não informado)

### cost
(float)
(zero se não informado)

### averageCost
(float)
(zero se não informado)

### unitOfMeasure
(object)
(irá setar a unidade de medida padrão "Unidade" caso não informado) 

Informar o ID da unidade de medida. Para buscar a listagem de unidades de medida, deve-se chamar o endpoint {{base_api_url}}/rpc/v2/inventory.get-unit-of-measure-paginate enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

Para cadastrar unidades de medida no sistema, acessar a URL no browser: {{base_web_url}}/register/stock/unit-of-measure

### group
(object)
(irá setar null caso não informado)

Informar o ID do grupo cadastrado na conta. Para buscar a listagem de grupos, deve-se chamar o endpoint {{base_api_url}}/rpc/v2/inventory.get-group-paginate enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

Para cadastrar grupos no sistema, acessar a URL no browser: {{base_web_url}}/register/stock/group

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

## Campos fiscais (para cálculo de impostos, consultar contabilidade para saber o que é cada parâmetro e o que informar)

### origem
(object)
(required)

Informar o ID da origem conforme tabela abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/ac14a926-7274-4660-bb31-1924bf337944)

### CST
(object)
(required)

Informar o ID do CST conforme tabela abaixo:
![image](https://github.com/user-attachments/assets/2463d84d-1a70-44fe-92dd-623d3fb1c18a)

### CSTNaoContribuinte
(object)
(required)

Informar o ID do CST conforme tabela abaixo:
![image](https://github.com/user-attachments/assets/2463d84d-1a70-44fe-92dd-623d3fb1c18a)

### NCM
(object)
(required)

Informar o ID do NCM conforme tabela:
[fiscalncm_202402201112.csv](https://github.com/filipe-golfe/EUA/files/14345583/fiscalncm_202402201112.csv)

### tributacao
(object)
(not required)

Informar o ID da tributação cadastrada na conta. Para verificar a lista de tributações, deve-se chamar o endpoint {{base_api_url}}/rpc/v1/fiscal.get-tributacao enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

Para cadastrar tributações no sistema, acessar a URL no browser: {{base_web_url}}/#/fiscal/configurations/tributacao

### tributacaoNaoContribuinte
(object)
(not required)

Informar o ID da tributação cadastrada na conta. Para verificar a lista de tributações, deve-se chamar o endpoint {{base_api_url}}/rpc/v1/fiscal.get-tributacao enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

Para cadastrar tributações no sistema, acessar a URL no browser: {{base_web_url}}/#/fiscal/configurations/tributacao

### FCP
(object)
(not required)

Informar o ID da tributação cadastrada na conta. Para verificar a lista de tributações, deve-se chamar o endpoint {{base_api_url}}/rpc/v1/fiscal.get-tributacao enviando o JSON de exemplo abaixo:

```
{
	"page": 1,
	"maxResults": 30
}
```

Para cadastrar tributações no sistema, acessar a URL no browser: {{base_web_url}}/#/fiscal/configurations/tributacao

### PIS
(float)
(not required)

Indica o percentual de PIS do produto.

Valores devem ser de 0 à 1 (sendo 1 = 100%).

### CSTPIS
(object)
(not required)

Informar o ID do CSTPIS conforme print abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### COFINS
(float)
(not required)

Indica o percentual de COFINS do produto.

Valores devem ser de 0 à 1 (sendo 1 = 100%).

### CSTCOFINS
(object)
(not required)

Informar o ID do CSTCOFINS conforme print abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### FCI
(string)
(not required)

---

# Atualização de produtos

Endpoint -> {{base_api_url}}/rpc/v2/Integrations.patch-product

É possível atualizar até 50 produtos por request.

Utiliza o mesmo payload do cadastro de produtos, a única diferença é que nesse é enviado um array e deve-se informar o id do produto que quer atualizar (usar o id do zetaweb).

Não é necessário enviar todos os parâmetros, deve-se enviar apenas o "id" e as propriedades que deseja atualizar.

JSON de exemplo:
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
