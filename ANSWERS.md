

ANSWERS:

1. Create a collection named orders.

    db.createCollection('orders')

2. Insert at least 3 documents that represent an order. IMPORTANT: See section below for fields.

    db.getCollection('orders').insert({ orderDate: '2017-03-14', orderTotal: 10, lineItems: [{unitPrice:10.00}, {quantity:2}, {productName:"Bacon"}]});

    db.getCollection('orders').insert({ orderDate: '2017-02-14', orderTotal: 20, lineItems: [{unitPrice:1.00}, {quantity:3}, {productName:"Steak"}]});

    db.getCollection('orders').insert({ orderDate: '2017-01-14', orderTotal: 100, lineItems: [{unitPrice:5.00}, {quantity:4}, {productName:"Chicken"}]});

3. Find a single order document, any order document.

    db.getCollection('orders').find({orderTotal: '1'})

4. Find all orders and make them look pretty.

    db.getCollection('orders').find().pretty()

5. Find all orders with an orderDate that is prior to 1/1/2016.

    db.getCollection('orders').find({'orderDate':{$lt: '2016-1-1'}})

6. Find all orders with an orderDate that is after 1/1/2016.

    db.getCollection('orders').find({'orderDate':{$gt: '2016-1-1'}})

7. Find orders with lineItems that have a quantity that is less than 50, but greater than 5. HINT: Look at $and and dot notation.

    db.getCollection('orders').find({$and : [{"lineItems.quantity": {$lt: 50}, "lineItems.quantity": {$gt: 5}}]})

8. Update one of your line items to 42.99. HINT: Look at dot notation

    db.getCollection('orders').update({orderTotal: 100}, {$set: {'lineItems.1.unitPrice': 42.99}})

9. Remove one of your orders.

    db.getCollection('orders').remove({_id: ObjectId("58c81ac09edf65e47958446e")})
