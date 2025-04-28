# Django Interview Questions and Answers

---

### 1. What is Django?

**Answer:**  
Django is a high-level, open-source Python web framework that encourages rapid development and clean, pragmatic design. It is designed to help developers take applications from concept to completion quickly. Django follows the "batteries-included" philosophy, providing almost everything developers might need out of the box (ORM, authentication, admin panel, etc.).

---

### 2. What are the advantages of using Django?

**Answer:**  
- **Rapid Development:** Django’s built-in features allow for quick development.
- **Security:** Protects against common web attacks like SQL injection, XSS, CSRF, etc.
- **Scalability:** Suitable for both small and large-scale applications.
- **Versatility:** Can be used for content management, scientific computing platforms, social networks, etc.
- **Robust Community:** Large community and extensive documentation.
- **Admin Interface:** Automatically generated admin panel for easy data management.

---

### 3. Explain Django’s MVT architecture.

**Answer:**  
Django uses the Model-View-Template (MVT) architecture:
- **Model:** Represents the database schema and business logic.
- **View:** Handles the user request, processes data via models, and returns a response.
- **Template:** The presentation layer, responsible for rendering HTML.

MVT is similar to MVC but Django itself handles the controller part.

---

### 4. How does Django handle database migrations?

**Answer:**  
Django uses migrations to propagate changes you make to your models (adding/removing fields, etc.) into the database schema.  
- `python manage.py makemigrations` creates migration files.
- `python manage.py migrate` applies them to the database.

---

### 5. What are Django models?

**Answer:**  
Models are Python classes that define the structure of your database tables. Each attribute in a model class represents a field in the table. Django models use an ORM to interact with the database, allowing you to use Python code instead of SQL.

---

### 6. How do you perform CRUD operations in Django?

**Answer:**  
- **Create:** `Model.objects.create()` or `Model.save()`
- **Read:** `Model.objects.all()`, `Model.objects.filter()`, `Model.objects.get()`
- **Update:** Retrieve an instance, change attribute values, then call `.save()`
- **Delete:** Retrieve an instance and call `.delete()`

---

### 7. What are Django QuerySets?

**Answer:**  
A QuerySet is a collection of database queries to retrieve objects from your database. It is lazy, meaning the database is not queried until the QuerySet is evaluated. Common methods include `.all()`, `.filter()`, `.exclude()`, and `.order_by()`.

---

### 8. Explain Django’s ORM.

**Answer:**  
Django's Object-Relational Mapper (ORM) translates Python code into SQL queries, allowing you to interact with the database using Python objects and methods instead of writing SQL statements.

---

### 9. What are Django templates?

**Answer:**  
Templates are text files (usually HTML) that define the structure or layout of a file. Django’s template language allows you to embed dynamic content using variables, tags, and filters.

---

### 10. How does Django handle static files and media files?

**Answer:**  
- **Static files:** CSS, JavaScript, images not uploaded by users. Managed using `STATIC_URL` and `STATIC_ROOT`.
- **Media files:** User-uploaded files, managed using `MEDIA_URL` and `MEDIA_ROOT`.

During development, Django serves these files automatically. In production, a web server should serve them.

---

### 11. What are Django views?

**Answer:**  
Views are Python functions or classes that receive web requests and return web responses.  
- **Function-based views (FBV):** Simple Python functions.
- **Class-based views (CBV):** Classes that provide more structure and reusability.

---

### 12. What is URL routing in Django?

**Answer:**  
URL routing is how Django maps URLs to views using `urls.py`. Each URL pattern is associated with a view function or class, enabling clean and readable URLs.

---

### 13. How do you implement authentication and authorization in Django?

**Answer:**  
Django provides a built-in authentication system (User model, login, logout, password management) and authorization (permissions, groups). You can also use decorators like `@login_required` and class-based mixins for access control.

---

### 14. What is middleware in Django?

**Answer:**  
Middleware are hooks into Django's request/response processing. They can process requests before views are called and responses before they're sent to the client. Examples: authentication, session management, security checks.

---

### 15. How can you create REST APIs with Django?

**Answer:**  
- Use Django REST Framework (DRF), which provides tools to build Web APIs.
- Define serializers, views, and URL patterns for your API endpoints.
- DRF supports authentication, permissions, and rendering to JSON/XML.

---

### 16. How do you optimize database queries in Django?

**Answer:**  
- Use `select_related` for foreign key relationships and `prefetch_related` for many-to-many.
- Avoid N+1 query problems.
- Use indexing and query only necessary fields.
- Analyze queries with Django Debug Toolbar.

---

### 17. How does Django handle forms and validation?

**Answer:**  
Django provides `forms.Form` and `forms.ModelForm` classes to handle form rendering, validation, and processing. You can define custom validation methods using `clean()` and `clean_<fieldname>()`.

---

### 18. What is the use of signals in Django?

**Answer:**  
Signals allow decoupled applications to get notified when certain actions occur (e.g., `pre_save`, `post_save`, `pre_delete`, `post_delete`). This is useful for triggering logic in response to changes.

---

### 19. How can you secure a Django application?

**Answer:**  
- Use Django’s built-in security features (CSRF protection, XSS prevention, etc.).
- Always validate and sanitize user input.
- Use HTTPS.
- Keep Django and dependencies updated.
- Use strong passwords and environment variables for secrets.

---

### 20. How do you deploy a Django application?

**Answer:**  
- Set up a production web server (e.g., Gunicorn, uWSGI) behind a reverse proxy (Nginx, Apache).
- Configure static and media file serving.
- Use environment variables for sensitive settings.
- Set `DEBUG = False` and define `ALLOWED_HOSTS`.
- Use a production-ready database (e.g., PostgreSQL).

