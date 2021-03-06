# Project Title

**Dive-Into-Django**

**What is ORM?**

ORMs provide a high-level abstraction upon a relational database that allows a developer to write Python code instead of SQL to create, read, update and delete data and schemas in their database. Developers can use the programming language they are comfortable with to work with a database instead of writing SQL statements or stored procedures.

For example, without an ORM a developer would write the following SQL statement to retrieve every row in the USERS table where the zip_code column is 94107:

```python
SELECT * FROM USERS WHERE zip_code=94107;
```

The equivalent Django ORM query would instead look like the following Python code:

```python
>>> users = Users.objects.filter(zip_code=94107)
```

The ability to write Python code instead of SQL can speed up web application development, especially at the beginning of a project. The potential development speed boost comes from not having to switch from Python code into writing declarative paradigm SQL statements. While some software developers may not mind switching back and forth between languages, it's typically easier to knock out a prototype or start a web application using a single programming language.

ORMs also make it theoretically possible to switch an application between various relational databases. For example, a developer could use SQLite for local development and MySQL in production. A production application could be switched from MySQL to PostgreSQL with minimal code modifications.

# Django aggregate function

Aggregate calculates values for the entire queryset.

1.  Max
2.  Min
3.  Avg
4.  Sum

**Example**

```python
>>> from django.db.models import Avg, Max, Min, Sum
>>> device.objects.all().aggregate(Avg('price'))
    {'price__avg': 12234.0}
>>> device.objects.all().aggregate(Max('price'))
    {'price__max':587961 }
>>> device.objects.all().aggregate(Min('price'))
    {'price__min': 1245}
>>> device.objects.all().aggregate(Sum('price'))
    {'price__sum': 10000245}
```

**Django annotate function**

Annotate function in django is nothing but groupby query

**example**

```python
>>> City.objects.values('country__name').annotate(Sum('population'))
    [
  {'country__name': u'Angola', 'population__sum': 6542944},
  {'country__name': u'Argentina', 'population__sum': 13074000},
  {'country__name': u'Australia', 'population__sum': 9650500},
  {'country__name': u'Bangladesh', 'population__sum': 17151925},
  {'country__name': u'Brazil', 'population__sum': 38676123},
  '...(remaining elements truncated)...'
]


>>> Account.objects.values('account_id').annotate(Count('stage'))
<QuerySet [{'account_id': 2, 'stage__count': 2}, {'account_id': 3, 'stage__count': 3}, {'account_id': 1, 'stage__count': 3}]>
```

**Orderby() function:**

```python
>>> City.objects.values('country__name') \
    .annotate(country_population=Sum('population')) \
    .order_by('-country_population')

[
  {'country__name': u'China', 'country_population': 309898600},
  {'country__name': u'United States', 'country_population': 102537091},
  {'country__name': u'India', 'country_population': 100350602},
  {'country__name': u'Japan', 'country_population': 65372000},
  {'country__name': u'Brazil', 'country_population': 38676123},
  '...(remaining elements truncated)...'
]


>>> Account.objects.values('id').order_by('-id')
<QuerySet [{'id': 9}, {'id': 8}, {'id': 7}, {'id': 6}, {'id': 5}, {'id': 4}, {'id': 3}, {'id': 1}]>
```

**count() function:**

```python
City.objects.values('country__name').count()
29
```

**distinct() function:**

```python
>>> Account.objects.values('account_id').distinct()
<QuerySet [{'account_id': 2}, {'account_id': 3}, {'account_id': 1}]>
```

# Join

**select_related:**
select_related function is used to simply make sql join between tables.

**exmaple**

```python
class Artist(models.Models):
    name = models.CharField(max_length=200)
    ...

class Song(models.Models):
    artist = models.ForeignKey(Artist)
    ...
```

Lets perform join between two tables

```python
>>> Song.objects.select_related('artist').get(id=1234).artist.name
'ALOK CHOUDHARY'
```

# https://docs.djangoproject.com/en/1.11/ref/models/querysets/#id4
