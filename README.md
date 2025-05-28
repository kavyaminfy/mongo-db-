# mongo-db-

crosoft Windows [Version 10.0.26100.4061]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Minfy.DESKTOP-81ME0ME>mongosh
Current Mongosh Log ID: 6836e4550bc6c7c23a6c4bcf
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.5.1
Using MongoDB:          8.0.9
Using Mongosh:          2.5.1

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/


To help improve our products, anonymous usage data is collected and sent to MongoDB periodically (https://www.mongodb.com/legal/privacy-policy).
You can opt-out by running the disableTelemetry() command.

------
   The server generated these startup warnings when booting
   2025-05-28T15:46:42.080+05:30: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
------

test> db.tasks.insertMany([
...   { task: "Buy groceries", status: "pending" },
...   { task: "Complete assignment", status: "pending" },
...   { task: "Call mom", status: "done" }
... ])
...
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6836e4fa0bc6c7c23a6c4bd0'),
    '1': ObjectId('6836e4fa0bc6c7c23a6c4bd1'),
    '2': ObjectId('6836e4fa0bc6c7c23a6c4bd2')
  }
}
test> use todoApp
switched to db todoApp
todoApp> db.createCollection("tasks")
{ ok: 1 }
todoApp> db.tasks.insertMany([
...   { task: "Buy groceries", status: "pending" },
...   { task: "Complete assignment", status: "pending" },
...   { task: "Call mom", status: "done" }
... ])
...
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    '1': ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    '2': ObjectId('6836e51b0bc6c7c23a6c4bd5')
  }
}
todoApp> db.tasks.find().pretty()
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: 'pending'
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: 'pending'
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd5'),
    task: 'Call mom',
    status: 'done'
  }
]
todoApp> db.tasks.find({ status: "pending" }).pretty()
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: 'pending'
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: 'pending'
  }
]
todoApp> db.tasks.updateOne(
...   { task: "Buy groceries" },
...   { $set: { status: "done" } }
... )
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
todoApp> db.tasks.deleteOne({ task: "Call mom" })
{ acknowledged: true, deletedCount: 1 }
todoApp> db.tasks.insertOne({
...   task: "Pay electricity bill",
...   status: "pending",
...   due: new Date("2025-06-01"),
...   priority: "high"
... })
...
{
  acknowledged: true,
  insertedId: ObjectId('6836e5660bc6c7c23a6c4bd6')
}
todoApp> db.tasks.find().sort({ priority: 1 }) // or use { due: 1 }
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: 'done'
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: 'pending'
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: 'pending',
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high'
  }
]
todoApp> db.tasks.find().sort({ priority: 1 }) // or use { due: 1 }db.tasks.find().sort({ priority: 1 }) // or use { due: 1 }
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: 'done'
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: 'pending'
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: 'pending',
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high'
  }
]
todoApp>

todoApp> b
ReferenceError: b is not defined
todoApp> todoApp> db.tasks.find({ status: "true" }).pretty()
ReferenceError: todoApp is not defined
todoApp> db.tasks.updateOne(
...   { task: "Buy groceries" },         // Filter
...   { $set: { status: true } }         // Update
... )
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
todoApp> db.tasks.updateMany(
...   { status: "pending" },
...   { $set: { status: true } }
... )
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}
todoApp> db.tasks.find().pretty()
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: true
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: true
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: true,
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high'
  }
]
todoApp> db.task{
...   _id: ObjectId("..."),
...   name: "Kavya Sharma",
...   email: "kavya@example.com",
...   role: "developer" // or "admin", "manager"
... }
... fdkd
Uncaught:
SyntaxError: Missing semicolon. (1:7)

> 1 | db.task{
    |        ^
  2 |   _id: ObjectId("..."),
  3 |   name: "Kavya Sharma",
  4 |   email: "kavya@example.com",

todoApp> db.tasks.insertOne({
...   task: "Prepare for DevOps exam",
...   status: false,          // false = not done, true = done
...   createdAt: new Date()
... })
...
{
  acknowledged: true,
  insertedId: ObjectId('6836ed4b0bc6c7c23a6c4bd7')
}
todoApp> {
...   acknowledged: true,
...   insertedId: ObjectId("6655e9f8e57a4b0f4e9f4567")
... }
...
... db.tasks.insertMany([
...   { task: "Buy milk", status: false, createdAt: new Date() },
...   { task: "Submit assignment", status: false, createdAt: new Date() },
...   { task: "Water the plants", status: true, createdAt: new Date() }
... ])
...
Uncaught:
SyntaxError: Missing semicolon. (3:12)

  1 | {
  2 |   acknowledged: true,
> 3 |   insertedId: ObjectId("6655e9f8e57a4b0f4e9f4567")
    |             ^
  4 | }
  5 |
  6 | db.tasks.insertMany([

todoApp> db.tasks.insertMany([
...   { task: "Buy milk", status: false, createdAt: new Date() },
...   { task: "Submit assignment", status: false, createdAt: new Date() },
...   { task: "Water the plants", status: true, createdAt: new Date() }
... ])
...
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6836ed5a0bc6c7c23a6c4bd8'),
    '1': ObjectId('6836ed5a0bc6c7c23a6c4bd9'),
    '2': ObjectId('6836ed5a0bc6c7c23a6c4bda')
  }
}
todoApp> db.tasks.find().pretty()
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: true
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: true
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: true,
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high'
  },
  {
    _id: ObjectId('6836ed4b0bc6c7c23a6c4bd7'),
    task: 'Prepare for DevOps exam',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:35.966Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd8'),
    task: 'Buy milk',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd9'),
    task: 'Submit assignment',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bda'),
    task: 'Water the plants',
    status: true,
    createdAt: ISODate('2025-05-28T11:02:50.576Z')
  }
]
todoApp>

