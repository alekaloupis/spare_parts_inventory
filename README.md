# Spare Parts Inventory

dataset: https://www.kaggle.com/datasets/mohdkhidir/medical-equipment-spare-parts-inventories-datasets?resource=download



# 1. Questão de negócio 

Dentro de uma institução hospitalar, nos últimos meses, houveram algumas interrupções na assistência aos pacientes devido à danificação de peças de equipamentos médicos.
Além disso, foi mapeado que esses transtornos estavam relacionadas à danificação de peças one-off, consideradas raras e com processo de fabricação específico. 

Sendo que a danificação das peças em uso e a não imediata reposição das mesmas impactaram na retomada do atendimento. A gestão considera de valor estratégico manter formas saudáveis de obtenção, garantir estoque para evitar novos transtornos e interrupções na rotina. E para isso, deseja discutir ações específicas em relação a essas peças e conta com o auxílio do analista de dados da empresa, profissional capaz de levantar dados e realizar análises. Atualmente, existe um inventário das peças sobressaletes, a saber peças disponíveis para reposição das peças em uso. E a partir desse inventário, a gestao hospitalar solicitou uma análise para averigurar a existência de indícios que constatem ou não uma situação de vulnerabilidade do hospital em relação a essas peças one-off. Dentre esses indícios, poderíamos citar: ausência de quantidade mínima, dificuldades de acesso, formas de aquisição, custos de aquisição.

Além disso, foi demandado a listagem das peças alvo em situação de vulnerabilidade. Por fim, foi solicitado que da análise, o analista apresente seus principais achados em uma reunião e elabore uma apresentação em Power Point.


# 2. Solução

## 2.1 Carga e tratamento dos dados

Essa análise exploratória será feita utilizando Excel e Power Query, ferramentas cuja versatilidade e intuitividade favorecem a obtenção de rápidas respostas. 

### Passo 1: Abrir um Excel vazio e carregar os dados a partir das sinalizações das imagens abaixo (Figuras 1 e 2):

##### Figura1: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/907a84d7-24b0-4001-94cb-986e0b13e5b9)

##### Figura2:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/a4157979-76f4-45e8-9592-3a161586f1cb)


Ao carregar os dados, iremos ser direcionados para o editor do Power Query

### Passo 2: Entender cada coluna do dataset disponível

•	Item Code: código da categoria da peça. Aqui temos 28 diferentes valores de Item Code que estão relacionadas a 28 descrições de item diferentes, que é justamente a coluna em seguida

•	Item Description: descrição da categoria da peça

•	Part No.: número do código da peça

•	Part Description: descrição da peça

•	Model: modelo da peça

•	Unit Of Measurement: unidade de medida da peça

•	Spare Part Type: tipo da peça sobressalente (Essa coluna envolve a categoria chave da nossa análise exploratória)

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

E repetimos para as demais colunas que sinalizamos que precisam ser excluídas.

### Passo 4: Identificar o tipo de dado de cada coluna 

•	Item Code: texto

•	Item Description: texto

•	Part No.: texto

•	Part Description: texto

•	Model: texto

•	Spare Part Type: texto

•	Location: texto

•	Specify: texto

•	Part Category: texto

•	Min Nos: número inteiro

•	Max Nos: número inteiro

•	Minimum Price Per Nos (RM): número decimal

•	Maximum Price Per Nos (RM): número decimal

•	Brand: texto

•	Status: texto

•	Expiry Age (In Month): número inteiro 

•	Current Stock Level: número inteiro

### Passo 5: Tratamento, substituição e transformação de dados/colunas

Ainda no editor do Power Query, na guia da Página Inicial, temos a opção Substituir valores (Figura 4). Na janela de edição, temos a opção de Valor a Ser Localizado e Substituir por (Figura 5).

### Figura 4: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/2ba93139-50ef-41f4-8185-3f3f5f29b330)

### Figura 5: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/44948d8a-57cd-43dc-aad7-8066dbfa3e85)

