Incluir lo siguiente en INSTALLED_APPS

*'rest_framework',

-----Crear un entorno virtual-----
>virtualenv nombre_del_entorno
>cd bin
>source activate

-----Elementos necesarios para instalación-----
>pip install djangorestframework

-----Crear un projecto-----
>django-admin.py startproject nombre_del_proyecto

-----Correr el servidor-----
>python manage.py runserver

-----Ejecutar migraciones-----
>python manage.py migrate

-----Crear superusuario-----
>python manage.py createsuperuser

-----Crear una aplicación-----
>django-admin.py startapp nombre_aplicacion

Nota_1. Cuando crees una aplicación en django debes registarla
en tu archivo setting.py en INSTALLED_APPS 


-----Agregar un valor a created_at-----
>create_At = models.DateTimeField(auto_now = True)

-----Ejecutar un makemigration-----
python manage.py makemigrations nombre_de_la_app

-----Crear Endpoint-----
1. Crea un el urls.py file en tu Video app
2. Copy lo siguiente:

from .views import ListVideo
from django.conf.urls import url
urlpatterns = [
 url(r'^videos/$', ListVideo.as_view(), name='lista-video'),
]

3. Crear una clase para el endpoint

from django.shortcuts import render
from rest_framework.views import APIView
from rest_framework.response import Response
from .serializers import VideoSerializer

from .models import Video

class ListVideo(APIView):
 def get(self, request):
  videos = Video.objects.all()
  video_json = VideoSerializer(videos, many=True)
  return Response(video_json.data)

4. Decirle a nuestro servidor que utilize nuestro endpoint
4.1. Deberes de agregarlo en el urls.py file de la siguiente
manera

urlpatterns = [
 url(r'^api/v1/', include('video.urls')),
]

Nota_1. Serializable un objecto es transformar un objeto
para que pueda ser transportado en http(marshall)

-----Serializer-----
1. Crear un serializers.py file

from rest_framework import serializers
from .models import Video

class VideoSeriaizer(serializers.ModelSerializer)
 class Meta:
  model = Video
  fields = ('title', 'description')  



