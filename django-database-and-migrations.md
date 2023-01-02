# Database

Django officially supports a number of databases
- PostgreSQL
- MariaDB
- MySQL
- Oracle
- ⭐️SQLite - this is the default database that ships with Django. If you don't otherwise establish a database in `settings.py`, 
  Django will create a SQLite database, a file in the root directory of the project, the first time you run `python manage.py migrate`.
- Each model in your Django application (including those that come in the Django source code, such as `Session`) will be represented by a table in 
  the database.
  
## Migrations

- When you run `python manage.py makemigrations`, Django perceives any changes to models, new models that were created, or models that have been deleted. 
  The migration files are created in the `migrations` directory by Django. Each migration file is a set of instructions for the changes that Django needs 
  to apply to the database. The order is important, and all the migration files should be committed to version control. _Remember: if you create a pull 
  request with changes to models, the corresponding migration files should be present in the pull request._
- The instructions in the `migrations` directory are actually _applied_ to the database when you run `python manage.py migrate`.
  
 