Então, na coluna Specify, vamos alterar o valor de null para not specified. Além disso, nessa mesma coluna, identificamos que temos dois valores quase iguais, a saber "Vendor – By Purchase Order" e "Vendor By Purchase Order". Obtemos essa informação, ao clicar com o botão esquerdo nessa coluna (Figura 6). Então, iremos optar por substituir esses valores e unificar tudo na categoria de Vendor By Purchase Order.

### Figura 6: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/7266a221-53b7-4e33-a87c-e41a32a7600f)


Uma das nossas hipóteses levantadas sugere que investiguemos a capacidade de estoque das peças sobressalentes. Ora, se o valor da coluna
"Current Stock Level" for menor que o mínimo valor em estoque, dado pela coluna "Min Nos", então podemos concluir que não temos o mínimo de peças em estoque. 

Sendo assim, vamos criar essa coluna calculada em nosso dataset "Current Stock Level Has Min?" - valores: Same/Yes/No. 


Podemos criar essa coluna, selecionando a opção Coluna Personalizada da aba Adicionar coluna do nosso editor do Power Query (Figura 7). Em seguida, será habilitada a janela para criarmos a coluna utilizando linguagem M (Figura 8). 

Neste caso, vamos utilizar uma lógica de if/else, comparando as colunas Currrent Stock Level e Min Nos. Após criar a lógica, clicamos em “ok” para criar a coluna.

### Figura 7: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/b88c3296-de4d-4857-86a7-b3088e1477bc)


### Figura 8: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/bb9b6d8b-4c2e-4d83-98ef-7d521ab3388a)

Terminadas os tratamentos, podemos finalmente clicar na opção Fechar e carregar conforme sinaliza a imagem abaixo:

### Figura 9:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/0a50b642-f606-461f-944f-6cde6cf5ec91)

Ao Fechar a Carregar, abrimos uma aba da Planilha e podemos remomeá-la para dataset conforme sinaliza a Figura 10 abaixo:


### Figura 10:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/44833a9b-b432-49c5-8ebc-0880e57e8030)


## 2.2 Análise exploratória 

Essencialmente, faremos essa análise exploratória, utilizando os recursos de Tabela Dinâmica e plotagem de gráficos e visualizações.

### 2.2.1 Quantity x Spare Part Type

Vamos começar entendendo a distribuição das categorias das peças em relação ao total.

Para tanto vamos inserir uma Tabela Dinâmica conforme sinaliza a Figura 11 abaixo. Em seguida, podemos selecionar a opção de criar essa tabela em uma nova planilha conforme indica a Figura 12:

### Figura 11:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/bd2766b6-5bc6-4fed-88bd-1ba2d0a30a0d)

### Figura 12:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/d888d3df-b710-42b5-90ed-c5fc9e1c864f)

Para obter os dados da distribuição das categorias das peças, podemos mover para o campo de linhas a coluna Spare Part Type e para o valores a coluna Item Code por exemplo (ver Figura 13). E então, obtemos o resultado em tabela que consta na Figura 14.

### Figura 13:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/3e63c558-05f4-4e43-b78f-abbe79038a44)

### Figura 14:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/772d0df3-a55b-4e2c-b19d-af00324a7c44)


Como opção, podemos alterar a forma como esses valores serão apresentados na tabela. Para isso, podemos clicar com o botão esquerdo no campo Contagem de Item Code - Configurações do Campo de Valor - Mostrar valores como - % do Total Geral (ver Figuras 15 e 16):


### Figura 15:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/29c636ac-e253-413c-b4aa-2fa5ba5667ae)

### Figura 16:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/8b2c6058-078c-4d87-9ac5-64b81c4aeb56)

Então, teremos o seguinte resultado (Figura 17): 

### Figura 17:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/e5fd12b1-3499-40b8-a1d0-a0dd95c06b59)


