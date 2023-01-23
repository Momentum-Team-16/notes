# REST API Development 101

## HTTP Methods, CRUD, & Database actions

| HTTP method | CRUD action     | SQL  (Django ORM does this for you) |
| ----------- | --------------- | ----------------------------------- |
| POST        | Create          | INSERT                              |
| GET         | Read (Retrieve) | SELECT                              |
| PUT/PATCH   | Update          | UPDATE                              |
| DELETE      | Destroy         | DELETE                              |

## REST is a convention for structuring API data

REST (shorthand for “Representational State Transfer”) is a set of guidelines for how to represent information in an API that provides data by means of HTTP requests. We consider this data “resources.” Resources in your API are probably your models, but may be other things as well. Like models, they are usually *nouns*.

### RESTful APIs provide endpoints to access data

You can think of an endpoint as an HTTP Method + URL + resource

## Resources can be single or a collection

Resources can be **single** or a **collection**. Habits are a resource in the Habit Tracker project; so are daily records for tracking progress on building a habit. You probably built urls + views that included, for example:

- *details about one specific habit* (a **single** resource)
- *a list of all your habits* (a **collection** resource)

Almost all REST APIs implement urls like the following to provide CRUD actions for single and collection resources.

| HTTP method | URL       | Description of resource      |
| ----------- | --------- | ---------------------------- |
| GET         | /habits   | list of all habits           |
| POST        | /habits   | create a new habit in the db |
| GET         | /habits/1 | one habit with PK 1          |
| PUT/PATCH   | /habits/1 | update habit with PK 1       |
| DELETE      | /habits/1 | delete habit with PK 1       |

## Resources can be **nested to show relationships**

Related resources can be nested**.** For example, you may have shown daily records related to a single habit on a habit detail page in your Habit Tracker app.

You could represent all the daily records (collection) for a specific habit like so:

| GET | /habits/1/daily-records | Show all daily records for habit with PK 1 |
| --- | ----------------------- | ------------------------------------------ |

## **Best Practices for your REST API**

### 📌 Use lower-case letters in the URL.

✅ `/habits`

❌ `/Habits`

### 📌 Use hyphens instead of underscores or camel-case in the URL.

✅ `/daily-records`

❌ `/daily_records`

### 📌 Don’t use CRUD verbs in the URL; the HTTP method already has a verb that maps to CRUD action.

✅ PATCH `habits/1`

❌ PATCH `habits/1/edit`

### 📌 Don’t nest resources unless you need to use some information in the URL path (like a PK) to look things up in the database in your view.

❌ `habits/1/daily_records/4`

✅ `daily_records/4`

### 📌 Consider what you should include in your API and what you should leave out

For example, you probably don’t want to provide a list of all your application’s users, except to users with special permissions.

### 📌 Use the right [status code](https://www.django-rest-framework.org/api-guide/status-codes/#status-codes)

Django and other libraries will do this for you most of the time, but sometimes you want to return an status code yourself. For example, if a request fails validation you could use a `400 Bad Request` status to indicate that.

```python
try:
  return super().create(request, *args, **kwargs)
except IntegrityError:
    error_data = {
       "error": "Unique constraint violation: a title with this author already exists."}
    return Response(error_data, status=status.HTTP_400_BAD_REQUEST)
```

### 📌 Use [pagination](https://www.django-rest-framework.org/api-guide/pagination/#pagination)

Paginating your API lets you manage large amounts of data, preventing your responses from becoming too slow and unwieldy.

For example, if a request would return 200 objects, your response may return the first set of 50 records with a link to the next set of 50 (and so on).

### 📌 Document your API

So that your users know what your endpoints are, how to use them, and what to expect in response. There are tools that you can use to generate documentation, but you can also just write up your endpoints and how they work in a README.md file in your repo.
