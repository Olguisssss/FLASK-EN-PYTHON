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

1/10/2025 

¿QUÉ ES UN CRUD?
CRUD SIGNIFICA CREATE, READ, UPDATE, DELETE. Es el conjunto de operaciones basicas que se realizan sobre una base de datos
CREATE: INSERTAR NUEVOS REGISTROS
READ: CONSULTAR DATOS EXISTENTES
UPDATE: MODIFICAR REGISTROS
DELETE: ELIMINAR REGISTROS

PARA CONECTAR CON LA BASE DE DATOS EN EL TERMINAL DE VISUAL STUDIO CODE:
pip install mysql-connector-python

se crea un nuevo archivo llamado dbtest.py 
y se escribe el siguiente codigo reemplazando los valores segun mi base de datos:

import mysql.connector

def get_connection():
    return mysql.connector.connect(
        host="localhost",
        user="root",
        password="root"
        database="classicmodels"
    )

esta función devuelve una conexión lista para usar en las operaciones CRUD

CREATE - INSERTAR UN CLIENTE:
import mysql.connector

def get_connection():
    return mysql.connector.connect(
        host="localhost",
        user="root",
        password="root",
        database="classicmodels"
    )

def crear_customer(customerNumber, customerName, contactLastName, contactFirstName, phone, addressLine1, city, country):
    conn = get_connection()
    cursor = conn.cursor()
    sql = """INSERT INTO customers (customerNumber, customerName, contactLastName, contactFirstName, phone, addressLine1, city, country) VALUES (%s, %s, %s, %s, %s, %s, %s, %s)"""
    values = (customerNumber, customerName, contactLastName, contactFirstName, phone, addressLine1, city, country)
    cursor.execute(sql, values)
    conn.commit()
    last_id = cursor.lastrowid
    cursor.close()
    conn.close()
    return last_id

id = 497
empresa = "nueva empresa talentotech"
nombre = "olga"
apellido = "torres"
telefono = "3134445731"
direccion = "cll 68 # 27-84"
ciudad = "bucaramanga"
pais = "colombia"
print(crear_customer(id,empresa,nombre,apellido,telefono,direccion,ciudad,pais))

luego en ejecutar se pone: python dbtest.py y se guardan los datos en la BD de MySQL

READ - CONSULTAR:
def obtener_productos():
    conn = get_connection()
    cursor = conn.cursor(dictionary=True)
    cursor.execute("select * from productos")               PARA CONSULTAR TODOS LOS PRODUCTOS
    rows = cursor.fetchall()
    cursor.close()
    conn.close()
    return rows                                        

def obtener_productos(id):
    conn = get_connection()
    cursor = conn.cursor(dictionary=True)
    cursor.execute("select * from productos where idproductos=%s", (id,))            PARA CONSULTAR UN SOLO PRODUCTO POR SU ID
    rows = cursor.fetchone()
    cursor.close()
    conn.close()
    return rows

UPDATE - MODIFICAR

def actualizar_productos(idproductos, nombre, precio, descripcion, lote, unidades_disponibles):
    conn = get_connection()
    cursor = conn.cursor()
    values = (nombre, precio, descripcion, lote, unidades_disponibles, idproductos)
    cursor.execute("update productos set nombre=%s, precio=%s, descripcion=%s, lote=%s, unidades_disponibles=%s where idproductos=%s", values)    *##IMPORTANTE PONER EL WHERE AL FINAL EN EL ID*
    conn.commit()
    cursor.close()
    conn.close
    return "producto actualizado" 

nombre = "polvo compacto"
precio = "16000"
descripcion = "polvo compacto color piel con filtro solar"
lote = "045"
unidades_disponibles = "57"
id = 1

print(actualizar_productos(id, nombre, precio, descripcion, lote, unidades_disponibles))

DELETE - ELIMINAR

def eliminar_productos(idproductos):
    conn = get_connection()
    cursor = conn.cursor()
    values = (idproductos,)
    cursor.execute("delete from productos where idproductos=%s", values)
    conn.commit()
    cursor.close()
    conn.close
    return "producto eliminado" 

print(eliminar_productos(4))


METODO PARA CREAR, LEER, ACTUALIZAR O ELIMINAR

while True:
    opcion = input("ingrese una opcion crear, leer, actualizar o eliminar")
    if opcion == "crear":
        print("ingrese los datos del producto")
        nombre = input("ingrese el nombre del producto")
        precio = input("ingrese el precio")
        descripcion = input("ingrese una descripcion del producto")
        lote = input("ingrese el lote del producto")
        unidades_disponibles = input("ingrese las unidades disponibles del producto")
        id = crear_productos(nombre,precio,descripcion,lote,unidades_disponibles)
        print(f"se creo el producto con id {id}")
    if opcion == "leer":
        print("estos son los productos")
        productos = obtener_productos()
        for producto in productos:
            print(producto)