Agora, para transformarmos essa tabelinha em um gráfico de barras por exemplo, podemos eliminar a categoria "vazio" a partir do Filtro. Depois disso, podemos ir na opção Inserir e selecionar a coluna conforme indicação da Figura 18:

### Figura 18:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/74ba7f97-4bc2-4b6d-96d2-646caae86bd0)

O resultado obtido é este gráfico de colunas que consta na imagem abaixo (Figura 19): 

### Figura 19:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/c43b267f-e200-433d-8ef0-a244a1d2be75)

No entanto, considerando que ele está poluído, vamos fazer algumas tratativas nele. No lado superior direito, temos a opção Botões de Campos (Figura 20).

Ao clicar nela, podemos selecionar a opção Ocultar tudo (Figura 21). 

### Figura 20: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/7e7a4785-6d31-4b15-9476-5a384c879156)

### Figura 21: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/ecafc510-19f7-4557-90b7-d5594aa1ca53)


Assim, nosso gráfico perde os botões de campos e filtros e fica mais limpo conforme imagem abaixo (Figura 22):

### Figura 22:


![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/159147a7-a490-4b27-a712-eb41e4ca9719)

Prosseguindo com a nossa limpeza, podemos eliminar esa linha de grade vertical, seguindo a opção abaixo (ver Figura 23):

### Figura 23: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/f0daff05-ed1f-40bd-aff8-0e159d503ee8)

Continuando nessa etapa de limpeza do gráfico gerado, podemos eliminar a linha vertical que delimita as categorias utilizadas no gráfico conforme demonstram as Figura 24 e 25 abaixo.

### Figura 24: 

Botão direito no gráfico - Formatar área do gráfico - Opções do Gráfico - Eixo Vertical (Categoria)

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/94f68f8f-2a82-4ecb-8b65-32a32bbde8f8)

### Figura 25

Opção de Linha - Sem Linha

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/7624189e-3e03-4543-b94f-513a070f1f08)

E, então, o resultado é este (Figura 26): 

### Figura 26: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/5ca147ed-b68e-401a-a339-529c9972d8f3)

Além disso, desejamos eliminar os rótulos de valores do eixo x. Para isso, podemos executar os seguintes comandos: 

Botão direito no gráfico - Formatar área do gráfico - Opções do Gráfico - Eixo Horizontal (Valor)

Em seguida, executamos o comando apresentado na Figura 27 abaixo: 

### Figura 27:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/bca600aa-2df8-4000-a24d-1cbd8462b0ca)

E então, obteremos o seguinte gráfico, resultado de diversas limpezas. 

### Figura 28:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/9648ca46-0d3a-4a5c-aea8-d11a8ccac141)


Agora, iremos incluir os rótulos de dados em nosos gráfico dado que optamos pela remoção dessa informação do eixo horizontal. Ver Figura 29: 

Selecionando o gráfico, clicamos no Botão + e, então, Opção Rótulo de Dados - Extremidade Externa

### Figura 29: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/44b54f62-3eef-482f-91f5-004bd051c9ac)

E eis o resultado obtido (Figura 30): 

### Figura 30:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/00659ede-bab2-406d-9b05-417f2b0d7bbc)

Além disso, desejamos retirar a legenda do lado direito (Total). Para isso, podemos selecionar o retângulo no qual essa legenda está e deletar. 

O resultado será esse (Figura 31). O que fica notório é que as barras começam a ocupar uma área maior da figura no momento que excluímos a legenda.

### Figura 31: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/25711d26-4edb-45ce-a660-17ba84ee3c64)

Clicando na caixa do título, podemos alterar a sua formatação, incluindo outra letra, tamanho. No caso abaixo, trocamos o conteúdo do título a letra de Calibri para Arial, negrito e tamanho 18 (ver Figura 32). 

### Figura 32: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/c8848a5c-efa0-49cd-8b0a-ab7a5ffe32e7)

Após uma breve pesquisa, identificamos que para alterar a ordem de disposição das colunas da tabela, podemos prosseguir da seguinte forma. 

