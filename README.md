# 📚 MongoDB Student Database Project

A practical MongoDB project demonstrating student record management using the MongoDB Shell (`mongosh`). The project covers CRUD operations, comparison and logical query operators, and verification of results on a `students` collection.

---

## 📌 Project Overview

This project demonstrates core NoSQL database operations in MongoDB: inserting, updating, deleting and querying student records. Every operation is documented with the exact command and the output produced in `mongosh`.

## 🗄️ Database Details

| Property | Value |
|---|---|
| Collection | `students` |
| Records inserted | 50 |
| Roll Numbers | 301–350 |
| Records remaining after updates/deletes | 47 |
| Departments | DS, IoT, Cyber, Cloud |
| Database Type | NoSQL (document-oriented) |
| Tool | MongoDB Shell (`mongosh`) |

Department split at the time of insertion: **14 DS, 13 IoT, 12 Cyber, 11 Cloud**.

## 🛠️ Technologies Used

- MongoDB
- MongoDB Shell (`mongosh`)
- MongoDB Query Language
- NoSQL Database

## 📊 Student Record Structure

Each student document contains:

- `rollNo`
- `name`
- `age`
- `department`
- `marks`

Some update operations also add:

- `status`

### Example Document

```js
{
  rollNo: 301,
  name: "Aarohi",
  age: 20,
  department: "DS",
  marks: 72
}
```

---

## 🔄 CRUD Operations

### 1. Insert One

Inserts a single student record (roll number 301).

```js
db.students.insertOne({
  rollNo: 301,
  name: "Aarohi",
  age: 20,
  department: "DS",
  marks: 72
})
```

### 2. Insert Many

Inserts 49 student records, roll numbers 302 to 350, in one operation.

Example (first few documents):

```js
db.students.insertMany([
  { rollNo: 302, name: "Vihaan", age: 19, department: "IoT", marks: 69 },
  { rollNo: 303, name: "Siddharth", age: 22, department: "Cyber", marks: 91 },
  { rollNo: 304, name: "Tanvi", age: 22, department: "Cloud", marks: 92 }
  // ... up to rollNo: 350 (full list in the project report)
])
```

Departments used: **DS, IoT, Cyber, Cloud**

### 3. Update One

Updates the marks of roll number 301 from 72 to 78.

```js
db.students.updateOne(
  { rollNo: 301 },
  { $set: { marks: 78 } }
)
```

### 4. Update Many

Adds `status: "Active"` to all Cyber department students (12 documents modified).

```js
db.students.updateMany(
  { department: "Cyber" },
  { $set: { status: "Active" } }
)
```

### 5. Delete One

Deletes the student with roll number 350.

```js
db.students.deleteOne({ rollNo: 350 })
```

### 6. Delete Many

Deletes students whose marks are less than 40 (roll 317 with 35 marks and roll 338 with 38 marks; `deletedCount: 2`).

```js
db.students.deleteMany({ marks: { $lt: 40 } })
```

After all update and delete operations, **47 documents** remain (50 inserted − 1 − 2 deleted).

---

## 🔎 Query Operations

| Operator | Meaning | Query | Matches |
|---|---|---|---|
| `$gt` | Greater than | `{ marks: { $gt: 80 } }` | 27 |
| `$lt` | Less than | `{ marks: { $lt: 80 } }` | 17 |
| `$eq` | Equal to | `{ marks: { $eq: 85 } }` | 2 (Prisha, Daksh) |
| `$gte` | Greater than or equal to | `{ marks: { $gte: 80 } }` | 30 |
| `$ne` | Not equal to | `{ marks: { $ne: 85 } }` | 45 |

```js
db.students.find({ marks: { $gt: 80 } })
db.students.find({ marks: { $lt: 80 } })
db.students.find({ marks: { $eq: 85 } })
db.students.find({ marks: { $gte: 80 } })
db.students.find({ marks: { $ne: 85 } })
```

## 🧠 Logical Operators

### `$and`

Students with marks greater than 70 **and** age less than 22 (20 matches).

```js
db.students.find({
  $and: [
    { marks: { $gt: 70 } },
    { age: { $lt: 22 } }
  ]
})
```

### `$or`

Students from either the Cloud **or** IoT department (22 matches).

```js
db.students.find({
  $or: [
    { department: "Cloud" },
    { department: "IoT" }
  ]
})
```

### `$not`

Students whose marks are **not** greater than 80 (20 matches).

```js
db.students.find({ marks: { $not: { $gt: 80 } } })
```

### Consistency check

The results agree with each other: 27 + 20 = 47 and 17 + 30 = 47, matching the 47 documents in the collection.

---

## 📋 Verification Operations

Check a single record after an update:

```js
db.students.findOne({ rollNo: 301 })
```

Confirm deleted records are gone (returns no documents):

```js
db.students.find({ rollNo: { $in: [317, 338, 350] } })
```

Count total documents (returns 47):

```js
db.students.countDocuments()
```

Count students by department:

```js
db.students.countDocuments({ department: "DS" })
db.students.countDocuments({ department: "IoT" })
db.students.countDocuments({ department: "Cyber" })
db.students.countDocuments({ department: "Cloud" })
```

---

## 🎯 Learning Objectives

This project provides practical understanding of:

- NoSQL databases
- Collections and documents
- CRUD operations
- MongoDB Shell (`mongosh`)
- MongoDB Query Language
- Comparison operators (`$gt`, `$lt`, `$eq`, `$gte`, `$ne`)
- Logical operators (`$and`, `$or`, `$not`)
- Updating and deleting documents
- Searching and filtering records
- Verifying results with acknowledgement objects and counts

---

## 🚀 How to Run

1. **Install MongoDB** and the MongoDB Shell (`mongosh`).
2. **Open MongoDB Shell**
   ```bash
   mongosh
   ```
3. **Select a database** (any name you prefer)
   ```js
   use <your_database_name>
   ```
4. **Run the commands** on the `students` collection in sequence and verify the output after each operation.

---

## 📂 Project Structure

```
MongoDB-Student-Database-Operations/
│
├── README.md
│
└── MongoDB_Student_Database_Report_v5.pdf
```

---

## 🎓 Academic Information

| Field | Details |
|---|---|
| Project | MongoDB Student Database Operations |
| Course | Database Management System (NoSQL / MongoDB) |
| Program | BCADS27, 3rd Semester |
| University | Babu Banarasi Das University, Lucknow, U.P |
| Submitted to | Mr. Harendra Singh Rajpoot |
| Learning partner | IBM (Project Based Experimental Learning) |

---

## 👨‍💻 Author

**Yash Tandon**
Roll No. 1250258513
BCADS27, 3rd Semester

---

## ⭐ Project Highlights

- ✅ MongoDB NoSQL Database
- ✅ Student Records Management
- ✅ CRUD Operations
- ✅ Insert One & Insert Many
- ✅ Update One & Update Many
- ✅ Delete One & Delete Many
- ✅ Comparison Operators
- ✅ Logical Operators
- ✅ Result Verification with Counts
- ✅ Academic Practical Project

---

## 🔮 Future Scope

- Use the Aggregation Framework for department-wise averages, toppers and rankings.
- Add schema validation rules for data types and required fields.
- Create indexes on frequently queried fields such as `marks` and `department`.
- Build a web dashboard (e.g. Node.js and Express) to interact with the data.
- Extend the database with courses, attendance and results.

---
