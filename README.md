# MongoDB-Notes 
what is mongoDB? 
it is a database that is used to store data whether in website or blog or blog site but 
what is the type of the mongo db and what makes it different from the other databases. 
it is commonly known as nosql database meaning that we do not use sql commands to interact 
with it. but are they so different from the sql databases? the sql database or the 
relational database is composed of tables with rows and coloumns where each table is used 
to store a specific data type like users or blog posts, and each row is a user record or 
blog post record or records for some data types stored in the table. each coloumn is a 
property on that particular record like email, name, id etc. different tables can be related 
to each other as for example one author might have many books (one to many relationship).

In order to query all records from the authors table we use: (astric means all)
# SELECT*FROM authors

Mongodb is very different from a sql database because instead of using tables of coloumns 
rows, we use collections and documents. each collection of nosql database would store a 
specific data type of data record like users athors or books or blog posts. these 
collections are called doucment. it can have a lot of benefits since it can be much easier 
just because their structure is more like json or javascript objects. It allows to store 
nested documents within a document. a document in the books collection could have another 
document inside it called author having properties as well eg name, age. This can be an 
alternative to use two tables in sql database, to store these two data types seperately
, we can store them in 2 different documents here as well do not get the wrong idea but 
usually it is better to just put them in one collection, letting it be more flexible. it has 
really good speed and responsive, it makes it easy for people who are familiar with java-
script so they can edit easily since they do not have to know much prior knowledge. 

28 tai tze soon 8536
the link to download mongoDB: 
https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqblVwS0xPTFBHWUdZLXBGWXZGQTQyZjExQS1HZ3xBQ3Jtc0tueEhmS2l0emh4SmpNNVllMnRxcnBJVGJ2X0owWXBoZVgydVlNWE02WXcyQUdKOTR3WkViaW1VRFRfUnhRckRha01YRTNPS2JZbE1fbGducTNQeVotZDlhaE00V0RTd0w2Z0I2d1J1dnB3UGY5d1RSUQ&q=https%3A%2F%2Fwww.mongodb.com%2Ftry%2Fdownload%2Fcommunity&v=gDOKSgqM-bQ

- collections and documents: 
mongodb stores data insides collection and database could have as many collections as we like
for many types of data let it be comments blog posts or Users. user collection stores the 
user data or the user documents, blog posts collection which stores blog posts. comment 
collection would store comment documents. it is set up like that so that we can categorize 
and get all related documents of the a certain collection. documents themselves represents 
the individual records in a specific collection. it can encompass a title, which have a 
string value, tags which can have an array, up votes which can be an integer. we would also 
have id property to uniquely identify a certain value, it is a special ID type in mongoDB.
Every document could be identified by this unique ID value, you can query to fetch that 
unique ID. It could have nested documents. 

-using mongodb compass: 
connection string is a special mongodb url, using an online mongodb service can copy the 
link and work with it in the application. just click on connect, connecting to mongodb 
service, make sure the services are working on the windows. there are built in databases in 
the app. create a new data base, we create new collections as well, add data. 
do not forget to add square brackets and commas when you wan to add multiple documents
{ rating: 9}

-using mongodbShell: 
we can use the terminal of the application itself or the window, it is mentioned in there 
that there is test> , it says that we are currently at database test but we want the 
directory to be in a different database. even if the directory does not exist we can 
switch to it and add collections and it will declare it 
# mongosh
# show dbs
# use bookstore
# use test (does not exist)
# use mydb (does not exist)
# cls
# db
# show collections

# var name= "adam"
# name

# name = "ahmed"
# name

# help
# exit


- Adding new documents through shell: 
adding from the shell will go as follows:(we can add another collection who does not exist)
# use bookstore
# db.books
# db.books.insertOne({Title: "the color of magic", Author:"terry pratchett", Pages:300, rating: 7, Genres: ["fantasy","magic"]})

# db.authors.insertOne({name:"brandon", age: 30})
# db.books.insertMany([{title: "the light fanstastic", author:"terry man", pages:78, rating:5, genres: ["fantasy"]}, {title: "the light of adam", author:"ssf df", pages:48, rating:4, genres: ["magic"]}])


-finding a document:
a lot of time we want to fetch documents from different places, in box collection:

# db.stories.find()  (show all the documents, it will first print 20 documents)
# cls
# db.stories.find({author: "patrick robertson"})
# db.stories.find({author: "patrick robertson", rating: 8})
# cls
# 
specifying which field we want
# db.books.find({author: "patrick robertson"}, {title: 1, author:1})
# 
# db.books.find({}, {title: 1, author:1})
finding only one record
# db.books.findOne({_id: ObjectId("63ab51eced4a65114df7a0c3")})


-sorting and limiting data: 
# db.stories.find().count()
# db.books.find({author: "patrick robertson"}).count()
# db.books.find().limit(3)
# db.books.find().limit(3).count()
# db.books.find().sort({title: 1}) (should be 1 or -1 referring to ascending or descending order)
# db.books.find().sort({title: -1}) (alphabetically from z-a)
# db.books.find().sort({title: -1}).limit(3)

-Nested documents: 
Properties can contain other values or other properties stored inside with values, we can 
say it is an array of documents. EG, reviews for the book? 

# db.books.insertOne({title: "the color of magic", author:"terry pratchett", pages:300, rating: 7, genres: ["fantasy","magic"], reviews: [{name: "youshi", body: "great book!!"}, {name: "mario", body: "so so"}]})
# db.books.insertMany([{title: "Lord of the kings", author:"adam", pages:300, rating: 10, genres: ["fantasy"], reviews: [{name: "Ahmed", body: "nice book!!"}, {name: "faris", body: "not that good"}]}, {title: "madness", author:"Shakespear", pages:200, rating: 4, genres: ["magic"], reviews: [{name: "Dji", body: "just wow"}, {name: "Anas", body: "wasn't really good"}]}])


- Operation and complex queries: (specific operator to do greater than for example )
# db.books.find({rating: {$gt: 4}})
# db.books.find({rating: {$gt: 7}})
# db.books.find({rating: {$lt: 7}})
# db.books.find({rating: {$gte: 7}})
# db.books.find({rating: {$gte: 7}, author:"adam"})

OR sign
# db.books.find({$or:[{rating: 7}, {rating: 10}]})
# db.books.find({$or:[{rating: 7}, {author: "Shakespear"}]})
# 

-quering arrays:
# db.books.find({ rating: {$in: [7,8,10]}})
# db.books.find({$or: [{rating: 7}, {rating: 8}, {rating: 10}]})
# db.books.find({ rating: {$nin: [7,8,10]}})

# db.books.find({genres: "magic"})
# db.books.find({genres: "fantasy"})
# db.books.find({genres: ["magic"]}) (we just have to add square bracket to specify it)
# db.books.find({genres: ["fantasy", "magic"]})

all items are in the list: (while there are other genres other than these 2 genres)
# db.books.find({genres: {$all: ["fantasy", "magic"]}})

review by Dji:
# db.books.find({"reviews.name":"Dji"})

-deleting documents:(export data, import later)
# db.books.find()
# db.books.deleteOne({_id: ObjectId("63ab661f9678c56c65bbc520")})
# db.books.find()
# db.books.deleteMany({author: "Shakespear"})  (going to delete every shakespear book)


-updating fields: 
# db.books.updateOne({_id: ObjectId("4684351dfd8z3d5fs81e8")},  {$set: {rating:8, pages:360 }})