Dado as barras do gráfico, clicamos com Botão direito - Classificar - Classificar do Maior para o Menor (ver Figura 33).

### Figura 33:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/31945508-c34b-45b4-9442-d7536d2dbf5f)

E o resultado é este que segue abaixo (Figura 34):

### Figura 34: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/7a951550-629d-4bba-9c9d-9e38f4662428)


Iremos prosseguir com a formatação da caixinha com as categorias do eixo vertical, selecionando a caixinha onde as categorias estão - Opções da Página Inicial - Fonte (Arial) e Sublinhado.

Quanto às caixinhas dos rótulos de dado, iremos incluir uma Fonte Arial, tamanho 7. 

A fim de realçar a caixinha da categoria One-Off, as peças que são o alvo principal de nossa análise, podemos seguir este passo a passo: 

Clicando na caixinha da One-off uma vez, automaticamente o Excel irá selecionar todas as caixinhas de categorias conforme apresenta a imagem abaixo: 

### Figura 35:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/8ad7ef00-8413-497a-af52-bb36415b99cc)


Então, para selecionar ESPECIFICAMENTE a caixinha da categoria One-Off podemos dar um DUPLO CLIQUE encima dela e, então, diversas opções serão habilitadas.

Sendo assim, iremos alterar a cor da Fonte na opção Rótulos de Dados para Vermelho (Figura 36). Na Página Inicial, ainda com a caixinha selecionada,
incluir  negrito e aumentar a fonte para 10. O resultado será o quê expressa a Figura 37.

### Figura 36:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/dc8d4a1d-1630-4655-9973-b1737726de7e)

### Figura 37:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/f8ac54d9-6bde-4560-b9a8-03482c42d4ef)


Por fim, partiremos para alterar as cores das barras das três diferentes categorias. Iremos optar por uma combinação de diferentes tons de cinza e realçar a borda em preto. 

Para isso, podemos clicar na primeira barra (Just In Time) e alterar a Cor para uma espécie de cinza bastante claro conforme aponta a Figura 38.

### Figura 38:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/48040eec-1fc8-49af-8a8b-62261fb1d240)

E vamos realçar a borda, indo nesta opção e selecionando a opção de cor preta (ver Figura 39). 

### Figura 39:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/af74c475-9c57-4692-bbe0-79f51addceba)

Nessa primeira etapa de formatação, obtemos a seguinte figura (ver Figura 40). 

### Figura 40:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/7cfab7fc-e8b0-42b3-ac7a-f7ba7e739153)

Por fim, aplicaremos as mesmas regras de formatação para a barra da categoria Fast Moving Item. No caso da categoria One-Off, iremos realçá-la com uma cor cinza mais escura e a borda preta. 

O resultado de nosso gráfico após essa etapa será este (ver Figura 41): 


### Figura 41:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/dcc50ea2-41bc-4d99-9209-5032fa240aba)

Para finalizar, selecionaremos o gráfico e alteraremos a borda com preenchimento de Linha Sólida e Cor Preta (Figura 42):

### Figura 42: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/c93abe46-93ce-4b3c-8767-dbf167616edf)

E este será nosso resultado final do gráfico Quantity x Spare Part Type (Figura 43):

### Figura 43:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/f3b43ad8-7554-4f66-81c2-6bf0be2240d1)

Para os propósitos dessa análise, vamos chamá-lo de Gráfico 1. 

## 2.2.2 Quantity x Spare Part Type x Location

Nesse segundo momento de nossa análise exploratória, iremos investigar a relaçaõ entre o tipo de peça sobressalente e a localização. Retomando o entendimento dessa coluna, cada categoria significa o seguinte:

company site office: escritório local da empresa (indicativo de facilidade da obtenção da peça)