---

# More Django Interview Questions with Examples


### 21. How can you customize the Django admin interface?
**Example:**  
How would you display additional fields in the admin list view for a `Book` model?
```python
class BookAdmin(admin.ModelAdmin):
    list_display = ('title', 'author', 'published_date')
admin.site.register(Book, BookAdmin)
```

---

### 22. How do you create custom template filters in Django?
**Example:**  
Write a custom filter to capitalize every word in a string.
```python
from django import template
register = template.Library()

@register.filter(name='capitalize_words')
def capitalize_words(value):
    return ' '.join([w.capitalize() for w in value.split()])
```

---

### 23. How would you handle file uploads in Django?
**Example:**  
Describe how to create a model to store uploaded images.
```python
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    avatar = models.ImageField(upload_to='avatars/')
```
In forms:
```python
form = ProfileForm(request.POST, request.FILES)
```

---

### 24. How can you implement pagination in Django?
**Example:**  
How would you paginate a list of blog posts?
```python
from django.core.paginator import Paginator

posts = Post.objects.all()
paginator = Paginator(posts, 10)  # 10 posts per page
page_number = request.GET.get('page')
page_obj = paginator.get_page(page_number)
```

---

### 25. What are class-based views (CBVs) and when would you use them?
**Example:**  
Use a `ListView` for displaying a list of articles.
```python
from django.views.generic import ListView
class ArticleListView(ListView):
    model = Article
    template_name = 'articles/list.html'
```

---

### 26. How do you implement signals for post-save actions?
**Example:**  
Send an email after a new user is registered.
```python
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def send_welcome_email(sender, instance, created, **kwargs):
    if created:
        send_email('Welcome!', instance.email)
```

---

### 27. How would you write a custom manager in Django?
**Example:**  
Create a manager to get all published blog posts.
```python
class PublishedManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(status='published')

class Post(models.Model):
    # fields...
    objects = models.Manager()       # The default manager.
    published = PublishedManager()   # Our custom manager.
```

---

### 28. What is context in Django templates? How do you pass extra context to a template?
**Example:**  
Pass a variable `user_type` to a template.
```python
return render(request, 'profile.html', {'user_type': 'admin'})
```

---

### 29. How can you perform raw SQL queries in Django?
**Example:**  
```python
from django.db import connection

def my_custom_sql():
    with connection.cursor() as cursor:
        cursor.execute("SELECT * FROM myapp_mymodel WHERE id = %s", [1])
        row = cursor.fetchone()
```
Or using the ORM:
```python
MyModel.objects.raw('SELECT * FROM myapp_mymodel WHERE id = %s', [1])
```

---

### 30. How do you implement caching in Django?
**Example:**  
Enable per-view caching for a view.
```python
from django.views.decorators.cache import cache_page

@cache_page(60 * 15)  # Cache for 15 minutes
def my_view(request):
    ...
```
Or use the low-level cache API:
```python
from django.core.cache import cache
cache.set('my_key', 'my_value', timeout=300)
value = cache.get('my_key')
```

---

### 31. How do you use Django’s built-in User model for authentication?
**Example:**  
Authenticate and log in a user.
```python
from django.contrib.auth import authenticate, login

user = authenticate(username='john', password='secret')
if user is not None:
    login(request, user)
```

---

### 32. What is a migration and what does a migration file contain?
**Example:**  
A migration is a Python file that contains code to modify your database schema (create, alter, or delete tables/fields).  
Example file content:
```python
class Migration(migrations.Migration):

    operations = [
        migrations.AddField(
            model_name='profile',
            name='age',
            field=models.IntegerField(null=True),
        ),
    ]
```

---

### 33. How do you restrict access to certain views in Django?
**Example:**  
Require login for a view.
```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    ...
```
Or for class-based views:
```python
from django.contrib.auth.mixins import LoginRequiredMixin

class DashboardView(LoginRequiredMixin, View):
    ...
```

---

### 34. How do you handle different environments (dev, staging, prod) in Django?
**Example:**  
Use separate settings files or environment variables:
```python
import os

DEBUG = os.environ.get('DJANGO_DEBUG', '') == '1'
```
You might have `settings/dev.py`, `settings/prod.py` for different environments.

---

### 35. How do you handle internationalization (i18n) in Django?
**Example:**  
Mark text for translation:
```python
from django.utils.translation import gettext as _

def my_view(request):
    output = _("Welcome to my site.")
```

---

### 36. How do you implement permissions for REST APIs in Django REST Framework?
**Example:**  
Restrict access to authenticated users only.
```python
from rest_framework.permissions import IsAuthenticated

class MyView(APIView):
    permission_classes = [IsAuthenticated]
    ...
```

---

### 37. What are migrations dependencies?
**Example:**  
Specify that a migration depends on another migration.
```python
class Migration(migrations.Migration):

    dependencies = [
        ('app_name', '0005_auto_20210401_1234'),
    ]
```

---

### 38. How do you customize Django’s error pages (404, 500)?
**Example:**  
Create `404.html` or `500.html` templates in your templates directory.  
You can also define custom views in `urls.py`:
```python
handler404 = 'myapp.views.custom_404_view'
```

---

### 39. How do you serve static files in production?
**Example:**  
Use a web server like Nginx or Apache to serve files from the directory specified in `STATIC_ROOT`.  
Example Nginx config:
```
location /static/ {
    alias /path/to/static/;
}
```

---

### 40. How do you create and use fixtures in Django?
**Example:**  
Export data:
```sh
python manage.py dumpdata myapp.ModelName > modelname.json
```
Load data:
```sh
python manage.py loaddata modelname.json
```