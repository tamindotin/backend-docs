# MongoDB Shell (mongosh) Cheat Sheet

## Start MongoDB Shell

### Local MongoDB

```bash
mongosh
```

### Docker Container

```bash
docker exec -it <container_name> mongosh
```

Example:

```bash
docker exec -it mongodb mongosh
```

---

# Authentication

If authentication is enabled:

```bash
mongosh -u <username> -p <password> --authenticationDatabase admin
```

Example:

```bash
mongosh -u admin -p admin123 --authenticationDatabase admin
```

Inside Docker:

```bash
docker exec -it mongodb mongosh \
-u admin \
-p admin123 \
--authenticationDatabase admin
```

Authenticate after entering the shell:

```javascript
use admin

db.auth("admin", "admin123")
```

---

# Database Commands

## Show all databases

```javascript
show dbs
```

---

## Switch database

```javascript
use myDatabase
```

---

## Show current database

```javascript
db
```

---

## Drop current database

```javascript
db.dropDatabase()
```

⚠️ Permanently deletes the current database.

---

# Collection Commands

## Show collections

```javascript
show collections
```

---

## Create collection

```javascript
db.createCollection("users")
```

---

## Drop collection

```javascript
db.users.drop()
```

⚠️ Permanently deletes the collection.

---

# Insert Documents

## Insert one

```javascript
db.users.insertOne({
    name: "John",
    age: 20
})
```

---

## Insert many

```javascript
db.users.insertMany([
    {
        name: "Alice",
        age: 21
    },
    {
        name: "Bob",
        age: 25
    }
])
```

---

# Read Documents

## Find all

```javascript
db.users.find()
```

Pretty output:

```javascript
db.users.find().pretty()
```

---

## Find one

```javascript
db.users.findOne({
    name: "John"
})
```

---

## Filter documents

```javascript
db.users.find({
    age: {
        $gt: 18
    }
})
```

---

## Select fields

```javascript
db.users.find(
    {},
    {
        name: 1,
        age: 1,
        _id: 0
    }
)
```

---

# Update Documents

## Update one

```javascript
db.users.updateOne(
    {
        name: "John"
    },
    {
        $set: {
            age: 22
        }
    }
)
```

---

## Update many

```javascript
db.users.updateMany(
    {},
    {
        $set: {
            active: true
        }
    }
)
```

---

# Delete Documents

## Delete one

```javascript
db.users.deleteOne({
    name: "John"
})
```

---

## Delete many

```javascript
db.users.deleteMany({
    active: false
})
```

---

# Query Operators

Greater than

```javascript
db.users.find({
    age: {
        $gt: 18
    }
})
```

Less than

```javascript
db.users.find({
    age: {
        $lt: 30
    }
})
```

Greater than or equal

```javascript
db.users.find({
    age: {
        $gte: 18
    }
})
```

Less than or equal

```javascript
db.users.find({
    age: {
        $lte: 25
    }
})
```

Equal

```javascript
db.users.find({
    age: 20
})
```

Not equal

```javascript
db.users.find({
    age: {
        $ne: 20
    }
})
```

IN

```javascript
db.users.find({
    age: {
        $in: [18, 20, 22]
    }
})
```

NOT IN

```javascript
db.users.find({
    age: {
        $nin: [18, 20]
    }
})
```

AND

```javascript
db.users.find({
    age: {
        $gt: 18
    },
    active: true
})
```

OR

```javascript
db.users.find({
    $or: [
        {
            age: 18
        },
        {
            age: 20
        }
    ]
})
```

---

# Sorting

Ascending

```javascript
db.users.find().sort({
    age: 1
})
```

Descending

```javascript
db.users.find().sort({
    age: -1
})
```

---

# Pagination

Limit

```javascript
db.users.find().limit(5)
```

Skip

```javascript
db.users.find().skip(10)
```

Skip + Limit

```javascript
db.users.find()
.skip(10)
.limit(5)
```

---

# Count Documents

```javascript
db.users.countDocuments()
```

Filtered count

```javascript
db.users.countDocuments({
    active: true
})
```

---

# Indexes

Show indexes

```javascript
db.users.getIndexes()
```

Create index

```javascript
db.users.createIndex({
    email: 1
})
```

Drop index

```javascript
db.users.dropIndex("email_1")
```

---

# User Commands

Show users

```javascript
db.getUsers()
```

Create user

```javascript
db.createUser({
    user: "admin",
    pwd: "password",
    roles: [
        {
            role: "root",
            db: "admin"
        }
    ]
})
```

---

# Useful Helpers

Show current database

```javascript
db
```

Show database stats

```javascript
db.stats()
```

Show collection stats

```javascript
db.users.stats()
```

List databases

```javascript
show dbs
```

List collections

```javascript
show collections
```

Clear terminal

```javascript
cls
```

Exit shell

```javascript
exit
```

or press

```
Ctrl + D
```

---

# Docker Examples

Start MongoDB container

```bash
docker start mongodb
```

Open mongosh

```bash
docker exec -it mongodb mongosh
```

Open with authentication

```bash
docker exec -it mongodb mongosh \
-u admin \
-p admin123 \
--authenticationDatabase admin
```

View logs

```bash
docker logs mongodb
```

---

# MongoDB CRUD ↔ Mongoose Mapping

| MongoDB Shell | Mongoose |
|--------------|----------|
| `insertOne()` | `Model.create()` |
| `find()` | `Model.find()` |
| `findOne()` | `Model.findOne()` |
| `updateOne()` | `Model.updateOne()` |
| `deleteOne()` | `Model.deleteOne()` |
| `countDocuments()` | `Model.countDocuments()` |
| `find().sort()` | `.sort()` |
| `find().limit()` | `.limit()` |
| `find().skip()` | `.skip()` |

---

# Commands You'll Use Most

- `show dbs`
- `use`
- `db`
- `show collections`
- `insertOne()`
- `find()`
- `findOne()`
- `updateOne()`
- `deleteOne()`
- `countDocuments()`
- `sort()`
- `limit()`
- `skip()`
- `getUsers()`
- `exit`
