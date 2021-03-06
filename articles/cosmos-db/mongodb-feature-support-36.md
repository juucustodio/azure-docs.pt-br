---
title: Sintaxe e recursos compatíveis da API do Azure Cosmos DB para MongoDB (versão 3.6)
description: Saiba mais sobre a sintaxe e os recursos compatíveis da API do Azure Cosmos DB para MongoDB (versão 3.6).
ms.service: cosmos-db
ms.subservice: cosmosdb-mongo
ms.topic: overview
ms.date: 08/07/2020
author: sivethe
ms.author: sivethe
ms.openlocfilehash: 0ca1f1222881a2b4ca640fa31192bd1c151ebd9f
ms.sourcegitcommit: e46f9981626751f129926a2dae327a729228216e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98028838"
---
# <a name="azure-cosmos-dbs-api-for-mongodb-36-version-supported-features-and-syntax"></a>API do Azure Cosmos DB para MongoDB (versão 3.6): sintaxe e recursos compatíveis
[!INCLUDE[appliesto-mongodb-api](includes/appliesto-mongodb-api.md)]

O Azure Cosmos DB é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft. Você pode se comunicar com a API do Azure Cosmos DB para MongoDB usando qualquer um dos [drivers](https://docs.mongodb.org/ecosystem/drivers) de cliente de software livre do MongoDB. A API do Azure Cosmos DB para MongoDB permite o uso de drivers de cliente existentes ao aderir ao [protocolo de transmissão](https://docs.mongodb.org/manual/reference/mongodb-wire-protocol) do MongoDB.

Usando a API do Azure Cosmos DB para MongoDB, você pode aproveitar os benefícios do MongoDB com os quais está acostumado, com todas as funcionalidades empresariais que o Cosmos DB oferece: [distribuição global](distribute-data-globally.md), [fragmentação automática](partitioning-overview.md), garantias de disponibilidade e latência, criptografia em repouso, backups e muito mais.

## <a name="protocol-support"></a>Suporte de protocolo

Por padrão, a API do Azure Cosmos DB para MongoDB é compatível com o servidor do MongoDB versão **3.6** em novas contas. Os operadores com suporte e qualquer limitação ou exceções estão listadas abaixo. Qualquer driver de cliente que entenda esses protocolos poderá conectar-se à API do Azure Cosmos DB para MongoDB. Observe que, ao usar a API do Azure Cosmos DB para contas do MongoDB, a versão 3.6 da conta tem o ponto de extremidade no formato `*.mongo.cosmos.azure.com`, enquanto a versão 3.2 da conta tem o ponto de extremidade no formato `*.documents.azure.com`.

## <a name="query-language-support"></a>Suporte de linguagem de consulta

A API do Azure Cosmos DB para MongoDB fornece um suporte abrangente para construções de linguagem de consulta do MongoDB. As seções a seguir mostram a lista detalhada de operações de servidor, operadores, estágios, comandos e opções atualmente compatíveis com o Azure Cosmos DB.

> [!NOTE]
> Este artigo lista apenas os comandos de servidor com suporte e exclui as funções de wrapper do lado do cliente. Funções de wrapper do lado do cliente, como `deleteMany()` e `updateMany()`, utilizam internamente os comandos de servidor `delete()` e `update()`. As funções que utilizam comandos de servidor com suporte são compatíveis com a API do Azure Cosmos DB para MongoDB.

## <a name="database-commands"></a>Comandos de banco de dados

A API do Azure Cosmos DB para MongoDB é compatível com os seguintes comandos de banco de dados:

### <a name="query-and-write-operation-commands"></a>Comandos de operação de consulta e gravação

|Comando  |Com suporte |
|---------|---------|
|excluir | Sim |
|localizar | Sim     |
|findAndModify | Sim  |
|getLastError|   Sim |
|getMore  |  Sim  |
|getPrevError | Não  |
|insert  |   Sim  |
|parallelCollectionScan  | Sim   |
|resetError |    Não  |
|atualizar  |   Sim  |
|[Alterar os fluxos](mongodb-change-streams.md)  |  Sim  |
|GridFS |   Sim  |

### <a name="authentication-commands"></a>Comandos de autenticação

|Comando  |Com suporte |
|---------|---------|
|authenticate    |   Sim      |
|logout    |      Sim   |
|getnonce   |    Sim     |


### <a name="administration-commands"></a>Comandos de administração

|Comando  |Com suporte |
|---------|---------|
|Coleções limitadas   |   Não      |
|cloneCollectionAsCapped     |   Não      |
|collMod     |   Não      |
|collMod: expireAfterSeconds   |   Não      |
|convertToCapped   |  Não       |
|copydb     |  Não       |
|create   |    Sim     |
|createIndexes     |  Sim       |
|currentOp     |  Sim       |
|drop     |   Sim      |
|dropDatabase     |  Sim       |
|dropIndexes     |   Sim      |
|filemd5    |   Sim      |
|killCursors    |  Sim       |
|killOp     |   Não      |
|listCollections     |  Sim       |
|listDatabases     |  Sim       |
|listIndexes     |  Sim       |
|reIndex     |    Sim     |
|renameCollection     |    Não     |
|ConnectionStatus    |     Não    |

### <a name="diagnostics-commands"></a>Comandos de diagnóstico

|Comando  |Com suporte |
|---------|---------|
|buildInfo         |   Sim      |
|collStats    |  Sim       |
|connPoolStats     |  Não       |
|ConnectionStatus     |  Não       |
|dataSize     |   Não      |
|dbHash    |    Não     |
|dbStats     |   Sim      |
|explain     |   Sim      |
|explain: executionStats     |   Sim      |
|recursos     |    Não     |
|hostInfo     |   Não      |
|listDatabases         |   Sim      |
|listCommands     |  Não       |
|profiler     |  Não       |
|serverStatus     |  Não       |
|top     |    Não     |
|whatsmyuri     |   Sim      |

<a name="aggregation-pipeline"></a>

## <a name="aggregation-pipelinea"></a>Pipeline de agregação</a>

### <a name="aggregation-commands"></a>Comandos de agregação

|Comando  |Com suporte |
|---------|---------|
|aggregate |   Sim  |
|count     |   Sim  |
|distinct  | Sim |
|mapReduce | Não |

### <a name="aggregation-stages"></a>Estágios de agregação

|Comando  |Com suporte |
|---------|---------|
|$collStats    |Não|
|$project    |Sim|
|$match    |Sim|
|$redact|    Sim|
|$limit    |Sim|
|$skip    |Sim|
|$unwind|    Sim|
|$group    |    Sim|
|$sample|        Sim|
|$sort    |Sim|
|$geoNear|    Não|
|$lookup    |    Sim|
|$out        |Sim|
|$indexStats|        Não|
|$facet    |Sim|
|$bucket|    Não|
|$bucketAuto|    Não|
|$sortByCount|    Sim|
|$addFields    |Sim|
|$replaceRoot|    Sim|
|$count    |Sim|
|$currentOp|    Não|
|$listLocalSessions    |Não|
|$listSessions    |Não|
|$graphLookup    |Sim|

### <a name="boolean-expressions"></a>Expressões boolianas

|Comando  |Com suporte |
|---------|---------|
|$and| Sim|
|$or|Sim|
|$not|Sim|

### <a name="set-expressions"></a>Expressões de definição

|Comando  |Com suporte |
|---------|---------|
| $setEquals | Sim|
|$setIntersection|Sim|
| $setUnion|Sim|
| $setDifference|Sim|
| $setIsSubset|Sim|
| $anyElementTrue|Sim|
| $allElementsTrue|Sim|

### <a name="comparison-expressions"></a>Expressões de comparação

|Comando  |Com suporte |
|---------|---------|
|$cmp     |  Sim       |
|$eq|    Sim| 
|$gt |    Sim| 
|$gte|    Sim| 
|$lt    |Sim|
|$lte|    Sim| 
|$ne    |    Sim| 
|$in    |    Sim| 
|$nin    |    Sim| 

### <a name="arithmetic-expressions"></a>Expressões aritméticas

|Comando  |Com suporte |
|---------|---------|
|$abs |  Sim       |
| $add |  Sim       |
| $ceil |  Sim       |
| $divide |  Sim       |
| $exp |  Sim       |
| $floor |  Sim       |
| $ln |  Sim       |
| $log |  Sim       |
| $log10 |  Sim       |
| $mod |  Sim       |
| $multiply |  Sim       |
| $pow |  Sim       |
| $sqrt |  Sim       |
| $subtract |  Sim       |
| $trunc |  Sim       |

### <a name="string-expressions"></a>Expressões de cadeia de caracteres

|Comando  |Com suporte |
|---------|---------|
|$concat |  Sim       |
| $indexOfBytes|  Sim       |
| $indexOfCP|  Sim       |
| $split|  Sim       |
| $strLenBytes|  Sim       |
| $strLenCP|  Sim       |
| $strcasecmp|  Sim       |
| $substr|  Sim       |
| $substrBytes|  Sim       |
| $substrCP|  Sim       |
| $toLower|  Sim       |
| $toUpper|  Sim       |

### <a name="text-search-operator"></a>Operador de pesquisa de texto

|Comando  |Com suporte |
|---------|---------|
| $meta | Não|

### <a name="array-expressions"></a>Expressões de matriz

|Comando  |Com suporte |
|---------|---------|
|$arrayElemAt    |    Sim|
|$arrayToObject|    Sim|
|$concatArrays    |    Sim|
|$filter    |    Sim|
|$indexOfArray    |Sim|
|$isArray    |    Sim|
|$objectToArray    |Sim|
|$range    |Sim|
|$reverseArray    |    Sim|
|$reduce|    Sim|
|$size    |    Sim|
|$slice    |    Sim|
|$zip    |    Sim|
|$in    |    Sim|

### <a name="variable-operators"></a>Operadores variáveis

|Comando  |Com suporte |
|---------|---------|
|$map    |Não|
|$let    |Sim|

### <a name="system-variables"></a>Variáveis do sistema

|Comando  |Com suporte |
|---------|---------|
|$$CURRENT|    Sim|
|$$DESCEND|        Sim|
|$$KEEP        |Sim|
|$$PRUNE    |    Sim|
|$$REMOVE    |Sim|
|$$ROOT        |Sim|

### <a name="literal-operator"></a>Operador literal

|Comando  |Com suporte |
|---------|---------|
|$literal    |Sim|

### <a name="date-expressions"></a>Expressões de data

|Comando  |Com suporte |
|---------|---------|
|$dayOfYear    |Sim    |
|$dayOfMonth|    Sim    |
|$dayOfWeek    |Sim    |
|$year    |Sim    |
|$month    |Sim|    
|$week    |Sim    |
|$hour    |Sim    |
|$minute|    Sim|    
|$segundo    |Sim    |
|$millisecond|    Sim|    
|$dateToString    |Sim    |
|$isoDayOfWeek    |Sim    |
|$isoWeek    |Sim    |
|$dateFromParts|    Não|    
|$dateToParts    |Não    |
|$dateFromString|    Não|
|$isoWeekYear    |Sim    |

### <a name="conditional-expressions"></a>Expressões condicionais

|Comando  |Com suporte |
|---------|---------|
| $cond| Sim|
| $ifNull| Sim|
| $switch |Sim|

### <a name="data-type-operator"></a>Operador de tipo de dados

|Comando  |Com suporte |
|---------|---------|
| $type| Sim|

### <a name="accumulator-expressions"></a>Expressões do acumulador

|Comando  |Com suporte |
|---------|---------|
|$sum    |Sim    |
|$avg    |Sim    |
|$first|    Sim|
|$last    |Sim    |
|$max    |Sim    |
|$min    |Sim    |
|$push|    Sim|
|$addToSet|    Sim|
|$stdDevPop|    Não    |
|$stdDevSamp|    Não|

### <a name="merge-operator"></a>Operador de mesclagem

|Comando  |Com suporte |
|---------|---------|
| $mergeObjects | Sim|

## <a name="data-types"></a>Tipos de dados

|Comando  |Com suporte |
|---------|---------|
|Double    |Sim    |
|String    |Sim    |
|Objeto    |Sim    |
|Array    |Sim    |
|Binary Data    |Sim|    
|ObjectId    |Sim    |
|Boolean    |Sim    |
|Data    |Sim    |
|Nulo    |Sim    |
|Inteiro de 32 bits (int)    |Sim    |
|Timestamp    |Sim    |
|Inteiro de 64 bits (longo)    |Sim    |
|MinKey    |Sim    |
|MaxKey    |Sim    |
|Decimal128    |Sim|    
|Expressão regular    |Sim|
|JavaScript    |Sim|
|JavaScript (com escopo)|    Sim    |
|Indefinido    |Sim    |

## <a name="indexes-and-index-properties"></a>Índices e propriedades de índice

### <a name="indexes"></a>Índices

|Comando  |Com suporte |
|---------|---------|
|Índice de campo único    |Sim    |
|Índice composto    |Sim    |
|Índice de várias chaves    |Sim    |
|Índice de texto    |Não|
|2dsphere    |Sim    |
|Índice 2D    |Não    |
|Índice de hash    | Sim|

### <a name="index-properties"></a>Propriedades de índice

|Comando  |Com suporte |
|---------|---------|
|TTL|    Sim    |
|Exclusivo    |Sim|
|Parcial|    Não|
|Não diferencia maiúsculas de minúsculas    |Não|
|Esparsos    |Não |
|Segundo plano|    Sim |

## <a name="operators"></a>Operadores

### <a name="logical-operators"></a>Operadores lógicos

|Comando  |Com suporte |
|---------|---------|
|$or    |    Sim|
|$and    |    Sim|
|$not    |    Sim|
|$nor    |    Sim| 

### <a name="element-operators"></a>Operadores de elemento

|Comando  |Com suporte |
|---------|---------|
|$exists|    Sim|
|$type    |    Sim|

### <a name="evaluation-query-operators"></a>Operadores de consulta de avaliação

|Comando  |Com suporte |
|---------|---------|
|$expr    |    Não|
|$jsonSchema    |    Não|
|$mod    |    Sim|
|$regex |    Sim|
|$text    | Não (Sem suporte. Use $regex.)| 
|$where    |Não| 

Em consultas de $regex, as expressões ancoradas à esquerda permitem a pesquisa de índice. No entanto, usar o modiciador 'i' (não sensível a maiúsculas e minúsculas) e o modificador 'm' (várias linhas) faz com que a coleção verifique todas as expressões.

Quando houver a necessidade de se incluir '$' ou '|', é melhor criar duas (ou mais) consultas regex. Por exemplo, considerando a seguinte consulta original ```find({x:{$regex: /^abc$/})```, ela deve ser modificada da seguinte maneira:

```find({x:{$regex: /^abc/, x:{$regex:/^abc$/}})```.

A primeira parte usará o índice para restringir a pesquisa a esses documentos começando com ^abc e a segunda parte corresponderá às entradas exatas. O operador de barra '|' atua como uma função "or" – a consulta ```find({x:{$regex: /^abc|^def/})``` faz a correspondência dos documentos em que o campo 'x' tem valores que começam com "abc" ou "def". Para utilizar o índice, é recomendável dividir a consulta em duas consultas diferentes unidas pelo operador $or: ```find( {$or : [{x: $regex: /^abc/}, {$regex: /^def/}] })```.

### <a name="array-operators"></a>Operadores de matriz

|Comando  |Com suporte | 
|---------|---------|
| $all | Sim| 
| $elemMatch | Sim| 
| $size | Sim | 

### <a name="comment-operator"></a>Operador de comentário

|Comando  |Com suporte | 
|---------|---------|
$comment |Sim| 

### <a name="projection-operators"></a>Operadores de projeção

|Comando  |Com suporte |
|---------|---------|
|$elemMatch    |Sim|
|$meta|    Não|
|$slice    | Sim|

### <a name="update-operators"></a>Operadores de atualização

#### <a name="field-update-operators"></a>Operadores de atualização de campo

|Comando  |Com suporte |
|---------|---------|
|$inc    |    Sim|
|$mul    |    Sim|
|$rename    |    Sim|
|$setOnInsert|    Sim|
|$set    |Sim|
|$unset| Sim|
|$min    |Sim|
|$max    |Sim|
|$currentDate    | Sim|

#### <a name="array-update-operators"></a>Operadores de atualização de matriz

|Comando  |Com suporte |
|---------|---------|
|$    |Sim|
|$[]|    Sim|
|$[<identifier>]|    Sim|
|$addToSet    |Sim|
|$pop    |Sim|
|$pullAll|    Sim|
|$pull    |Sim|
|$push    |Sim|
|$pushAll| Sim|


#### <a name="update-modifiers"></a>Atualizar modificadores

|Comando  |Com suporte |
|---------|---------|
|$each    |    Sim|
|$slice    |Sim|
|$sort    |Sim|
|$position    |Sim|

#### <a name="bitwise-update-operator"></a>Operador de atualização bit a bit

|Comando  |Com suporte |
|---------|---------|
| $bit    |    Sim|    
|$bitsAllSet    |    Não|
|$bitsAnySet    |    Não|
|$bitsAllClear    |Não|
|$bitsAnyClear    |Não|

### <a name="geospatial-operators"></a>Operadores geoespaciais

Operador | Com suporte| 
--- | --- |
$geoWithin | Sim |
$geoIntersects | Sim | 
$near |  Sim |
$nearSphere |  Sim |
$geometry |  Sim |
$minDistance | Sim |
$maxDistance | Sim |
$center | Não |
$centerSphere | Não |
$box | Não |
$polygon |  Não |

## <a name="cursor-methods"></a>Métodos de cursor

|Comando  |Com suporte |
|---------|---------|
|cursor.batchSize()    |    Sim|
|cursor.close()    |Sim|
|cursor.isClosed()|        Sim|
|cursor.collation()|    Não|
|cursor.comment()    |Sim|
|cursor.count()    |Sim|
|cursor.explain()|    Não|
|cursor.forEach()    |Sim|
|cursor.hasNext()    |Sim|
|cursor.hint()    |Sim|
|cursor.isExhausted()|    Sim|
|cursor.itcount()    |Sim|
|cursor.limit()    |Sim|
|cursor.map()    |Sim|
|cursor.maxScan()    |Sim|
|cursor.maxTimeMS()|    Sim|
|cursor.max()    |Sim|
|cursor.min()    |Sim|
|cursor.next()|    Sim|
|cursor.noCursorTimeout()    |Não|
|cursor.objsLeftInBatch()    |Sim|
|cursor.pretty()|    Sim|
|cursor.readConcern()|    Sim|
|cursor.readPref()        |Sim|
|cursor.returnKey()    |Não|
|cursor.showRecordId()|    Não|
|cursor.size()    |Sim|
|cursor.skip()    |Sim|
|cursor.Sort()    |    Sim|
|cursor.tailable()|    Não|
|cursor.toArray()    |Sim|

## <a name="sort-operations"></a>Classificar operações

Ao usar a operação `findOneAndUpdate`, há suporte para operações de classificação em um único campo, mas não há para operações em vários campos.

## <a name="unique-indexes"></a>Índices exclusivos

[Índices exclusivos](mongodb-indexing.md#unique-indexes) verificam se um campo específico não tem valores duplicados em todos os documentos em uma coleção, de modo semelhante à maneira como a exclusividade é preservada na chave "_id" padrão. Você pode criar índices exclusivos no Cosmos DB usando o comando `createIndex` com o parâmetro de restrição `unique`:

```javascript
globaldb:PRIMARY> db.coll.createIndex( { "amount" : 1 }, {unique:true} )
{
        "_t" : "CreateIndexesResponse",
        "ok" : 1,
        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 4
}
```

## <a name="compound-indexes"></a>Índice composto

[Índices compostos](mongodb-indexing.md#compound-indexes-mongodb-server-version-36) fornecem uma forma de criar um índice para grupos de campos para até oito campos. Esse tipo de índice difere dos índices compostos nativos do MongoDB. No Azure Cosmos DB, os índices compostos são usados para operações de classificação aplicadas a vários campos. Para criar um índice composto, você precisa especificar mais de uma propriedade como o parâmetro:

```javascript
globaldb:PRIMARY> db.coll.createIndex({"amount": 1, "other":1})
{
        "createdCollectionAutomatically" : false, 
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 2,
        "ok" : 1
}
```

## <a name="time-to-live-ttl"></a>Vida útil (TTL)

O Cosmos DB é compatível com uma TTL (vida útil) com base no carimbo de data/hora do documento. A TTL pode ser habilitada para coleções acessando o [portal do Azure](https://portal.azure.com).

## <a name="user-and-role-management"></a>Gerenciamento de usuários e funções

O Cosmos DB ainda não dá suporte a usuários e funções. No entanto, o Cosmos DB dá suporte ao Azure RBAC (controle de acesso baseado em função do Azure) e as senhas/chaves de leitura/gravação e somente leitura que podem ser obtidas por meio do [portal do Azure](https://portal.azure.com) (página Cadeia de conexão).

## <a name="replication"></a>Replicação

O Cosmos DB é compatível com a replicação automática nativa em camadas mais baixas. Essa lógica é estendida para atingir também réplica global e baixa. O Cosmos DB não dá suporte a comandos de replicação manual.

## <a name="write-concern"></a>Problema de Gravação

Alguns aplicativos dependem de uma [Preocupação de gravação](https://docs.mongodb.com/manual/reference/write-concern/) que especifica o número de respostas necessárias durante uma operação de gravação. Devido à forma como o Cosmos DB lida com a replicação em segundo plano, todas as gravações são automaticamente Quorum, por padrão. Toda preocupação de gravação especificada pelo código do cliente é ignorada. Saiba mais em [Como usar níveis de consistência para maximizar a disponibilidade e o desempenho](consistency-levels.md).

## <a name="sharding"></a>Fragmentação

O Azure Cosmos DB oferece suporte à fragmentação automática, do lado do servidor. Ele gerencia a criação, o posicionamento e o balanceamento de fragmentos automaticamente. O Azure Cosmos DB não dá suporte a comandos de fragmentação manual, o que significa que você não precisa invocar comandos como addShard, balancerStart, moveChunk etc. Você só precisa especificar a chave de fragmentação ao criar os contêineres ou consultar os dados.

## <a name="sessions"></a>Sessões

O Azure Cosmos DB ainda não dá suporte a comandos de sessões do lado do servidor.

## <a name="next-steps"></a>Próximas etapas

- Para obter mais informações, confira [Recursos de versão Mongo 3.6](https://devblogs.microsoft.com/cosmosdb/azure-cosmos-dbs-api-for-mongodb-now-supports-server-version-3-6/)
- Saiba como [usar o Studio 3T](mongodb-mongochef.md) com a API do Azure Cosmos DB para MongoDB.
- Saiba como [usar o Robo 3T](mongodb-robomongo.md) com a API do Azure Cosmos DB para MongoDB.
- Explore [exemplos](mongodb-samples.md) do MongoDB com a API do Azure Cosmos DB para MongoDB.

<sup>Observação: este artigo descreve um recurso do Azure Cosmos DB que fornece a compatibilidade de protocolo de transmissão com bancos de dados MongoDB. A Microsoft não executa bancos de dados MongoDB para fornecer esse serviço. O Azure Cosmos DB não está afiliado à MongoDB, Inc.</sup>