todoApp> db.tasks.updateOne(
...   { task: "Buy milk" },                      // Filter
...   { $set: { updatedAt: new Date() } }        // Update
... )
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
todoApp> db.tasks.updateMany(
...   {},
...   { $set: { updatedAt: new Date() } }
... )
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 7,
  modifiedCount: 7,
  upsertedCount: 0
}
todoApp>

todoApp> db.tasks.find().pretty()
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: true,
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high',
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836ed4b0bc6c7c23a6c4bd7'),
    task: 'Prepare for DevOps exam',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:35.966Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd8'),
    task: 'Buy milk',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd9'),
    task: 'Submit assignment',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bda'),
    task: 'Water the plants',
    status: true,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  }
]
todoApp> db.tasks.countDocuments()
7
todoApp> db.tasks.find().sort({ createdAt: -1 })
[
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd8'),
    task: 'Buy milk',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd9'),
    task: 'Submit assignment',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bda'),
    task: 'Water the plants',
    status: true,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836ed4b0bc6c7c23a6c4bd7'),
    task: 'Prepare for DevOps exam',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:35.966Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: true,
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high',
    updatedAt: ISODate('2025-05-28T11:07:50.185Z')
  }
]
todoApp> const sevenDaysLater = new Date();
... sevenDaysLater.setDate(sevenDaysLater.getDate() + 7);
...
... db.tasks.updateMany(
...   {},
...   { $set: { dueDate: sevenDaysLater } }
... )
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 7,
  modifiedCount: 7,
  upsertedCount: 0
}
todoApp> db.tasks.find({}, { task: 1, dueDate: 1 }).pretty()
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed4b0bc6c7c23a6c4bd7'),
    task: 'Prepare for DevOps exam',
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd8'),
    task: 'Buy milk',
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd9'),
    task: 'Submit assignment',
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bda'),
    task: 'Water the plants',
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  }
]
todoApp> db.tasks.find({
...   status: false,
...   dueDate: { $lt: new Date() }
... }).pretty()
...

todoApp> db.tasks.find({
...   $or: [
...     { status: true },
...     { dueDate: { $gt: new Date() } }
...   ]
... }).pretty()
...
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: true,
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high',
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed4b0bc6c7c23a6c4bd7'),
    task: 'Prepare for DevOps exam',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:35.966Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd8'),
    task: 'Buy milk',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd9'),
    task: 'Submit assignment',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bda'),
    task: 'Water the plants',
    status: true,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  }
]
todoApp> db.tasks.find({
...   status: false,
...   $or: [
...     { dueDate: { $lt: new Date() } },
...     { task: /urgent/i }   // case-insensitive regex match
...   ]
... }).pretty()
...

todoApp> const twentyMinutesAgo = new Date(Date.now() - 20 * 60 * 1000);
...
... db.tasks.find({
...   createdAt: { $gte: twentyMinutesAgo }
... }).pretty()
...

todoApp> const twentyMinutesAgo = new Date(Date.now() - 20 * 60 * 1000);
...
... db.tasks.find({
...   updatedAt: { $gte: twentyMinutesAgo }
... }).pretty()
...
[
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd3'),
    task: 'Buy groceries',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836e51b0bc6c7c23a6c4bd4'),
    task: 'Complete assignment',
    status: true,
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836e5660bc6c7c23a6c4bd6'),
    task: 'Pay electricity bill',
    status: true,
    due: ISODate('2025-06-01T00:00:00.000Z'),
    priority: 'high',
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed4b0bc6c7c23a6c4bd7'),
    task: 'Prepare for DevOps exam',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:35.966Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd8'),
    task: 'Buy milk',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bd9'),
    task: 'Submit assignment',
    status: false,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  },
  {
    _id: ObjectId('6836ed5a0bc6c7c23a6c4bda'),
    task: 'Water the plants',
    status: true,
    createdAt: ISODate('2025-05-28T11:02:50.576Z'),
    updatedAt: ISODate('2025-05-28T11:07:50.185Z'),
    dueDate: ISODate('2025-06-04T11:20:09.759Z')
  }
]
