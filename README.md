# Django_Clase_19_Playground

# REPASO
Siempre crear las 3 patas
. Template
. Views
. Urls

# Cargar todo pero desde RENDER
En vez de usar el loader desde django.template
Vamos a usar render y asi bajamos los codigos a utilizar.

Colocamos en views 
    from django.shortcuts import render

# solo hacemos un diccionario y un return

def prueba_render(request):
    datos = {'nombre':'Pepe'}
    return render(request, r'inicio/prueba_render.html', datos) 


Y listo se redujo un monton de codigo...

# Recomendacion

Siempre tener la carpeta templates por fuera y al mismo nivel. Para lo que es relacionado al proyecto (para uso de todo la aplicacion)
Y usar templant en cada app por separado. VER APP_DIRS: true, junta todo  / unifica todo por dentro desde afuera (?)

Django cuando le dijimos en setting que busque en la BD 'templates', entonces cuando necesito informacion, va a buscarla en todos los lugares que digan templates de todos lados del proyecto y los unifica. POR ESO TRATAR DE NO TENER EL MISMO NOMBRE, YA QUE PUEDE GENERAR ERRORES

# Mover los templates
Movemos todos los templates de la app inicio a la carpeta inicio-->templates(que creamos)

# Crear carpetas dentro de templates
Podemos crear carpetas de las diferentes app que vamos a trabajar pero dentro de la carpeta templates
OJO, si se hace eso, pero antes estaba programado para que lo busque solo de templates, entonces hay que modificar todo.
Ejemplo en Views.py buscar en:
template = loader.get_template(r'mostrar_fecha.html')

y cambiarlo por 
template = loader.get_template(r'inicio/mostrar_fecha.html')


# Comenzando con Bootstrap
Descargamos un archivo .zip de la pagina https://startbootstrap.com/theme/landing-page

# Creamos static
Creamos una carpeta que se llama static dentro de la carpeta inicio

# Pegamos en static
Solo agarramos de nuestro archivo .zip las carpetas y archivos
assets
css
js
index.html

Los pegamos en la carpeta static
STATIC es porque en setting vemos que lo tomo como STATIC_URL = 'static/'

Son los que realmente nos importan

# Movemos Index.html
Sacamos index.html de static y lo colocamos en templates
Al hacer esto debemos modificar la funcion de mi_vista.

def mi_vista(request):
    print('Pase por aca!!! REY') #sale en la terminal, en el momento en que se ejecute
    # return HttpResponse('<h1>Mi Primera Vista</h1>')
    return render(request,'inicio/index.html')

# Cargue de paguina
Vemos que nos carga la imagen pero nos faltan todos los estilos
Para eso "cargamos" static agregando al hmtl indel esto:

{% load static %}

En esta ubcicacion

<html lang="en">
    {% load static %}
    <head>

Y modificamos 
<link href="css/styles.css" rel="stylesheet" />

Por 

<link href= {% static 'css/styles.css' %} rel="stylesheet" />

Tambien debemos modificar los de JS

En index esta:

<script src="js/scripts.js"></script>

Y lo modificamos por:

<script src={% static 'js/scripts.js' %}></script>

# Nos recomienda volver a hacer una carpeta inicio para evitar la busqueda erronea de archivos
Creamos una carpeta inicio dentro de static y movemos todo para ahi adentro.
Pero si hacemos eso, debemos cambiar el link y el script del paso anterior

<link href= {% static 'inicio/css/styles.css' %} rel="stylesheet" />
<script src={% static 'inicio/js/scripts.js' %}></script>

# hacer que aparezcan las imagenes
Hacer lo mismo, tenes que cambiar la direccion a {% static "inicio/..." %}
Con las partes que tenga que modificarse: por ejemplo
<img class="img-fluid rounded-circle mb-3" src={% static "inicio/assets/img/testimonials-1.jpg" %}   alt="..." />