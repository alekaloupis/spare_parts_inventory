# Spare Parts Inventory

dataset: https://www.kaggle.com/datasets/mohdkhidir/medical-equipment-spare-parts-inventories-datasets?resource=download

# 1. Questão de negócio 

Nos últimos meses, houveram algumas interrupções na assistência aos pacientes devido à danificação de partes ou equipamentos médicos da instituição.
Além disso, foi mapeado que esses transtornos estavam relacionadas às peças one-off, consideradas peças únicas ou raras, que para serem fabricadas exigem processos mais específicos.

A gestão hospitalar necessita mapear se a instituição está em uma condição de vulnerabilidade em relação a essas peças one-off caracterizada pelas dificuldades de acesso, baixo estoque ou alto custo de aquisição
das mesmas.

Então, com o objetivo de mapear a condição das peças dessa categoria disponíveis no inventário, a gestão hospitalar solicitou uma análise exploratória a partir do inventário.

# 2. Hipóteses 

a) As peças one-off são mais caras na média que as peças das demais categorias

b) Há uma menor quantiddade de peças one-off no inventário do que peças das demais categorias

c) As peças one-off são mais difíceis de serem obtidas do que as peças das demais categorias. 

# 3. Solução

### 3.1 Carga e tratamento dos dados

Essa análise exploratória será feita utilizando Excel e Power Query, ferramentas cuja versatilidade e intuitividade favorecem a obtenção de rápidas respostas. 

### Passo 1: Abrir um Excel vazio e carregar os dados a partir das sinalizações das imagens abaixo (Figuras 1 e 2):

##### Figura1: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/907a84d7-24b0-4001-94cb-986e0b13e5b9)

##### Figura2:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/a4157979-76f4-45e8-9592-3a161586f1cb)


Ao carregar os dados, iremos ser direcionados para o editor do Power Query

### Passo 2: Entender cada coluna do dataset disponível

•	Item Code: código da categoria da peça

•	Item Description: descrição da categoria da peça

•	Part No.: número do código da peça

•	Part Description: descrição da peça

•	Model: modelo da peça

•	Unit Of Measurement: unidade de medida da peça

•	Spare Part Type: tipo da peça sobressalente

      Fast Moving Item – item de rápida movimentação
      Just in Time – Ajustado ao tempo
      One Off – Peça rara/única
	
•	Location: locação

      Company Site Office – escritório local da empresa
      Centralized – Centralizada 
      Others - Outros
      
•	Specify: especificação da peça / forma pela qual a peça é adquirida

      Vendor by Purchase Order – fornecedor por ordem de compra
      Not Specified – Não especificado
      
•	Part Category: categoria da peça

•	Is Expiry date Required: não foi possível obter uma correta identificação do significado dessa coluna. E, também, na especificação do dataset no Kaggle, não há qualquer informação a respeito. Em um cenário de mercado, provavelmente o analista perguntaria para alguém da área responsável pelos dados para esclarecer esta dúvida.

•	Min Nos: mínimo de peças no inventário 

•	Max Nos: máximo de peças no inventário

•	Minimum Price Per Nos (RM): preço mínimo por peça 

•	Maximum Price Per Nos (RM): preço máximo por peça

•	Brand: marca da peça

•	Status: status da peça

•	Expiry Age (In Month): data de validade da peça

•	Current Stock Level: nível do estoque atual

### Passo 3: Remover colunas desnecessárias

Nessa análise iremos optar por excluir as seguintes colunas

•	Unit of measurement: temos apenas uma informação neste dataset. Todas as colunas estão preenchidas com o dado “unit”, o quê significa que todas as peças estão em formato de unidade. Uma vez que o analista já compreendeu este dado, já podemos excluí-lo.

•	Part category:  temos apenas uma informação neste dataset. Todas as colunas estão preenchidas com o dado “biomedical”, o quê significa que todas as peças são do tipo biomédico. Vamos utilizar o mesmo raciocínio utilizado no item anterior, a saber uma vez que já compreendemos esta informação, já podemos excluir esta coluna.


•	Status: temos apenas uma informação neste dataset. Todas as colunas estão preenchidas com o dado “active”, a saber todas as peças do inventário estão ativas. Então, já podemos excluir essa coluna.

•	Is Expiry Data Required: não foi possível identificar o conteúdo dessa coluna. Portanto, iremos optar pela exclusão.

Para excluir, podemos utilizar a opção apresentada na figura abaixo (Figura 3): 

##### Figura3:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/4879a402-945a-408d-b77d-fb64d65ac4d8)



























