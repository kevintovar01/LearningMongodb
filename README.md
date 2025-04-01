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

