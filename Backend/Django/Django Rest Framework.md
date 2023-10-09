# Django Rest Framework

Django REST framework is a powerful and flexible toolkit for building Web APIs.

## Installation
---
```
pip install djangorestframework
pip install markdown
pip install django-filter
```

add `'rest_framework'` to your `INSTALLED_APPS`:
```python
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```
<br>

## Implementation
---

### 1. Serializers
---

Serializers are JSON parsers for Models.

***serializers.py***
```python
from django.contrib.auth.models import User, Group
from rest_framework import serializers


class UserSerializer(serializers.Serializer):
    class Meta:
        model = User
        fields = ['url', 'username', 'email', 'groups']


class GroupSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Group
        fields = ['url', 'name']
```

### 2. Views
---
Views are functions for how data be display.

```python
from django.contrib.auth.models import User, Group
from rest_framework import viewsets
from rest_framework import permissions
from tutorial.quickstart.serializers import UserSerializer, GroupSerializer


class UserViewSet(viewsets.ModelViewSet):
    """
    API endpoint that allows users to be viewed or edited.
    """
    queryset = User.objects.all().order_by('-date_joined')
    serializer_class = UserSerializer
    permission_classes = [permissions.IsAuthenticated]


class GroupViewSet(viewsets.ModelViewSet):
    """
    API endpoint that allows groups to be viewed or edited.
    """
    queryset = Group.objects.all()
    serializer_class = GroupSerializer
    permission_classes = [permissions.IsAuthenticated]
```

### 3. URLs
---
URLs are for wireing views into urls.
```python
from django.urls import include, path
from rest_framework import routers
from tutorial.quickstart import views

router = routers.DefaultRouter()
router.register(r'users', views.UserViewSet)
router.register(r'groups', views.GroupViewSet)

# Wire up our API using automatic URL routing.
# Additionally, we include login URLs for the browsable API.
urlpatterns = [
    path('', include(router.urls)),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```



