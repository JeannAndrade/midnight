Instalação no Linux -> <https://docs.mongodb.com/manual/administration/install-on-linux/>

<https://docs.microsoft.com/pt-br/windows/wsl/tutorials/wsl-database#install-mongodb>

**********************************************************
***********  Iniciar o serviço   *************************
**********************************************************

sudo service mongodb start --> Você deverá ver uma resposta [OK].
sudo service mongodb status  --> Você deverá ver uma resposta [Falha] se nenhum banco de dados estiver em execução.
sudo service mongodb stop --> para interromper a execução do banco de dados.

**********************************************************
***********     Conceitos        *************************
**********************************************************

No mongoDb não existe o conceito de tabela, o que se guarda são collections

Relacionamento entre Collections
 One to Many
 Many to Many
 One to One
 Subdocuments

Mongoose - um ODM, ou seja um framework para se trabalhar com o MongoDb de uma forma mais simplista

Na minha máquina o MongoDb já foi instalado, o passo a passo está no arquivo de configuração do ambiente de desenvolvimento
Para testar não para o terminal. Utilize o aplicativo MongoDb Compass que foi instalado junto com a aplicação.
No próprio aplicativo já existe um MongoSh, que é o shell para o mongo. se quiser ver funcionando rode o seguinte comando

Para listar os bancos de dados
show dbs

Para trocar de banco de dados
use nome-banco

Para obter informações sobre as coleções presentes no banco
db.getCollectionInfos() para uma listagem mais detalhada
db.getCollectionNames() para um array com os nome

use novoBanco
db.novaColecao.insertOne({nome: "Jeann"})
db.novaColecao.find()
mongoimport <arquivo> -d <database> -c <collection>
mongoexport -c <collection> -d <database> -o <output>
mongodump -d <banco> -o <diretorio>
mongorestore <diretorio>

use novoBanco
db.novaColecao.insertOne({nome: "Jeann"})
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
