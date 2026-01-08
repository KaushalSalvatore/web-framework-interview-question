#### Q-1 Django REST Framework (DRF) ?
```bash
DRF is a powerful toolkit built on Django to build RESTful APIs with features like serializers, 
authentication, permissions, throttling, and viewsets.

REST is an architectural style using HTTP methods (GET, POST, PUT, PATCH, DELETE) to perform 
CRUD operations on resources.
```

#### Q-2 What is a Serializer ?
```bash
Serializers convert model instances ↔ JSON and handle validation.
```
#### Q-3 Serializer vs ModelSerializer ?
```bash
ModelSerializer auto-generates fields and validations from a model.
```

#### Q-4 What is ViewSet ?
```bash
A ViewSet combines multiple views (list, create, retrieve, update, delete) into a single class.
```

#### Q-5 What is Pagination ?
```bash
Splits large results into pages.
REST_FRAMEWORK = {
  'DEFAULT_PAGINATION_CLASS': 'PageNumberPagination'
}
```

#### Q-6 What does HATEOAS stand for ?
```bash
HATEOAS = Hypermedia As The Engine Of Application State

HATEOAS is a REST principle where the API response includes links that tell the client what 
actions can be performed next.

With HATEOAS, the server guides the client by providing links to related actions in the API response.

{
  "order_id": 101,
  "status": "created",
  "links": {
    "self": "/orders/101/",
    "pay": "/orders/101/pay/",
    "cancel": "/orders/101/cancel/"
  }
}

Client knows exactly what it can do next
✔ Loose coupling
✔ Easier API evolution

✅ Benefits of HATEOAS
Decouples client from server
Makes APIs self-descriptive
Easier versioning & maintenance
```

#### Q-7 What does CORS stand for ?
```bash
CORS = Cross-Origin Resource Sharing
CORS decides whether a browser is allowed to call an API hosted on a different domain.

Access-Control-Allow-Origin: https://frontend.com
Access-Control-Allow-Methods: GET, POST
Access-Control-Allow-Headers: Authorization

pip install django-cors-headers

INSTALLED_APPS = [
    'corsheaders',
]
MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
]
CORS_ALLOWED_ORIGINS = [
    "https://frontend.com",
]
```

#### Q-8 How does DRF handle a request internally ?
```bash
Request hits Django middleware
DRF wraps Django request into Request
Authentication runs
Permission checks
Throttling checks
View logic executes
Serializer validation
Response rendered
Exception handling
Response returned
```

#### Q-9 Difference between APIView, GenericAPIView, and ViewSet ?
```bash
APIView: Full control, manual CRUD
GenericAPIView: Adds queryset, serializer, mixins
ViewSet: Groups multiple actions into one class
Use ViewSets for standard CRUD APIs.
```

#### Q-10 How does DRF handle serialization vs deserialization?
```bash
Serialization → Model → JSON
Deserialization → JSON → Python → Model
```

#### Q-11 How do you optimize serializer performance ?
```bash
Avoid SerializerMethodField
Use values() for read-only APIs
Preload related objects
Use to_representation() carefully
```

#### Q-12 How do you secure DRF APIs ?
```bash
Use HTTPS
Strong authentication
Permissions
Throttling
Input validation
```

#### Q-13 How do you design DRF APIs for scale ?
```bash
Stateless APIs
Caching
Pagination
Async tasks
Database indexing
```

#### Q-14 JWT Authentication ? 
```bash
pip install djangorestframework-simplejwt
```

#### Q-15 Create a Simple API View ?
```bash
Create a Simple API View
class HelloView(APIView):
    def get(self, request):
        return Response({"msg": "Hello"})

ModelSerializer Example
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = "__all__"
```

#### Q-16 API Is Slow in Production ? 
```bash
Use select_related / prefetch_related
Add caching
Use pagination
```

#### Q-17 Duplicate Records via API ?
```bash
Add DB constraints
Use unique=True
```

#### Q-18 API Returning Large Response ?
```bash
Pagination
Field limiting
```

#### Q-19 Need Background Processing ?
```bash
Use Celery.
```

#### Q-20 Need API Documentation ?
```bash
Use Swagger / OpenAPI.
drf-yasg
```