centralized: centralizada (peça alocada em local centralizada, possivelmente alguma matriz ou local especializado para armazenamento 

others: não especificado. 
     
A diferença desta análise será que incluiremos duas hierarquias em nossa análise, a saber spare part type e location e daí calcular as quantidades de peças. Então, em nossa Tabela Dinâmica, incluiremos duas categorias nossas linhas, a saber as próprias colunas spare part type e location. O resultado será uma tabela com dois níveis de análise (ver Figura 44):

### Figura 44:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/6fd4b4bc-06a9-4f57-aa81-a982394c19b6)

Consequentemente, o gráfico derivado dessa tabela terá a seguinte disposição (ver Figura 45). 

### Figura 45: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/993905f4-6b7b-4015-b37b-bba103b36522)

Então, prosseguiremos com as formatações e limpezas necessárias semelhantes às que aplicamos no gráfico da análise anterior, a saber limpar campos, retirar linhas verticais, alteração de fonte, inclusão de rótulos de dados.

Feita essa primeira etapa de formatações, obtivemos o seguinte gráfico (ver Figura 46). 

### Figura 46:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/bfa47a99-109b-47cc-b75e-a369c50800d3)

Para invertermos a disposição das categorias, vamos em opções do Eixo Horizontal e aplicar a condição presente na imagem abaixo (ver Figura 47). 

### Figura 47:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/bee77e5b-0c73-4104-9a4e-d7f84842d698)

 O resultado será esse (ver Figura 48). 

 ### Figura 48:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/5eae528c-1c1f-46e9-9004-4e970ef68d47)

Dado que temos dois níveis em nosso rótulo de dados, vamos alterar a distância entre eles na opção Eixo Horizontal Categoria - Rótulos - Distância do Eixo (alterado p/350) (figura 49).

### Figura 49:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/020ab484-1719-4832-9d89-653e7900a00c)

Então, somando essa formatação com a aplicação de formatações semelhantes às que fizemos na análise anterior, nosso gráfico final (Gráfico 2) ficará dessa forma (ver Figura 50). 

### Figura 50:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/70d73291-196f-4527-97cc-9bbe1c462122)

Podemos refinar nosso entendimento da categoria others dentro da coluna LOCATION. Aqui, fizemos uma tabela dinâmica incluindo nos níveis de análise as colunas LOCATION e SPECIFY.
E todos os casos de Location = "Others" são peças que são adquiridas com fornecedor (categoria Vendor By Purchase Order da coluna SPECIFY). (ver Figura 51). 

### Figura 51:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/a526d392-52da-4cf8-9fa8-b64a6b8d5bcf)


Sendo assim, o significado da categoria Others da coluna LOCATION possivelmente é de que a peça está AINDA COM O FORNECEDOR ou com algum subcontratado desse fornecedor e, não, diretamente para rápido manejo da instituição. Podemos trabalhar com essa hipótese, porém, dentro de um contexto de projeto interno à empresa, poderíamos tentar tirar a dúvida sobre o significado dessa categoria mais assertivamente com alguém vinculado a essa área.

## 2.2.3 Quantity x Spare Part Type x Specify

Agora vamos trabalhar com a análise de dois níveis, a saber colunas Spare Part Type e Specify para quantidade de peças.Nessa análise, aplicaremos rigorosamente as mesmas regras de formatação das que foram aplicadas na análise anterior, resultando no seguinte gráfico (Gráfico 3), ver figura 52 que é semelhante ao gráfico 2

### Figura 52: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/e483e055-65ea-43c8-9be6-59529954c586)

### 2.2.4 Spare Part Type x Maximum Price Per Nos

Vamos começar com uma tabela dinâmica que envolva essas colunas. Por padrão, a coluna é habilitada para realizar a soma de todos os valores da coluna Maximum Price Per Nos. (ver Figura 53).

### Figura 53:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/8e960ba9-8b33-44e3-b15d-4321969e6e2c)

No entanto, desejamos trabalhar com a Média. Então, iremos alterar essa opção para Média. 

Clicar no campo Maximum Price Per Nos com botão esquerdo - Configurações do Campo de Valor - Média (ver Figura 54).

### Figura 54:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/11d86a74-6c09-4fbc-a2c0-e84abaa71c57)

Logo em seguida, vamos selecionar os valores resultantes, ir na Página Inicial - Número. O resultado será esse (ver Figura 55). 

### Figura 55: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/78c79620-95e6-4f39-b4ed-638598fc4c4e)

Aqui, iremos fazer uma visualização um tanto diferente das produzidas anteriormente. Inicialmente vamos copiar os valores gerados pela Tabela Dinâmica, incluindo a Média Geral, em uma
nova tabela. E, depois formatamos todas essas colunas como tabela.

Selecionar as colunas - Inserir - Formatar como Tabela - Minha tabela tem cabeçalhos. 

O resultado será a figura abaixo:

### Figura 56:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/3da1508b-8ac1-45de-869f-89d81415055e)


Agora, iremos incluir ícones (bolinh vermelha/verde) para os valores de média da categoria que ultrapassarem os valores da Média Geral.

Para isso selecionamos a coluna Maximum Price Per Nos Média - Formatação Condicional - Conjunto de ícones - Mais Regras (ver Figura 57). 

### Figura 57:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/6448d50c-5ae1-4b25-bc77-d9b46032e4b1)


E então, o resultado dessa opção será essa tela: 

### Figura 58:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/c9575134-6bd8-4f4f-aff4-ed28209c64fb)

Ao clicarmos em Ok, será feita a seguinte formatação. 

### Figura 59:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/57962eaf-2cc4-47d2-8791-6dd09b3f33f1)

No entanto, desejamos realçar como negativo (cor vermelha) os valores acima da média e não os que estão abaixo. Sendo assim, teremos que modificar uma opção na tela de Gerenciar Regras. 

Ao invés das opções da sequência abaixo (figura 60), vamos aplicar a sequência da figura 61.

### Figura 60:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/84c03b70-bb85-4f37-9e4a-483b7f1399bf)


### Figura 61: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/3710df0e-3c98-4a24-a13c-ad44c8e6f01d)

Alterando a configuração e clicando em Ok, o resultado em nossa tabela será este: 

### Figura 62:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/90e73eaf-f732-4380-bf29-7c1598952de9)

Então, copiamos essa tabela para fora dessa formatação de tabela e obteremos a visualização que utilizaremos para a análise (tabela 1). 


### 2.2.5 Spare Part Type x Minimum Price Per Nos

Para essa análise, vamos reproduzir o mesmo passo a passo da análise anterior e obteremos a visualização abaixo (tabela 2). 

### Figura 63:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/47c8d113-af81-4d04-be32-dc644dafe104)

### 2.2.6 Spare Part Type x Current Stock Level Has Min

Vamos agora confeccionar uma tabela dinâmica e gráfico envolvendo as colunas spare part type e current stock level has min e as quantidades, procedendo de forma semelhante ao passo a passo que utilizamos
na confecção das outras análises. 

No entanto, diferentemente das análises anteriores, vamos produzir tabelas para os diferentes de tipos de peças de forma individual. 

Para isso, dado a tabela dinâmica, podemos filtrar, por exemplo, a coluna One-Off, o quê retornará apenas as informações dessa coluna (ver figura 64). 

Clicar com botão esquerdo no campo Rótulo de Linha e selecionar a categoria One-Off por exemplo.

### Figura 64: 

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/f87852cd-b9bf-499e-a957-f7483caad1fa)

