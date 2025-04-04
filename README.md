# LearningMongoDB


---

### ✨ Hi, I'm Kevin!

I'm currently learning **MongoDB** to use in my future projects and unlock their full potential.\
I started exploring NoSQL databases because I realized that traditional **SQL databases** may not be ideal for certain types of projects I have in mind.

I mean that as an app or product grows — possibly reaching millions of users — a relational database like **SQL** might face scalability issues.

Although I can still build many of my ideas using **PostgreSQL**, for platforms like **social media** or **e-commerce apps**, it's often better to use a **NoSQL database** because they tend to be more scalable and flexible in handling unstructured data.

That being said, in this repository, I’ll also be creating a **full API using PostgreSQL**, since it’s still a powerful and reliable choice for many other kinds of applications.

---

### 🧠 What I'm learning now:

- Advanced MongoDB features (Aggregation, Indexing, etc.)

---

### 💡 Future goals:

- Build scalable backend systems
- Learn GraphQL
- Deploy full-stack apps

---

### 🌐 Follow my journey:

If you're interested in seeing how my projects evolve, feel free to check out my repositories and leave a star ⭐ if something catches your eye!

---

🚀 Let's Connect or Collaborate!

I'm always open to learning new things and improving my skills. If you have useful resources, suggestions, or even project ideas that could help me grow as a developer — feel free to share them!

If you're working on something exciting or have a product idea in mind, I'd love to hear about it. Maybe we can build something great together.

For example, it could be a startup idea, a community tool, or even just a fun app. I'm eager to collaborate and bring ideas to life! 👀


--- 

### 📚 How I Started Learning MongoDB

I began learning MongoDB by watching a YouTube video and reading through a helpful page that summarizes key concepts quickly:

```bash
🌐 Page: https://learnxinyminutes.com/mongodb/
▶️ YouTube: https://www.youtube.com/watch?v=c2M-rlkkT5o
```

To get started, I installed `mongosh` on my Arch Linux system using the following command:

```bash
yay -Sy mongodb-bin
```

Once installed, you can connect to MongoDB with:

```bash
mongosh
```

At this point, I encountered a common issue — MongoDB wasn't running yet. To fix this, you need to start the MongoDB service with the following commands:

```bash
sudo systemctl status mongodb
sudo systemctl enable mongodb
sudo systemctl start mongodb
```

Now MongoDB is up and running and ready to use! 🚀

---

### 🧠 Some Important Concepts Before Getting Started

- A **collection** is a group of documents.
- A **database** is a group of collections.

> In MongoDB, documents are stored in collections, and collections belong to databases.  
This is the basic structure you'll work with when using MongoDB.

---

### 🧪 Basic MongoDB Shell Commands

Here are some fundamental MongoDB shell commands I’ve learned so far:

#### 📂 Viewing and Selecting Databases

```bash
show dbs            # Lists all databases
use <database>      # Switches to the specified database (creates it if it doesn't exist)
```

If you use a database that doesn't exist yet, MongoDB will *prepare* to create it. However, the database is only actually created when you insert data (like a collection or document).

**Example:**

```bash
use school                  # 'school' doesn't exist yet
db.createCollection("students")   # Creates a collection within the 'school' database
```

This effectively creates a new database called `school`.

#### 🗑️ Dropping a Database

To delete the current database:

```bash
db.dropDatabase()
```

---

### 📝 Inserting Documents

Now, let’s see how to insert documents into a MongoDB database.

**Single document:**

```bash
use school
db.students.insertOne({ name: "Spongebob", age: 30, gpa: 3.2 })
```

> If the `students` collection doesn't exist, MongoDB will automatically create it.

**Multiple documents:**

```bash
db.students.insertMany([
  { name: "Patrick", age: 38, gpa: 1.5 },
  { name: "Sandy", age: 27, gpa: 4.0 },
  { name: "Gary", age: 18, gpa: 2.5 }
])
```

---

### 🔍 Retrieving Documents

To return all documents in a collection:

```bash
db.students.find()
```
---

### 🧬 MongoDB Data Types

Now let's learn about some common **data types** in MongoDB documents. These include:

