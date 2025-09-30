Trabajaremos con Flask en Python para crear aplicaciones que interactúen con la base de datos.
Aprenderán a:
✅ Conectar backend con bases de datos
✅ Crear APIs básicas
✅ Desarrollar la lógica de interacción con datos

INTRODUCCION AL DESARROLLO BACKEND CON PYTHON Y FLASK
OBJETIVOS:
-Comprender qué es el desarrollo backend
-Conocer el rol de un framework web
-Instalar y configurar Flask

Funciones del Backend
Gestionar la logica de negocio de la aplicacion.
Procesar solicitudes desde el frontend.
Conectarse y administrar bases de datos.
Manejar la seguridad y la autenticación.
Comunicar diferentes servicios y APIs.

Componentes principales:
Servidor: Hardware o software que ejecuta la aplicacion backend.
Base de datos: Donde se almacenan y consultan los datos.
APIs: Interfaces que permiten la comunicación entre sistemas.
Lógica de negocio; Reglas que dictan el funcionamiento de la aplicación.

Tecnologias mas usadas
Lenguajes: JAVA, PYTHON, JAVASCRIPT (NODE.JS), PHP, C#
Bases de datos: MYSQL, POSTGRESQL, MONGODB
Frameworks: SPRING BOOT, DJANGO, EXPRESS.JS, LARAVEL
APIs: REST, GRAPHQL

BACKEND VS FRONTEND
FRONTEND: Lo que el usuario ve e interactua (interfaz grafica)
BACKEND: Lo que ocurre detrás de escena: logica, datos y reglas de negocio 

EJEMPLO: CUando un usuario inicia sesión en una aplicacion
el frontend envia el usuario y contraseeña
el backend verifica en la base de datos
si es correcto, genera un token de acceso y responde al frontend

Rutas y vistas en Flask 
Flask es un microframework para python que facilita la creacion de aplicaciones web ligeras, flexibles y escalables.

1. Abrir VS CODE

2. CREAR ARCHIVO APP.PY
3. EJECUTAR PIP INSTALL PYTHON

4. Escribir dentro del archivo:
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "¡Hola, Flask!"

if __name__ == "__main__":
    app.run(debug=True)


4. Luego en el terminal escribir: python app.py y dar clic en el enlace generado.
5. crear carpeta templates
6. crear carpeta static
7. crear archivo index.html
8. from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "¡Hola, Flask!"

DEBAJO SE ESCRIBE OTRO CODIGO PARA HACER OTRA PAGINA:
@app.route("/about")
def about():
    return "Acerca de nosotros"

Para colocar nombres
@app.route("/user/<nombre>")
def usuarios(nombre):
    return f"hola {nombre}"

Para colocar productos
@app.route("/productos/<producto>")
def productos(producto):
    return f"el producto {producto} no esta disponible"

Para colocar numeros y no letras (id es para que el usuario solo pueda introducir números:
@app.route("/post/<int:id>")
def post(id):
    return f"el id del post es {id}"

Para buscar un parametro, en la primera linea agregar from flask import request y luego:
@app.route("/search")
def search():
    q = request.args.get("q")
    h = request.args.get("h")
    return f"El parametro de busqueda es {q} y {h}"

    estas se llaman con URL tipo: /search?q=flask

Vistas que devuelven HTML:
from flask import url_for, redirect 
@app.route("/old")
def old():
    return redirect(url_for("about"))

Templates y Jinja2 en Flask
Que es jinja2? Es el motor de plantillas que usa flask para renderizar HTML dinámico
Permimte insertar variables de python en HTML

las variables {{}} se reemplazan con valores enviados desde flask
    
if __name__ == "__main__":
    app.run(debug=True)

|upper es para poner las lechas en mayuscula


HERENCIA DE PLANTILLAS



