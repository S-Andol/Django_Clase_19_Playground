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