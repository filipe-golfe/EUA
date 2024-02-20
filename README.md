- Documentação para empresas Optantes do Simples Nacional.

- Em todos os endpoints citados, deve-se usar o método POST.

- Em todos os endpoints, deve-se informar o header Authorization-Compufacil com o token de autorização da conta (resetado diariamente)

---

# Cadastro de Produtos

Endpoint -> https://api.clippfacil.com.br/rpc/v1/inventory.post-product

JSON de exemplo:
```
```

## Discriminação dos campos a serem alterados

### description/barCode/reference/observation
Informar os valores (string)

### price/cost/quantity
Informar os valores (float)

### PIS/COFINS
Informar os percentuais do PIS/COFINS, valores devem ser de 0 à 1 (sendo 1 = 100%).

### CSTPIS/CSTCOFINS
Informar o ID do CSTPIS ou CSTCOFINS conforme print abaixo:
![image](https://github.com/filipe-golfe/EUA/assets/69996639/e4af3d7c-28cc-4e30-8f6b-3cfd145968a1)

### tributacao/tributacaoNaoContribuinte
Informar o id da tributação cadastrada na conta. Para verificar a lista de tributações da conta, deve-se chamar o endpoint https://api.clippfacil.com.br/rpc/v1/fiscal.get-tributacao enviando o JSON de exemplo abaixo:

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

---