Desse filtro, podemos copiar as informações da tabela dinâmica para outras células limpas e alterar a formatação. Ao final, teremos essa tabela que contém a quantidade total de peças
da categoria One Off por diferente situação de estoque (chamaremos de tabela 3). As tabelas correlatas para as peças de tipo Just in Time (tabela 4) e Fast Moving Item (tabela 5) - Ver figura abaixo.

### Figura 65:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/49f673a3-3400-4ce4-979c-fb0f19db3861)


Para os propósitos dessa análise, vamos considerar que Current Stock Level Has Min = Same significa que o estoque da peça possui exatamente a quantidade mínima desejável para a peça (valor da Coluna Min Nos) enquanto que o Current Stock Level Has Min = No signfica que o estoque da peça possui menos do que a quantidade mínima desejável para a peça. Essas duas situações, iremos caracterizar como uma situação de vulnerabilidade da peça.



### 2.2.6 Criando um dataset com os dados das peças One-Off com situação vulnerável de estoque

Pensando que o objetivo inicial de nossa análise é identificar uma possível situação de vulnerabilidade das peças sobressalentes de tipo one-off, vamos criar um dataset unicamente com essas peças. 

Para isso, podemos abrir uma nova planiha em nossa base de dados, no botão + na extremidade esquerda de nosso arquivo. Para filtrar as colunas com as condições que desejamos, podemos utilizar a função FILTRO do Excel. 

