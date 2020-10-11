# MongoDB

Difference between SQL and NoSQL

SQL
1) rdbms engines - mySQL, postgresSQL, microsoft sql server, oracle, IBM DB
2) implemented using tables
3) most suitable to perform flexible queries, to enforce field constraints, perform relational queries amng the tables


NoSQL
1) built for the sake of high performance
2) MongoDB, Cassandra
3) implemented using tables, documents, graph(key: value pairs)
4) Mongodb - faster and for large data.

SETUP
1) create a cluster
2) give network access(0.0.0.0 means access your db from anywhere)
3) give database access - admin 
4) connect your cluster to command shell
C:\Program Files\MongoDB\Server\4.4\bin>mongo "mongodb+srv://cluster0.my9kz.mongodb.net/test" --username <username> --password <password>

MongoDB learnings

1) use db - to create a database
2) db.createCollection("Ranjitha")
3) show dbs - shows the db's created in a cluster
4) Insert data - data types - string, date, integer, list, object
db.favorites.insert({title: 'Emily', company: 'Savior', favfood: 'cheeseburger', IGfollowers: '10', friends: ['camille', 'gabrielle', 'mindy'], partner : {name: 'gabrielle', age:'27'}, date: Date() })

5) Insert multiple in one query

db.favorites.insertMany([
{title: 'Emily', company: 'Savior', IGfollowers: '10', friends: ['camille', 'gabrielle', 'mindy'], partner : {name: 'gabrielle', age:'27'}, date: Date() }, 
{title: 'Gabrielle', company: 'cafe'},
{title: 'Mindy', company: 'Nanny'}
])

6) to view the documents / objects
db.favorites.find()
db.favorites.find().pretty()

7) synonym of where clause
db.favorites.find({title: 'Gabrielle'}).pretty()

8) sort
db.favorites.find().sort({title: 1}).pretty()

9) count()
limit()

10) forEach(function(doc) {print('Blog post' + doc.title)})

11) update - replaces everything
db.favorites.update({title:'Emily'}, 
{title: 'Sylvie', company: 'Savior'})

partial updating with set$
db.favorites.update({title:'Emily'},
{
   $set: {
	company: 'chicago office'
	}
} )

12) delete
db.favorites.remove({title: 'Mindy'})

13) sub documents 
In RDB you would have forgein key point to another table, but on Mongo you can avoid using multiple tables
avoiding joins

db.favorites.update({title:'Emily'},
{
   $set: {
    subtable: [
    {
    	prevcity: 'Chicago',
    	newcity: 'Paris'
    },
    {
    	prevcity: 'Normandy',
    	newcity: 'Paris'
    }
    ]
    }
} )

db.favorites.update({title:'Sylvie'},
{
   $set: {
    subtable: [
    {
    	prevcity: 'China',
    	newcity: 'Paris'
    }
    ]
    }
} )

14) retrieve all data entries that has "paris" as newcity
db.favorites.find({ subtable: { $elemMatch: { newcity: 'Paris' } } }).pretty()

15)  using greater than(gt), gte, lt, lte
db.favorites.update({title:'Sylvie'},
{
   $set: {
	IGfollowers: 19
	}
} )

db.favorites.find({IGfollowers: {$gt: 15} })


