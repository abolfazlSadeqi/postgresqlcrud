
Create a simple CRUD application with postgresql and EF7 Core :

## Install and setup
### 1. Download and install a PostgreSQL server and unzip File

https://www.postgresql.org/download/windows/
 
### 2. initdb
•	Open command-line tool and run command

•	a)cd path\bin

•	b)initdb.exe -U postgres -A password -E utf8 -W -D path\Data


### 3. start service with use pg_ctl
•	pg_ctl -D  "path\Data"  start

### 4. config pgAdmin 4

•	a)Go to the “path\pgAdmin 4\runtime”

•	b)run pgAdmin4.exe

•	c)Go to “Dashboard”. click “Add New Server” to add a new connection.

 
•	Set configure 

|Tab|Config	|description|
|-|-|-|
|General|Name|Set custom Name|
|Connection|Hostname/Address|set your server’s IP |
|Connection|Port	|Set your server’s Port(Default :5432)|
|Connection|Database Maintenance|Set name of the database  |
|Connection|username  |Set custom username  (Default : postgres )|
|Connection|password	|Set custom password|
 
## Steps implementing

### 1.Install packages ON nugget

|package|desc|
|-|-|
|Npgsql.EntityFrameworkCore.PostgreSQL|	is the open source EF Core provider for PostgreSQL|
|Microsoft.EntityFrameworkCore.Tools|	Entity Framework Core Tools for the NuGet Package Manager Console in Visual Studio.|
|Microsoft.EntityFrameworkCore.Design|	Shared design-time components for Entity Framework Core tools.|
|Microsoft.EntityFrameworkCore|	It supports LINQ queries, change tracking, updates, and schema migrations. EF Core works with SQL Server, SQLite, MySQL, PostgreSQL, and other databases through a provider plugin API.|

### 2. Define a DBSet 
```

 public class Person
{

    [Key]
    public int ID { set; get; }
     ….


}
```

### 3. Define a DbContext
```

 public class TestCurdContext : DbContext
{
    public TestCurdContext(DbContextOptions<TestCurdContext> options)
        : base(options)
    {
    }
    public DbSet<Person> Persons => Set<Person>();
}
```

### 4. add config to appsetting 
 ```

 "ConnectionStrings": {
  "TestCurdContextConnection": "Server=localhost;Database=testdb;UserId=postgres;Password=123"
}
```
 

### 5.add configuration in Program or startup 
 ```

 services.AddDbContext<TestCurdContext>(options =>
  options
    .UseNpgsql(Configuration
               .GetConnectionString("TestCurdContextConnection")));
```


### 6.Using methods (insert, update, …)
Because we use EF, we can use EF's Command
 



Tech Specification:
----
.EFCore7 

.Net7

.Swagger UI

.TDD(XUnit)

.WebAPI

.postgresql

feature:
--
CURD For Classes

Integration Test



