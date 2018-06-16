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
    {'price__min': 01245}
```