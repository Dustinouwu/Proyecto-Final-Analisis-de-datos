# Proyecto final análisis de datos

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

Puedes encontrar mucho más de cómo utilizar este proyecto en nuestra [Wiki](https://github.com/tu/proyecto/wiki)

## Versionado 📌

Usamos [SemVer](http://semver.org/) para el versionado. Para todas las versiones disponibles, mira los [tags en este repositorio](https://github.com/tu/proyecto/tags).

## Autores ✒️

_Menciona a todos aquellos que ayudaron a levantar el proyecto desde sus inicios_

* **Andrés Villanueva** - *Trabajo Inicial* - [villanuevand](https://github.com/villanuevand)
* **Fulanito Detal** - *Documentación* - [fulanitodetal](#fulanito-de-tal)

También puedes mirar la lista de todos los [contribuyentes](https://github.com/your/project/contributors) quíenes han participado en este proyecto. 

## Licencia 📄

Este proyecto está bajo la Licencia (Tu Licencia) - mira el archivo [LICENSE.md](LICENSE.md) para detalles

## Expresiones de Gratitud 🎁

* Comenta a otros sobre este proyecto 📢
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.
* etc.



---
⌨️ con ❤️ por [Villanuevand](https://github.com/Villanuevand) 😊

