# What is Django?

Django is a high-level Python web framework that enables rapid development of secure and maintainable websites.


- [Release Notes](https://docs.djangoproject.com/en/5.0/releases)


## Source Code

Django web applications typically group the code that handles each of these steps into separate files:

- URLs
- View
- Models
- Templates


### URLs

A URL mapper is typically stored in a file named `urls.py`

For example, the mapper `urlpatterns` defines a list of mappings between _routes_ (specific URL patterns) and corresponding view functions.

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('book/<int:id>/', views.book_detail, name='book_detail'),
    path('catalog/', include('catalog.urls')),
    re_path(r'^([0-9]+)/$', views.best),
]
```

The `urlpatterns` object is a list of `path()`


### Views

Views are the heart of the web application, receiving HTTP requests from web clients and returning HTTP responses.

For example, the function `index` receives an `HttpRequest` object as a parameter (request) and returns an `HttpResponse` object.

```python
# filename: views.py (Django view functions)

from django.http import HttpResponse

def index(request):
    # Get an HttpRequest - the request parameter
    # perform operations using information from the request.
    # Return HttpResponse
    return HttpResponse('Hello from Django!')
```


### Models

Django web applications manage and query data through Python objects referred to as models.

For example, a model for a `Team` object. The `Team` class is derived from the Django class `models.Model`

It defines:
- the team name and 
- team level

as character fields and specifies a maximum number of characters to be stored for each record.


```python
# filename: models.py

from django.db import models

class Team(models.Model):
    team_name = models.CharField(max_length=40)

    TEAM_LEVELS = (
        ('U09', 'Under 09s'),
        ('U10', 'Under 10s'),
        ('U11', 'Under 11s'),
        # …
        # list other team levels
    )
    team_level = models.CharField(max_length=3, choices=TEAM_LEVELS, default='U11')
```


### Templates

Template systems allow you to specify the structure of an output document, using placeholders for data that will be filled in when a page is generated.


```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Home page</title>
</head>
<body>
  {% if youngest_teams %}
    <ul>
      {% for team in youngest_teams %}
        <li>{{ team.team_name }}</li>
      {% endfor %}
    </ul>
  {% else %}
    <p>No teams are available.</p>
  {% endif %}
</body>
</html>
```
