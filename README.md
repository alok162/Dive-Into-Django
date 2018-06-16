# Project Title
**Dive-Into-Django**


# Django aggregate function
  1. Max
  2. Min
  3. Avg
  4. Sum

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
Account.objects.values('account_id').distinct()
<QuerySet [{'account_id': 2}, {'account_id': 3}, {'account_id': 1}]>
```