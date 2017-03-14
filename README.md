DETAILS FROM WEB-APP:

Assignment DetailsUncompleted:
https://github.com/kdszafranski/prime-mongo-crud-lecture-notes/
In this challenge, we’re going to practice basic Mongo syntax. This should help better solidify some concepts that were covered during lecture.

Assumptions:
You are using the mongo shell or Robomongo
You installed mongo via homebrew
mongod is currently running on your computer
Setup
Follow the instructions below before continuing with this challenge.

Create your database:
We are creating a database to hold a collection with at least 3 documents.

Open mongo shell:
Type use phi to create your database (or use an existing database)
GitHub repo
Create a GitHub repo named “prime-solo-mongo”.
Create a file called “mongo.txt”. You will store your responses to the exercise questions here.
Exercise
For each of the following questions

Write a comment that specifies which question you are answering. Use JavaScript comment syntax.
Write the Mongo query that answers the question, below that comment.
Example question and answer
// 0. Create a collection named joe
db.createCollection('joe')

Tasks:

1. [ ] Create a collection named orders.
2. [ ] Insert at least 3 documents that represent an order. IMPORTANT: See section below for fields.
3. [ ]Find a single order document, any order document.
4. [ ]Find all orders and make them look pretty.
5. [ ]Find all orders with an orderDate that is prior to 1/1/2016.
6. [ ]Find all orders with an orderDate that is after 1/1/2016.
7. [ ]Find orders with lineItems that have a quantity that is less than 50, but greater than 5. HINT: Look at $and and dot notation.
8. [ ]Update one of your line items to 42.99. HINT: Look at dot notation
9. [ ] Remove one of your orders.

order fields:
orderDate -- see https://docs.mongodb.org/manual/reference/method/Date/
orderTotal
lineItems -- an array of line item objects with fields
unitPrice
quantity
productName


--------------------------------------------------




DETAILS FROM REPO:

# Mongo CRUD/Intro Lecture Notes

Open Mongo shell: `mongo`

## Database

Create a new datbase called 'sigma':

`use sigma`

Create a new Collection called 'books':

`db.createCollection('books')`

Create a session variable as a short-hand:

`var books = db.books`

List Collections in current db

`show collections`

## CRUD Syntax

[CRUD Operations Docs](https://docs.mongodb.com/manual/crud/)

## Create (Insert)
```
books.insert({
  title: "Snow Crash",
  author: "Neal Stephenson",
  edition: 1.2
  });
```

See what's in the Collection.

`books.find()`

`books.findOne()` Returns the first Document that matches.

Query criteria needs quotes if the field name has dots in it.

> books.find({title: "Snow Crash"})

> books.find({"ratings.1.score": 999})

**Examples to Insert**

> books.insert({
  title: "A Tale of Two Cities",
  author: "Charles Dickens",
  edition: 2,
  published: new ISODate('1859-5-20')
});

> books.insert({
  title: "Murder on the Orient Express",
  author: "Agatha Christie",
  edition: 2
});

> books.insert({
  title: "Snow Crash",
  author: "Neal Steve",
  edition: 1.2,
  ratings: [
    {score: 5},
    {score: 1}
  ]
});

> books.insert({
  title: "Catcher in the Rye",
  author: "Someone",
  edition: 1,
  ratings: [
    {score: 2},
    {score: 5},
    {score: 3.5},
    {score: 4}
  ]}
);


## Read (Find)
All books in our Collection:

> books.find(); or books.find({})

Make it pretty by chaining .pretty() onto your query.

> books.find().pretty()

Specific:

> books.find({title: "Snow Crash"});

Like Search:

> books.find({title: /Cat/});

`$exists` checks if this Document has a property/field.

> books.find( {ratings: {$exists: true} } )


### [Query Operators](https://docs.mongodb.com/manual/reference/operator/query/)

By Date. Before today:
> books.find({published: {$lt: new Date('2016-11-28')}})

Find based on given edition numbers range

> books.find({'edition':{$lt: 3}, 'edition':{$gt: 1.2} })

#### Partial List

* `$lt`, `$gt` (less-than, greater-than)
* `$lte`, `$gte` (less-,greater-than or equals)
* `$ne` (not equal)
* Implicit AND is used when multiple fields are specified.
* Explicit `$and` possible


## Update
books.update()

> books.update({title:"Catcher in the Rye"}, {$set: author: "J. D. Salinger"});

### [Arrays](https://docs.mongodb.com/v3.2/reference/operator/update-array/)

Push into an existing array on a Document:

> books.update({title: "Catcher in the Rye"}, {$push: {ratings: {score: 4.5}}})

> books.update({title: "Catcher in the Rye"}, {$push: {ratings: {score: 9}}})

**Update a value in an array**

Find It:

> books.find({title: "Catcher in the Rye"})

Update It:

> books.update({title: "Catcher in the Rye"}, {$set: {"ratings.1.score": 999}})


## Delete (Remove)
books.remove({"_id" : ObjectId("583dc0b4482c7736c1d27058")})
583dc0b4482c7736c1d27058
