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
$ poetry run django-admin.py startproject djangodemo
$ poetry shell
>> python manage.py startapp catalog
```
in setting.py json; INSTALLED APPS end put:
```python
'catalog.apps.CatalogConfig', 
```
in DATABASES update to:
```python
'default': {
    'ENGINE': 'django.db.backends.mariadb',
    'NAME': 'teste',
    'USER': 'root',
    'PASSWORD': 'toor',
    'HOST': 'localhost',
    'PORT': '3306',
}
```
in TIMEZONE update to:
```python
TIME_ZONE = 'America/Sao_Paulo'
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
