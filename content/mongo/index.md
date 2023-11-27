---
layout: internal
---

# MongoDB

Fontes:

* Anotações do curso: MongoDB do básico ao avançado (c/ Mongoose e projetos), do Matheus Battisti na Udemy
* Página do MongoDB no [Docker Hub](https://hub.docker.com/r/mongodb/mongodb-community-server)

## Relacional vs Não relacional

* Os bancos relacionais demandam uma forte configuração de tabelas, colunas e relações entre tabelas para o seu funcionamento;
* Os não relacionais não são rigorosos quanto a isso, podemos criar colunas quando um dado é inserido;
* Essa característica gera flexibilidade para o não relacional e também poder ser sinônimo de desorganização;
* Apesar do nome, o não relacional pode ter relações entre collections.

## Instalando o MongoDB

A melhor maneira de se usar o MongoDB é através do Docker. Neste [endereço](https://www.mongodb.com/compatibility/docker) tem as instruções necessárias para subir um container com o MongoDB. A seguir fiz o meu resumo da parte que me interessa.

Vamos criar um container docker a partir de uma imagem do MongoDB versão *6.0-ubi8*. A ideia é acessar esse Mongo através do Compass no endereço mongodb://user:pass@localhost:27017, sendo que para isso publiquei a porta 27017, criei um volume para persistência dos dados e também estou usando variáveis de ambiente para inicializar o MongoDB com o usuário root.

Criando um volume:

`docker volume create mongodb-vol`

Cria uma variável para setar a tag do mongo que irá rodar:

`export MONGODB_VERSION=6.0-ubi8`

Executa o container:

`docker run --name mongodb -d -p 27017:27017 -v mongodb-vol:/data/db -e MONGO_INITDB_ROOT_USERNAME=user -e MONGO_INITDB_ROOT_PASSWORD=pass mongodb/mongodb-community-server:$MONGODB_VERSION`

## Instalando o Compass

Primeiro baixe o pacote do compass [veja aqui a última versão](https://www.mongodb.com/docs/compass/current/install/)

`wget https://downloads.mongodb.com/compass/mongodb-compass_1.40.4_amd64.deb`

Em seguida instale o pacote baixado

`sudo dpkg -i mongodb-compass_1.40.4_amd64.deb`

## Conceitos

No mongoDb não existe o conceito de tabela, o que se guarda são *documents* dentro de *collections*.

Existem os seguintes tipos de relacionamento entre Collections

* One to Many
* Many to Many
* One to One
* Subdocuments

Mongoose - um ODM, ou seja um framework para se trabalhar com o MongoDB de uma forma mais simplista

Na minha máquina o MongoDB já foi instalado, o passo a passo está no arquivo de configuração do ambiente de desenvolvimento
Para testar não para o terminal. Utilize o aplicativo MongoDB Compass que foi instalado junto com a aplicação.
No próprio aplicativo já existe um MongoSh, que é o shell para o mongo. se quiser ver funcionando rode o seguinte comando

## Comandos

Para listar os bancos de dados

`show dbs`

Para criar um banco ou trocar de banco de dados

`use nome-banco`

Para obter informações sobre as coleções presentes no banco

`db.getCollectionInfos()`

Para retornar um array com os nomes das *collections*:

`db.getCollectionNames()`

Para criar ou acessar uma collection basta usar o comando db.nome_colecao

O exemplo abaixo cria um banco, uma coleção e insere um document dentro. Em seguida pede para listar todos os documents da coleção.

use novoBanco
db.novaColecao.insertOne({nome: "Jeann"})
db.novaColecao.find()

mongoimport <arquivo> -d <database> -c <collection>
mongoexport -c <collection> -d <database> -o <output>
mongodump -d <banco> -o <diretorio>
mongorestore <diretorio>

use novoBanco
db.novaColecao.insertOne({nome: "Jeann", idade: 40})
db.novaColecao.find()
mongodump -d novoBanco -o novobancodir
db.dropDatabase()
mongorestore novobancodir

InsertMany

db.collection.insertMany([{conteudo},{conteudo},{conteudo}])

Write Concern

db.mercado.insertMany([{},{},{}],{w: "majority", wtimeout: 200})

Update
db.books.updateOne({_id:314}, {$set: {pageCount: 1000}})
db.books.updateMany({pageCount: {$gt: 500}},{$set: {bestseller: true}})
db.books.updateMany({pageCount: {$gt: 500}, categories: "Java"},{$push: {categories: "Many Pages"}})

Trocar todo o conteudo (replace)
db.books.replaceOne({_id: 120},{foi: "substituido"})

Atualizando um array
db.books.updateOne({_id: 201},{$push: {categories: "PHP"}})

Atualizando todos
db.books.updateMany({},{$set: {atualizando: true}})

Delete
db.books.deleteOne({_id:314})
db.books.deleteMany({categories: "Java"})
deleteMany com o filtro vazia vai deixar a collection vazia

Tipo de dados
const matheus = db.strings.findOne({nome: "Matheus"})
typeof matheus.nome (string)
typeof matheus (object)

Data
db.datas.insertOne({nome: "Matheus", created_at: new Date()})

Number
No mongo todos os números são classificados como double
db.number.insertOne({double: 12.2, outro_double: 50, inteiro: NumberInt("5")})

Operadores
$eq
db.restaurants.findOne({rating:{$eq:5}})
$gt e $gte
db.restaurants.find({type_of_food: "Breakfast", rating: {$gte: 3}})
$lt e $lte
$in
db.restaurants.find({type_of_food: {$in: ["Pizza","Chinese"]}})
$ne (not equal)
db.restaurants.find({rating: {$ne: 3}})
$exists
db.restaurants.find({bad_restaurant: {$exists: true}})
$text
db.restaurants.find({$text: {$search: "pizza"}})
É preciso criar um indice encima do campo que será usado para busca
db.restaurants.createIndex({name: "text"})

Consultando dentro de array
db.alunos.find({quimica: {$all: [10]}})   --se dentro do array tem alguma nota 10

db.alunos.find({quimica: {$size: 2}})     --retorna apenas os documentos com array de tamanho 2

operador $inc
O operador $inc pode acrescentar ou diminuir uma quantidade especificada a um valor
db.blog.updateOne({author: "Matheus Battisti"}, {$inc: {postCount: 2}})

operador $min
O operador $min atualiza um valor, caso o especificado do operador seja menor que o do registro
db.blog.updateOne({author: "Maicon Santos"}, {$min: {postCount: 0, likesReceived: 0}})

operador $max
O operador $max atualiza um valor, caso o especificado do operador seja maior que o do registro
db.blog.updateOne({author: "Maicon Santos"}, {$max: {postCount: 250}})

operador $mul
O operador $mul multiplica o valor de um campo pelo especificado
db.blog.updateOne({author: "Maicon Santos"}, {$mul: {postCount: 2}})

operador $rename
O operador $rename renomeia um campo, por outro nome que definimos
db.blog.updateMany({}, {$rename: { author: "author_fullname"}})

operador $unset
tem como objetivo remover um campo de um item
db.blog.updateMany({},{$unset:{active: ""}})

operador $addToSet
adiciona um ou mais valores em arrays, apenas se eles já não estiverem lá, ou seja, não dulica elementos
db.blog.updateOne({author: "Matheus"},{$addToSet: {categories: {$each: ["PHP","Vue"]}}})

operador $pop
remove o último ou o primeiro elemento de um array
para remover o primeiro utilize -1, para remover o ultimo utilize 1
db.blog.updateOne({author: "Matheus"}, {$pop: {categories: -1}})

Operador $push
adiciona um ou mais valores a um array, mas duplica os valores caso já existam
db.blog.updateOne({author: "Matheus"}, {$push: {categories: "Linux"}})

Operador $pullAll
para remover vários itens de um array utilizando o $pullAll
db.blog.updateOne({author: "Matheus"}, {$pullAll: {categories: ["Linux", "Docker"]}})

Criação de indices
db.inspections.createIndex({certificate_number: 1})

Criação de indices em embedded documents
db.inspections.createIndex({"address.city": 1})

Verificando indices de uma collection
db.inspections.getIndexes()

Para remover um indice
db.inspections.dropIndex({certificate_number: 1})

Para remover todos os indice
db.inspections.dropIndexes()

Agregadores
$bucket
use bookCollection
db.books.aggregate([
{
 $bucket: {
  groupBy: "$pageCount",
  boundaries: [100,200,300,400,500,600,700],
  default: "OTHERS",
  output: {
   "count": {$sum:1}
  }
 }
}
])

using MongoDB.Bson;
using MongoDB.Driver;

new BsonArray
{
    new BsonDocument("$match",
    new BsonDocument("authors", "Gavin King")),
    new BsonDocument("$sort",
    new BsonDocument("pageCount", -1)),
    new BsonDocument("$limit", 3),
    new BsonDocument("$project",
    new BsonDocument
        {
            { "title", 1 },
            { "pageCount", 1 }
        })
}
