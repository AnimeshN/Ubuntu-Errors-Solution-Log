https://www.youtube.com/watch?v=aHC3uTkT9r8&t=311s

### in model.py we are creating a table Post with diffrent attributes

```
from django.db import models
from django.utils import timezone
from django.contrib.auth.models import User

class Post(models.Model):
	title = models.CharField(max_length=100)
	content = models.TextField()
	date_posted = models.DateTimeField(default=timezone.now)
	author = models.ForeignKey(User, on_delete=models.CASCADE)   #User is already created by django
```
```
python manage.py makemigrations # in migration folder you can check 000#_initial.py
python manage.py  sqlmigrate <appname> 000#
python manage.py migrate
python manage.py shell
```
#### following are some commands from shell( blog is appname)
```
from blog.models import Post
from django.contrib.auth.models import User
User.objects.all()
User.objects.first()
User.objects.filter(username='').first()
user = User.objects.filter(username='').first()
user.id
user.pk
User.obects.get(id=1)
Post.objects.all()
post_1 = Post(title='Blog 1', content='',author=user)
post_1.save()
```
```
#in models.py

def __str__(self):			# for returning string as we want  in Post.objects.all()
	return self.title     
```
```
post.author.email   #merging table
user.post_set.all()  # set of all post by user
user.post_set.create(title='Blog 3', content = '') # directly post is created
```
### how to pass data in database into a page using views

```
# in views.py
from .models import Post

def home(request):
	context = {
		'posts':Post.objects.all()	
	}
	return render(request, 'blog/home.html',context)
```

# we can display post data like
```
{% block content %}
{% for post in posts %}
	{{post.author}}
	{{post.date_posted|date:"F d, Y"}} #date formatting	
	{{post.title}}
	{{post.content}}	
{% endfor %}
{% endblock content %}

``` 

#### how to add our Post table to admin
```
#in admin.py

from django.contrib import admin
from . models import Post

admin.site.register(Post)

```






