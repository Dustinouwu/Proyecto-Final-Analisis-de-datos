# Proyecto final análisis de datos

### Autores ✒️

_Todos los colaboradores del proyecto desde sus inicios son:_

- [Dustin Chávez](https://github.com/Dustinouwu)
- [Steven Guañuna](https://github.com/Dustinouwu)
- [Miguel Muzo](https://github.com/Dustinouwu)
- [Kevin Pinanjota](https://github.com/Dustinouwu)

--- 

### Descripción 📄

El equipo de trabajo para el proyecto denominado data lake el cual tiene como objetivo la recolección de datos y evaluación para poder determinar varias conclusiones.

![image](https://user-images.githubusercontent.com/74844624/155891550-57279e29-faa4-44f5-97f7-dff2f2e23824.png)

---
## Content 🚀
- [Pre-requisitos](#Pre-requisitos)
	- [Bases SQL](#bases-sql)
	- [Bases NO SQL](#Bases-NO-SQL)
	- [Fuentes de internet](#Fuentes-de-internet)
	- [Otras](#Otras)
- [Twitter to CouchDB](#Twitter-to-CouchDB)
- [Webscraping to Neo4j](#Webscraping-to-Neo4j)
- [Facebook to CouchDB](#cFacebook-to-CouchDB)
- [Twitter to MongoDB](#Twitter-to-MongoDB)
- [Kaggle to MySQL](#Kaggle-to-MySQL)
- [INEC to SQL Server](#INEC-to-SQL-Server)
- [WebScraping to PostgreSQL](#WebScraping-to-PostgreSQL)
- [Datos abiertos to MySQL](#Datos-abiertos-to-MySQL)


## Pre-requisitos 📋

_Para poder desarrollar el proyecto es necesario instalar las bases de datos y un ID en donde se vaya a ejecutar el script realizado en python_

### Bases SQL 

- Mysql: Una de las bases de datos más utilizadas de código abierto, para entornos de desarrollo web.  

- Sql lite: Sistema gestor de base de datos relacional, relativamente pequeña y además de código abierto. 

- Sql server: El lenguaje de desarrollo utilizado es Transact-SQL, una implementación del estándar ANSI del lenguaje SQL, utilizado para manipular y recuperar datos, tablas y definir relaciones entre ellas. 


 ### Bases NO SQL 

- CouchDB: Gestor de base de datos cuyo foco está puesto en la facilidad de su uso y en ser “una base de datos que asume la web de manera completa”. 

- Neon4J: Base de datos orientada a grafos, se describe como un motor de persistencia embebido, que almacena datos estructurados en lugar de tablas.  

- MongoDB: Es un sistema de base de datos orientado a documentos y a la vez de código abierto, también tiene distinta forma de guardar datos, especialmente guarda estructuras de datos BSON con un esquema dinámico. 

- MongoDB – Atlas: Trata del mismo concepto que la base de datos MongoDB, pero con la gran diferencia que esta se encuentra en la nube, haciéndola más efectiva al momento de hacer trabajos con muchas personas. 
 ### Fuentes de internet:  
- Facebook: Red social creada con el propósito a mantener contacto con personas a largas o cortas distancias, compartiendo diferente contenido, ya sea audiovisual, información, etc. 
- Twitter: Red social de microblogging, con un servicio de comunicación bidireccional con el que se puede llegar a compartir información de diverso tipo de forma rápida. 
### Otras:  
- Pycharm: Es un entorno de desarrollo integrado utilizado en la programación de computadoras, específicamente para el lenguaje Python. Está desarrollado por la empresa checa JetBrains. 
- PowerBI: Servicio de análisis de datos desarrollada por Microsoft, creado con la intención de proporcionar visualizaciones que logren ser interactivas y con capacidades de inteligencia empresarial. 


## Twitter To CouchDB

_Una serie de ejemplos paso a paso que te dice lo que debes ejecutar para tener un entorno de desarrollo ejecutandose_

_Dí cómo será ese paso_

```
Da un ejemplo
```

_Y repite_

```
hasta finalizar
```

_Finaliza con un ejemplo de cómo obtener datos del sistema o como usarlos para una pequeña demo_

## Webscraping to Neo4j

```
Da un ejemplo
```

_Explica como ejecutar las pruebas automatizadas para este sistema_

## Facebook to CouchDB

_Explica que verifican estas pruebas y por qué_

```
Da un ejemplo
```

## Twitter to MongoDB

_Explica que verifican estas pruebas y por qué_

```
Da un ejemplo
```

## Kaggle to MySQL

_Agrega notas adicionales sobre como hacer deploy_

## INEC to SQL Server

_Menciona las herramientas que utilizaste para crear tu proyecto_

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - El framework web usado
* [Maven](https://maven.apache.org/) - Manejador de dependencias
* [ROME](https://rometools.github.io/rome/) - Usado para generar RSS

## WebScraping to PostgreSQL

Por favor lee el [CONTRIBUTING.md](https://gist.github.com/villanuevand/xxxxxx) para detalles de nuestro código de conducta, y el proceso para enviarnos pull requests.

## Datos abiertos to MySQL

Extraeremos el archivo estático desde la página del gobierno “DATOS ABIERTOS”, específicamente el tema de “personas perdidas”. 
[Datos abiertos](https://datosabiertos.gob.ec/)

![image](https://user-images.githubusercontent.com/74982150/155870656-476c702c-dd07-4462-831d-73d24416778a.png)

- Procedimiento

Importaremos algunas librerías para poder realizar tanto la conexión para la base de datos MYSQL y poder leer el archivo que vamos a extraer de las páginas de archivos estáticos.

```py
import mysql.connector as msql
import pandas as pd
from sqlalchemy import create_engine
```

Establecemos el nombre del host, el usuario y la contraseña de nuestro servidor de MYSQL, y posteriormente realizaremos esta conexión mediante un if, identificaremos si dicha conexión es exitosa o no, además de crear una variable para poder realizar las operaciones en lenguaje SQL en Python.

```py
connections = msql.connect(host = 'localhost', user = 'root', password='123456')
if connections.is_connected():
    cursor = connections.cursor()
    print("Conexión Exitosa")
else:
    print("Conexión Rechazada")
```

Con la variable antes mencionada, crearemos mediante lenguaje SQL, una nueva base de datos dentro de MYSQL con la siguiente línea:

```py
cursor.execute("CREATE DATABASE PersonasPerdidas;")
```

Crearemos una consulta para poder demostrar que la base de datos “PersonasPerdidas” se haya creado dentro de la base de datos de MYSQL.

```py
consulta = pd.read_sql("show databases;",connections)
consulta
```

Estableceremos la conexión hacia MYSQL desde Python, añadiendo el usuario, contraseña y por ultimo la base de datos que vamos a utilizar en este caso “PersonasPerdidas”

```py
engine = create_engine('mysql+mysqldb://root:123456@localhost:3306/PersonasPerdidas')
consulta
```

Cargaremos a la variable “df” gracias a la librería de pandas, el documento que extrajimos de la página de archivos estáticos mediante la extensión csv, también para poder leer este archivo hemos necesitado declarar el tipo de separador que utiliza nuestro archivo, caso contrario las columnas al momento de extraer se unen, adicionalmente utilizaremos ecoding para poder leer este archivo y para que no existan errores dentro de la lectura del archivo.

```py
df = pd.read_csv("mdg_personasdesaparecidas_pm_2021_enero_diciembre.csv", sep=";" ,encoding='latin-1')
```

Como último paso, añadiremos la variable que ya contiene el archivo, crearemos la tabla que va ir en la base de datos, en este caso con el nombre de “información”, añadiremos la conexión previamente creada y pasaremos toda la información del archivo CSV  a la base de datos de MYSQL.

```py
try:
    df .to_sql('información', con=engine, if_exists = 'replace', index = False)
    print("creación y almacenamiento completados")
except Exception as e:
    print(e)
```

![image](https://user-images.githubusercontent.com/74982150/155870977-b0c469a5-9d8e-4f3b-a454-8634b177adf5.png)

![image](https://user-images.githubusercontent.com/74982150/155870981-8567f4e5-61fe-419d-ba3b-c550f0a16c32.png)

Puedes encontrar mucho más de cómo utilizar este script en [ARCHIVO ESTÁTICO A MYSQL](https://github.com/tu/proyecto/wiki)

---

### MYSQL A MONGODB-ATLAS

Utilizaremos las siguientes librerías para poder realizar esta transición entre base de datos.

```py
from argparse import ArgumentParser
from pymongo import MongoClient
from pymongo.errors import ConnectionFailure
import mysql.connector as msql
import pandas as pd
from sqlalchemy import create_engine
import certifi
import numpy as np
```

Crearemos la conexión hacia MONGODB ya establecido como conectador de datos, añadiendo que en este caso se va a tratar de MONGODB -ATLAS, para esto utilizaremos el clouster en el MONGODB en la nube, comprobaremos el éxito de esta conexión, y adicionalmente crearemos el nombre de la base de datos y colección para MONGODB y guardándolos en distintas variables.

```py
try:
    ca = certifi.where()
    client = MongoClient('mongodb+srv://miguel:miguel@cluster0.ed8kj.mongodb.net/test', tlsCAFile=ca )

    client.server_info()
    print("Conexion exitosa")
    client.close
except pymongo.errors.ServerSelectionTimeoutError as errorTiempo:
    print("Conexión rechazada")
dbm = client['Mysql_to_Mongodb']
cole = dbm['Datos_de_SQL']
```

Volveremos a establecer la conexión hacia MYSQL.

```py
engine = create_engine('mysql+mysqldb://root:123456casa@localhost:3306/PersonasPerdidas')
```

```py
connections = msql.connect(host = 'localhost', user = 'root', password='123456', database ='PersonasPerdidas')
if connections.is_connected():
    cursor = connections.cursor()
    cursor.execute("select database();")
    record = cursor.fetchone()
    print("Se conectó a la base de datos: ", record)
```

Crearemos el dataframe para poder pasar hacer la trasición de MYSQL hacia MONGODB, almacenaremos todo esto en una lista, para posteriormente mediante append para ir almacenando los múltiples datos y pasarlos hacia MONGODB-ATLAS.

```py
def createDocsFromDF(documento, collection = None, insertToDB=False):
    docs = []
    fields = [col for col in documento.columns]
    for i in range(len(documento)):
        doc = {col:documento[col][i] for col in documento.columns if col != 'index'}
        for key, val in doc.items():
            if type(val) == np.int64:
                doc[key] = int(val)
            if type(val) == np.float64:
                doc[key] = float(val)
            if type(val) == np.bool_:
                doc[key] = bool(val)
        docs.append(doc) 
    if isinstance(docs, list): 
        cole.insert_many(docs)   
    else: 
        cole.insert_one(docs)
    print("guardado exitosamente")    
    return docs 
```


```py
createDocsFromDF(documento)
```

```py
guardado exitosamente
Output exceeds the size limit. Open the full output data in a text editor

[{'Provincia': 'PICHINCHA',
  'Latitud': '-0,156852339',
  'Longitud': '-78,47783944',
  'Edad Aprox.': 29,
  'Sexo': 'HOMBRE',
  'Motivo Desaparción': 'PROBLEMAS SOCIALES',
  'Motivo Desaparción Obs.': 'INFLUENCIA DE AMISTADES',
  'Fecha Desaparición': '6/8/2021',
  'Situación Actual': 'ENCONTRADO',
  'Fecha Localización': '8/8/2021',
  '_id': ObjectId('621713c7f07d4a11cc5add7e')},
 {'Provincia': 'MORONA SANTIAGO',
  'Latitud': '-2,0021974',
  'Longitud': '-77,9967043',
  'Edad Aprox.': 15,
  'Sexo': 'MUJER',
  'Motivo Desaparción': 'PROBLEMAS SOCIALES',
  'Motivo Desaparción Obs.': 'INFLUENCIA DE AMISTADES',
  'Fecha Desaparición': '15/7/2021',
  'Situación Actual': 'ENCONTRADO',
  'Fecha Localización': '9/8/2021',
  '_id': ObjectId('621713c7f07d4a11cc5add7f')},
 {'Provincia': 'AZUAY',
  'Latitud': '-2,882362',
  'Longitud': '-79,0589399',
  'Motivo Desaparción Obs.': 'FAMILIA DISFUNSIONAL',
  'Fecha Desaparición': '13/6/2021',
  'Situación Actual': 'ENCONTRADO',
  'Fecha Localización': '16/6/2021',
  '_id': ObjectId('621713c7f07d4a11cc5ae165')},
 ...]
```

Puedes encontrar mucho más de cómo utilizar este script en nuestra [MYSQL A MONGODB-ATLAS](https://github.com/tu/proyecto/wiki)

--- 

### ANÁLISIS EN POWERBI
Se realizó en el análisis del tema seleccionado “personas desaparecidas”, analizando primero la cantidad de personas desaparecidas por provincia, destacando en ella que las principales provincias que tienen un mayor número de casos son las del Guayas y Pichincha, esto se debe a que son provincias muy pobladas y por ende el número siempre va a ser alto a diferencia de otras provincias, otro punto a destacar es la provincia de Galápagos, que al ser una zona netamente turística tiene un gran control por lo no tiene mucha probabilidad de que una persona se pierda.

![image](https://user-images.githubusercontent.com/74982150/155871162-bdef92bf-0fd5-44d4-9056-879fb6ccecab.png)

Tendremos un segundo análisis sobre la cantidad de personas desaparecidas, mediante su tipo de género, en este caso, tendremos una gran diferencia entre hombres y mujeres, siendo así la cantidad de mujeres que desaparecen superó por mas de un 50% a los hombres durante el año 2021 en todas las provincias del Ecuador, siguiendo con el análisis tendremos la fecha en la cuál las personas desaparecen igualmente por provincias, y por último tendremos la razón por la cuál se da esta situación, destacando dos que son las que tienen más porcentaje, estos serían problemas familiares y problemas sociales, seguidos de otro porcentaje alto en gente que no se pudo reportar el motivo. 

![image](https://user-images.githubusercontent.com/74982150/155871184-daf57eec-c10e-4759-851c-370cf333bd9f.png)


En conclusión las personas tienden a desaparecer por motivos financieros, problemas sociales pero principalmente por problemas familiares, dentro de estos casos tenemos que las mujeres suelen ser las que tienen una mayor taza de desaparición, por otro lado tenemos una gran cantidad de estas que han sido encontradas y es un punto positivo teniendo un porcentaje muy bajo en personas que aún no han sido encontradas y aún menor en personas fallecidas.

![image](https://user-images.githubusercontent.com/74982150/155871191-548461b8-edb3-4390-a87b-9b2a0416b285.png)

![image](https://user-images.githubusercontent.com/74982150/155871199-de41546a-ac27-49db-95d5-a4ef4de24128.png)


## Versionado 📌

Usamos [SemVer](http://semver.org/) para el versionado. Para todas las versiones disponibles, mira los [tags en este repositorio](https://github.com/tu/proyecto/tags).


## Licencia 📄

Este proyecto está bajo la Licencia (Tu Licencia) - mira el archivo [LICENSE.md](LICENSE.md) para detalles

## Expresiones de Gratitud 🎁

* Comenta a otros sobre este proyecto 📢
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.
* etc.



---
⌨️ con ❤️ por [Villanuevand](https://github.com/Villanuevand) 😊

