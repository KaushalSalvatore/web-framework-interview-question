#### Q-1 How do you order results in SQLAlchemy ?
```bash
session.query(User).order_by(User.name.asc()).all()
```

#### Q-2 How do you count rows in SQLAlchemy ?
```bash
session.query(User).count()
```

#### Q-3 How to get distinct values in SQLAlchemy ?
```bash
session.query(User.city).distinct().all()
```

#### Q-4 How do you join tables in SQLAlchemy ?
```bash
session.query(User).join(Address).all()
```

#### Q-5 How do you perform left outer join in SQLAlchemy ?
```bash
session.query(User).outerjoin(Address).all()
```

#### Q-6 How do you get first and last records in SQLAlchemy ?
```bash
session.query(User).first()
session.query(User).order_by(User.id.desc()).first()
```

#### Q-7 How do you perform OR queries in SQLAlchemy ?
```bash
from sqlalchemy import or_
session.query(User).filter(or_(User.name == 'John', User.age > 30)).all()
```

#### Q-8 How do you perform NOT EQUAL queries in Django ORM ?
```bash
User.objects.exclude(name='John')
```

#### Q-9 How do you get only specific columns in SQLAlchemy ?
```bash
session.query(User.name, User.email).all()
```

#### Q-10 How to update with expression in SQLAlchemy ?
```bash
session.query(User).update({User.age: User.age + 1})
```

#### Q-11 How to check if an object exists in SQLAlchemy ?
```bash
session.query(User).filter(User.email == "abc@gmail.com").first() is not None
```

#### Q-12 How do you bulk insert in SQLAlchemy ?
```bash
session.bulk_save_objects(users_list)
session.commit()
```

#### Q-13 How to use subquery in SQLAlchemy ?
```bash
sub = session.query(User.id).filter(User.age > 30).subquery()
session.query(Address).filter(Address.user_id.in_(sub)).all()
```

#### Q-14 How to use group_by in SQLAlchemy ?
```bash
session.query(User.city, func.count(User.id)).group_by(User.city).all()
```

#### Q-15 How to filter nullable values in SQLAlchemy ?
```bash
session.query(User).filter(User.profile == None).all()
```

#### Q-16 How to do case-insensitive search in SQLAlchemy ?
```bash
from sqlalchemy import func
session.query(User).filter(func.lower(User.name) == 'john').all()
```
#### Q-17 Field Lookups example ? 
```bash
Query field lookups are nothing but a condition which specifies same as the SQL WHERE clause. They are stated 
as keyword arguments to the QuerySet methods such as filter(), exclude(), and get().
Student.objects.filter(first_name__startswith = 'Ritesh')   
Student.objects.get(first_name__exact = 'Arpita')       
Student.objects.filter(last_name__contains = 'Shar') 
```

#### Q-18 __endswith ? 
```bash
User.objects.filter(city__endswith='2').values('id','city')
```

#### Q-19 Relational operators ? 
```bash
gt -Greater than.
gte -Greater than or equal to.
lt -Less than.
lte -Less than or equal to.

User.objects.filter(age__gt=20).values('id','age')
```

#### Q-20 __startswith ? 
```bash
User.objects.filter(city__startswith='city').values('id','city')
```