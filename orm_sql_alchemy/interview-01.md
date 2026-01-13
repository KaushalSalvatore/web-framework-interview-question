#### Q-1 What are the benefits of using an ORM tool ?
```bash
ORM tools abstract the database layer, allowing developers to work with objects instead of 
writing complex SQL queries.
They simplify database operations by automatically generating SQL queries based on object-oriented 
code.
ORM tools handle database connections, transactions, and caching, reducing the amount of boilerplate 
code.
```

#### Q-2 What is the difference between the code-first and database-first approaches ?
```bash
Code first approach involves creating the database schema based on the code, while database first approach involves 
creating the code based on an existing database schema.
Code first approach focuses on defining the entities and their relationships in code, and then generating the database 
schema from the code.
Database first approach involves designing the database schema first, and then generating the code based on the schema.
Code first approach provides more control over the database schema and allows for easier versioning and migration.
Database first approach is useful when working with an existing database or when the database schema is already defined.
Code first approach is commonly used in Object-Relational Mapping (ORM) frameworks like Entity Framework.
Database first approach is commonly used when working with legacy systems or when the database design is critical.
```

#### Q-3 How would you handle transactions and rollbacks in SQLAlchemy ?
```bash
In SQLAlchemy, transactions are handled using session objects. A new transaction begins automatically after Session.commit() 
is called. If any error occurs during the transaction, Session.rollback() is used to rollback all changes made in the current 
transaction.

from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
engine = create_engine('sqlite:///example.db')
Session = sessionmaker(bind=engine)
session = Session() 
try:          # perform some operations...
session.add(some_object)
session.commit()
except:
session.rollback()
finally:
session.close()
```

#### Q-4 What is the role of the MetaData class in SQLAlchemy ?
```bash
MetaData in SQLAlchemy serves as a registry for schema constructs like tables. It collects Table objects and provides
SQL generation services. MetaData is initialized with bind parameters to connect to a database, allowing it to issue 
CREATE and DROP commands directly.
```

#### Q-5 How does SQLAlchemy handle relationships between tables and what are its advantages ?
```bash
SQLAlchemy uses a system called Object-Relational Mapping (ORM) to handle relationships between tables. It allows 
developers to work with databases using Pythonic syntax, abstracting the underlying SQL commands.

The advantages of SQLAlchemy’s approach include:
1. Abstraction: Developers don’t need deep knowledge of SQL.
2. Flexibility: Supports multiple DBMS systems.
3. Efficiency: Lazy loading optimizes database queries.
4. Maintainability: Changes in schema can be managed through ORM without altering codebase.
5. Consistency: Enforces data integrity at ORM level.
```

#### Q-6 Disadvantages of ORM ?
```bash
Slower than raw SQL
Hard to optimize complex queries
Might hide database-specific optimizations
```

#### Q-7 How do you define a model in SQLAlchemy ?
```bash
from sqlalchemy import Column, Integer, String
from sqlalchemy.orm import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
```

#### Q-8 How do you insert a record in SQLAlchemy ORM ?
```bash
user = User(name="John")
session.add(user)
session.commit()
```

#### Q-9 How do you query all records ?
```bash
users = session.query(User).all()
```

#### Q-10 How do you filter rows ?
```bash
user = session.query(User).filter(User.name == "John").first()
```

#### Q-11 How do you perform LIKE queries in SQLAlchemy ?
```bash
results = session.query(User).filter(User.name.like("%jo%")).all()
```

#### Q-12 How do you update a record ?
```bash
user = session.query(User).filter_by(id=1).first()
user.name = "NewName"
session.commit()
```

#### Q-13 How do you delete a record ?
```bash
user = session.query(User).get(1)
session.delete(user)
session.commit()
```

#### Q-14 What is relationship() in SQLAlchemy ?
```bash
class Address(Base):
    __tablename__ = "addresses"
    id = Column(Integer, primary_key=True)
    user_id = Column(Integer, ForeignKey("users.id"))

    user = relationship("User", back_populates="addresses")
```
#### Q-15 How to perform aggregation in Django ORM ?
```bash
from django.db.models import Count
User.objects.aggregate(total=Count("id"))
```

#### Q-16 How do you perform group by in SQLAlchemy ?
```bash
session.query(User.name, func.count(User.id)).group_by(User.name).all()
```

#### Q-17 How do you handle transactions in SQLAlchemy ?
```bash
with session.begin():
    session.add(User(name="John"))
```

#### Q-18 What is lazy loading vs eager loading ?
```bash
| Type  | Description                               |
| ----- | ----------------------------------------- |
| Lazy  | Loads related data when accessed          |
| Eager | Loads related data immediately using join |
```

#### Q-19 What is the difference between filter() and filter_by() in SQLAlchemy ?
```bash
filter() uses expressions → filter(User.age > 30)
filter_by() uses keyword arguments → filter_by(age=30)
```

#### Q-20 How do you perform an IN query in SQLAlchemy ?
```bash
session.query(User).filter(User.id.in_([1, 2, 3])).all()
```