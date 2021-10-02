![Z(i,j)=X(i,k) * Y(k, j); k=1 to n](http://www.sciweavers.org/tex2img.php?eq=Z_i_j%3D%5Csum_%7Bi%3D1%7D%5E%7B10%7D%20X_i_k%20%2A%20Y_k_j&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=)

# django-blog
django blog

create a new project
`$ poetry new <project-name>`

to use python 3.9 virtual env
`$ python env use 3.9`

activate env
`$ poetry shell`

install django framework
`$ poetry add django@latest`


or

```bash
$ mkdir <project-name>
$ cd <project-name>
$ poetry init --no-interaction --dependency django
$ poetry install
$ poetry run django-admin startproject <project-name>
$ poetry shell
>> python manage.py startapp <app-name>
```
in setting.py json; INSTALLED APPS end put:
```python
'catalog.apps.CatalogConfig', 
```
in DATABASES update to:
```python
'default': {
    'ENGINE': 'django.db.backends.mysql',
    'NAME': 'teste',
    'USER': 'root',
    'PASSWORD': 'toor',
    'HOST': 'localhost',
    'PORT': '3306',
}
or the default sqlite3
'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': 'mydatabase',
    }
```
in TIMEZONE update to:
```python
TIME_ZONE = 'America/Sao_Paulo'
# and language code
# LANGUAGE_CODE = 'pt-br'
```
others to change in future is
```python
SECRET_KEY =
```
for production
and 
```python
DEBUG = True 
```
just in development

To add routes to an app:
```python
# in urls.py
# Use include() to add paths from the catalog application
from django.conf.urls import include
from django.urls import path

urlpatterns += [
    path('catalog/', include('catalog.urls')),
]
```

sei praq n mas adiciona no final do arquivo tbm
para redirecionar a base url pra o app criado em /catalog/
```python
#Add URL maps to redirect the base URL to our application
from django.views.generic import RedirectView
urlpatterns += [
    path('', RedirectView.as_view(url='/catalog/')),
]
```

TO RUN/START DEV SERVER
in env shell put
```bash
python manage.py runserver
```

if you want to serve static files in development
```python
# Use static() to add url mapping to serve static files during development (only)
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

create a urls.py file in your app and put:
```python
from django.urls import path
from catalog import views


urlpatterns = [

]
```
and run it in env to migrate models to database:
```bash
>> python3 manage.py makemigrations
>> python3 manage.py migrate
```
ATENÇÃO: Você precisará executar os comandos acima sempre que alterar seus models de uma forma que afete a estrutura de dados que precisa ser armazenada (incluindo adição e remoção de todos models e campos individuais)

O comando makemigrations cria (mas não aplica) as migrações para todos aplicativos instalados em seu projeto (você pode especificar o nome do aplicativo para executar apenas uma migração para um único projeto). Isso te permite checar o código para essas migrações antes delas serem aplicadas — quando você é experiente em Django, você pode escolher ajustá-los um pouco!

O comando migrate aplica as migrações em seu banco de dados (Django rastreia quais foram adicionados ao banco de dados atual).

to create a user to login in django admin route
(in enviroment)
```bash
>> python manage.py createsuperuser
```

VIEWs

to use views to render html create a directory called `templates/` with a `index.html` file in your app
and a route to work 
```python
def home(request, name):
    return render(request, 'index.html')
```