- `String` – Text data
- `Integer` – Whole numbers
- `Double` – Numbers with decimals
- `Boolean` – `true` or `false`
- `Date` – Date and time values
- `Null` – Represents a null or missing value
- `Array` – A list of values
- `Object` – Embedded documents (objects inside objects)

In MongoDB, we can also nest(anidar) documents or use arrays to represent more complex data structures.

**Example: Inserting a document with various data types:**

```bash
db.students.insertOne({
  name: "Larry",
  age: 32,
  gpa: 2.8,
  fullTime: false,
  registerDate: new Date(),
  graduationDate: null,
  courses: ["Biology", "Chemistry", "Calculus"],
  address: {
    street: "123 Fake St.",
    city: "Bikini Bottom",
    zip: 12345
  }
})
```

In this example:
- `registerDate` uses JavaScript's `Date()` object to store the current date.
- `courses` is an array of strings.
- `address` is a nested object (embedded(incorporado) document).

---

### 📊 Sorting and Limiting Documents

To **sort documents**, we use the `.sort()` method:

```bash
db.students.find().sort({ name: 1 })   # 1 for ascending (A-Z), -1 for descending (Z-A)
db.students.find().sort({ gpa: 1 })    # Sort by GPA in ascending order
```

To **limit** the number of documents returned:

```bash
db.students.find().limit(10)           # Returns only the first 10 documents
```

You can **combine sorting and limiting**:

```bash
db.students.find().sort({ gpa: -1 }).limit(1)   # Returns the student with the highest GPA
```

---

### 🔎 The `.find()` Method

The `.find()` method allows you to query documents and control which fields to return using **projection**.
`.find({query}, {projection})`

```bash
db.students.find({ name: "Spongebob" }, { _id: false, name: true })
```

In this example:
- The **query** is `{ name: "Spongebob" }`
- The **projection** is `{ _id: false, name: true }`, which returns only the `name` field and hides the `_id`

> Projections let you customize your output — useful for showing only what you need!

---

### 🔧 Updating Documents

To update documents in MongoDB, you can use the `.updateOne()` or `.updateMany()` methods.

#### 🛠️ Syntax

```bash
db.collection.updateOne(filter, update)
db.collection.updateMany(filter, update)
```

#### 🔄 Common Update Operators

- `$set`: Updates or adds a value to a field.
- `$unset`: Removes a field from the document.
- `$exists`: Checks if a field exists (used in queries, not updates).

#### 💡 Examples

```bash
# Set 'fullTime' to true for the student named "Larry"
db.students.updateOne({ name: "Larry" }, { $set: { fullTime: true } })

# Set 'fullTime' to false for all students
db.students.updateMany({}, { $set: { fullTime: false } })

# Set 'fullTime' to true, but only if the field already exists
db.students.updateMany(
  { fullTime: { $exists: true } },
  { $set: { fullTime: true } }
)
```

#### ❌ Remove a field

```bash
db.students.updateOne(
  { name: "Larry" },
  { $unset: { fullTime: "" } }
)
```


### 🗑️ Deleting Documents

Deleting documents in MongoDB is straightforward, similar to updating.

#### 💥 Basic Deletion Methods

```bash
db.students.deleteOne({ name: "Larry" })      # Deletes the first match
db.students.deleteMany({ fullTime: false })   # Deletes all students where 'fullTime' is false
```

#### 🔍 Conditional Deletion with `$exists`

You can also delete documents that are missing certain fields:

```bash
db.students.deleteMany({ registerDate: { $exists: false } })
```

This removes all documents that don't have a `registerDate` field.

---

### 📘 MongoDB Comparison Query Operators

Comparison operators in MongoDB allow you to filter documents based on specific value comparisons. Here’s a quick rundown with examples:

---

### 🔹 `$ne` – Not Equal

Returns documents where the value of the field is **not equal** to the specified value.

```bash
db.students.find({ name: { $ne: "Spongebob" } })
```

**Output:**
```bash
[
  {
    _id: ObjectId('67eea94cb2b50e38206b140c'),
    name: 'Kevin',
    gpa: 5,
    fullTime: true
  },
  {
    _id: ObjectId('67eeaa01b2b50e38206b140d'),
    name: 'Patrick',
    gpa: 2.3,
    fullTime: true
  },
  {
    _id: ObjectId('67eeaa01b2b50e38206b140e'),
    name: 'Larry',
    gpa: 5,
    fullTime: true
  }
]
```