Desejamos filtrar do dataset original, unicamente as colunas spare part type = One Off e current stock level has min = No/Same (ver Figura 66:)

### Figura 66:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/744115b9-1dd4-4502-ba19-97ab2561004b)

Na fórmula FILTRO do Excel, o "*" significa "E" enquanto que o "+" significa "OU". Aplicando a fórmula, obtivemos todas as linhas do dataset original que respeitam as condições estipuladas (ver Figura 67).

### Figura 67:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/72968d20-8a9a-48d6-8569-70442e9f02e9)

Para completar nossa tabela, vamos copiar o cabeçalho do dataset original neste novo dataset filtrado. 

Tendo o novo dataset já com o cabeçalho vamos copiar e colar todas as linhas para uma nova aba da planilha, utilizando a função de Colar somente Valores.

Dessa forma, o nosso dataset novo perderá a referência com o dataset de origem. Essa nossa nova aba da planilha receberá o nome de only_one_off

Então, iremos começar formatando o only_one_off como Tabela e alterando os tipos de dados das colunas para que sejam compatíveis com o dataset original. 

Superada essa etapa, verificamos que as colunas Brand e Model do only-one-off incluíram o número "0" nas linhas vazias, destoando do original. Então, iremos ajustar essa informação. 

Podemos efetuar essa tarefa manualmente uma vez que não poderemos utilizar o editor do Power Query para substituir esses valores. Basta filtrarmos no only_one_off as colunas Brand e Model e apagar os valores 
"0" e, assim, essas linhas ficarão vazias. 

Após ligação com a secretaria da gestão, foi definido que a listagem das peças one-off deveria ser enviada por email em formato csv. Então, iremos copiar a tabela que contém apenas as peças one-off para outro arquivo csv, salvar e  encaminhar por email. (arquivo "only_one_off" compartilhado aqui neste repositório).



# 3. Discutindo a problemática da análise

A gestão hospitalar gostaria de visualizar o resultado das análises em uma apresentação de Power Point a ser enviada pelo email pelo Analista de Dados previamente antes da reunião. (arquivo de nome
"presentation"). Foi sinalizado que essa apresentação deve ser o mais objetiva possível, servindo apenas para dar o start das discussões que se desenvolverão a partir dos achados da análise.

Vamos salvar todas os gráficos e tabelas dessa análise pois depois as incluíremos na apresentação. Para isso, podemos dar botão direito no gráfico/tabela - Salvar como imagem - nomear o arquivo e selecionar a pasta para o salvamento. (ver Figura 68).

### Figura 68:

![image](https://github.com/alekaloupis/spare_parts_inventory/assets/107442506/96af1f9a-c9c1-4c7b-a305-42981624debf)


Sendo que no momento da reunião, o analista se encarregará de apresentar os resultados.


# 4. Próximos passos

Recebida a análise pela equipe diretiva e feita a reunião, o analista receberá possíveis fedbacks e novas demandas referentes ao problema das peças. 


# 5. Tecnologias envolvidas no projeto 

Excel, Power Query, Power Point







