# Python - sqlalchemy
> Autor: Lucas Joshua Pires

## 1. Creating a common interface with the Database (engine)

- SQLite
~~~ python
from sqlalchemy import create_engine

dialect_driver = 'sqlite:///'
db = 'census.sqlite'
engine = create_engine('sqlite:///census.sqlite')
~~~

- ### PostgreSQL
~~~ python
from sqlalchemy import create_engine

dialect_driver = 'postgresql+psycopg2://'
user_passwd = 'student:datacamp'
host_port = '@postgresql.csrrinzqubik.us-east-1.rds.amazonaws.com:5432/'
db = 'census'
engine = create_engine(dialect_driver + user_passwd + host_port + db)
~~~

## 2. Printing all table names
~~~ python
print(engine.table_names())
~~~

## 3. Connecting to the Database
~~~ python
connection = engine.connect()
~~~

## 4. Printing the SQLAlchemy Table object
~~~ python
from sqlalchemy import Table, MetaData
metadata = MetaData()
census = Table('census', metadata, autoload=True, autoload_with=engine)
print(repr(census))
~~~

## 5. Creating Statements:
~~~ python
from sqlalchemy import select, where, like, between, \
    in_, and_, not_, or_, \
    order_by
~~~

### SELECT
~~~ python
stmt = select([census])
results = connection.execute(stmt).fetchall()
~~~

### WHERE
~~~ python
stmt = select([census]).where(census.columns.state == 'Californias')
stmt = select([census]).where(census.columns.state.startswith('New'))
results = connection.execute(stmt).fetchall()
~~~

### OR
~~~ python
stmt = select([census]).where(
    or_(
        census.columns.state == 'California',
        census.columns.state == 'Texas'
    )
)
results = connection.execute(stmt).fetchall()
~~~

### ORDER BY
~~~ python
stmt = select([ census.columns.state,
                census.columns.age]).order_by(census.columns.age,
                                              census.columns.state.desc())
results = connection.execute(stmt).fetchall()
~~~

### COUNT / SUM
~~~ python
from sqlalchemy import func
stmt = select([func.count(census.columns.pop2018)])
stmt = select([func.count(census.columns.pop2018.distinct())])
stmt = select([func.sum(census.columns.pop2018)])
stmt = select([func.sum(census.columns.pop2018.distinct())])
results = connection.execute(stmt).scalar()
~~~

### GROUP BY
~~~ python
pop2018_sum = func.sum(census.columns.pop2018).label('population')
stmt = select([census.columns.state, pop2018_sum])
stmt = stmt.group_by(census.columns.state)
results = connection.execute(stmt).fetchall()

for result in results:
    print(result.state, result.age, result.sex)
~~~