---

### 🔹 `$lt`, `$lte`, `$gt`, `$gte` – Less Than / Greater Than

Used to compare numerical (or date) values:

```bash
db.students.find({ age: { $lt: 20 } })   # Less than 20
db.students.find({ age: { $lte: 20 } })  # Less than or equal to 20
db.students.find({ age: { $gt: 20 } })   # Greater than 20
db.students.find({ age: { $gte: 20 } })  # Greater than or equal to 20
```

**Example: Range query using `$gte` and `$lte`:**
```bash
db.students.find({ gpa: { $gte: 3, $lte: 4 } })  # GPA between 3 and 4
```

---

### 🔹 `$in` and `$nin` – Match Specific Values

These operators match if the field’s value is **in** or **not in** a list of specified values.

```bash
db.students.find({ name: { $in: ["Spongebob", "Larry"] } })
```

This will return students whose names are either *Spongebob* or *Larry*.

```bash
db.students.find({ name: { $nin: ["Kevin", "Patrick"] } })
```

This returns students whose names are **not** *Kevin* or *Patrick*.

---


### 🧠 Logical Query Operators

Logical operators in MongoDB allow you to combine or modify query conditions using logical expressions. These return documents based on whether certain **conditions are true or false**.

---

### 🔹 `$and` – Logical AND

Returns documents that **match all** the specified conditions.

```bash
db.students.find({
  $and: [
    { fullTime: true },
    { age: { $lte: 20 } }
  ]
})
```

This finds students who are **full-time** _and_ **20 or younger**.

---

### 🔹 `$or` – Logical OR

Returns documents that **match at least one** of the specified conditions.

```bash
db.students.find({
  $or: [
    { fullTime: false },
    { age: { $lte: 20 } }
  ]
})
```

This finds students who are either **not full-time** _or_ **20 or younger**.

---

### 🔹 `$nor` – Logical NOR

Returns documents that **fail to match all** the specified conditions.

```bash
db.students.find({
  $nor: [
    { fullTime: false },
    { age: { $lte: 20 } }
  ]
})
```

This finds students who are **full-time** _and_ **older than 20** (i.e., not matching either condition).

---

### 🔹 `$not` – Logical NOT

**Inverts** the effect of a query expression. Returns documents that **do not** match the condition.

```bash
db.students.find({
  age: { $not: { $gte: 30 } }
})
```

This finds students whose age is **not greater than or equal to 30**.

---

### 📌 Indexes

Indexes support the efficient execution of queries in MongoDB.  
Without indexes, MongoDB must perform a **collection scan**, meaning it checks every document in the collection to find matches for a query.  
If an appropriate index exists, MongoDB can use it to quickly locate the relevant documents, improving performance significantly.

#### 🔍 Check how a query is executed:

```bash
db.students.find({ name: "Larry" }).explain("executionStats")
```

#### ⚙️ Create an index on a field:

```bash
db.students.createIndex({ name: 1 })   # 1 for ascending, -1 for descending
```

#### 📃 List all indexes:

```bash
db.students.getIndexes()
```

#### ❌ Drop an index:

```bash
db.students.dropIndex("name_1")
```

> Indexes speed up read operations, but they use more memory and may slow down inserts, updates, and deletes because the **B-tree** structure must be updated each time.

📌 **Tip:** Indexes are great when your app reads a lot of data, but be careful when doing frequent updates or deletions.

---

### 📁 Collections

To view all collections in the current database:

```bash
show collections
```

You can also pass options when creating a collection:

```bash
db.createCollection("teachers", {
  capped: true,
  size: 1000 * 1024,   # 10 MB max size
  max: 100             # Max 100 documents
})
```

> `capped: true` means it's a fixed-size collection that behaves like a circular buffer.

To delete a collection:

```bash
db.courses.drop()
```

---

### ✅ Wrapping Up

At this point, I’ve completed this MongoDB learning path.  
Now I’m going to **start implementing everything I’ve learned** in real projects to reinforce my knowledge and build cool things! 🚀
