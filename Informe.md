# Volúmenes para persistir base de datos.
## 1.Titulo:
Persistencia de datos en contenedores Docker: uso de volúmenes con PostgreSQL y pgAdmin4 en Play With Docker.
## 2. Tiempo de duración:
Tiempo en minutos usados para desarrollar la práctica es de 120 minutos.
## 3. Fudamentos:
Docker es una plataforma de contenedores que permite empaquetar aplicaciones y sus dependencias en un entorno portátil y aislado. Uno de los desafíos comunes al trabajar con contenedores es la persistencia de datos. Por defecto, los contenedores son efímeros, lo que significa que los datos se eliminan cuando un contenedor se detiene o se borra. Para solucionar esto, Docker ofrece el uso de volúmenes.
Los volúmenes permiten almacenar datos de forma persistente fuera del ciclo de vida del contenedor. Se almacenan en una ubicación controlada por Docker en el sistema host. Esto es especialmente útil al trabajar con bases de datos, como PostgreSQL.
PostgreSQL es un sistema de gestión de bases de datos relacional de código abierto. En esta práctica, se ejecutará PostgreSQL dentro de contenedores Docker en la plataforma Play With Docker (PWD), y se usará pgAdmin4 como cliente para conectarse, manipular y comprobar la persistencia de los datos.
### Docker ofrece tres tipos principales de almacenamiento:
- Volúmenes nombrados (Named Volumes)
- Volúmenes anónimos (Anonymous Volumes)
- Bind mounts
## 4. Conocmientos previos:
Para completar esta práctica, el estudiante debe tener conocimientos en:
1. Manejo de navegador.
2. Comandos fundamentales de Docker.
3. Instalación y uso de clientes de base de datos como pgAdmin4.
4. Conceptos básicos de bases de datos relacionales y SQL.
## 5. Objetivo a alcanzar:
1. Comprender la diferencia entre contenedores con y sin volúmenes en términos de persistencia de datos.
2. Crear y administrar contenedores PostgreSQL usando Docker.
3. Crear y administrar volúmenes en Docker.
4. Verificar la persistencia de una base de datos utilizando pgAdmin4 como herramienta cliente.
## 6. Eqipo necesario:
1. Computador con sistema operativo Windows.
2. Navegador web moderno (Chrome, Firefox, etc.)
3. Acceso a la plataforma https://labs.play-with-docker.com.
4. Docker versión 20.x (PWD ya lo incluye).
5. pgAdmin4 (local o versión online).
## 7. Material de apoyo:
1. Documentación oficial de Docker: https://docs.docker.com/storage/volumes/
2. Documentación de PostgreSQL: https://www.postgresql.org/docs/
3. Guía de la asignatura
4. Cheat Sheet de comandos Linux y Docker
## 8. Procedimiento:
## Parte 1: Base de datos sin volumen.
###  Crear contenedor PostgreSQL:
En el terminal de Play With Docker (PWD):
```
docker run --name server_db1 -e POSTGRES_PASSWORD=1234 -p 5432:5432 -d postgres
````
### Evidencia:
<imag!![in3](https://github.com/user-attachments/assets/95afa96b-236e-428e-9332-79a6935102c3)

### Crear base de datos y tabla:
Desde pgAdmin:
1. Crear una base de datos llamada test.
2. Dentro de test, crear una tabla customer con los campos:
- id (tipo integer, primary key)
- fullname (tipo text)
- status (tipo text)
Insertar un registro de prueba, por ejemplo:
```
INSERT INTO customer (id, fullname, status) VALUES (1, 'Juan Pérez', 'activo');
````
### Evidencia:
<imag!![in3 1](https://github.com/user-attachments/assets/875e4908-1e49-40ac-ab17-ec984677aeeb)

<imag!![in3 2](https://github.com/user-attachments/assets/70e207ec-f174-4047-a996-1759da9fbbd7)
<imag!![in3 3](https://github.com/user-attachments/assets/378f07ac-fb45-4950-9d9b-a6e6bcaea71c)
<imag!![in3 4](https://github.com/user-attachments/assets/bbb9eee7-f9d8-4944-82c1-f15bc7fac5cd)
<imag!![in3 5](https://github.com/user-attachments/assets/a7d88140-12b6-406d-a0a3-04b92cc92861)
<imag!![in3 6](https://github.com/user-attachments/assets/5963b939-7fb4-410b-b8f1-469facac3121)
<imag!![in3,7](https://github.com/user-attachments/assets/941e35a3-6196-440f-b060-d121b1833d91)
<imag!![in3 8](https://github.com/user-attachments/assets/87d21574-5e30-4cf8-a61f-1ace36612a71)

### Eliminar el contenedor:
Vuelve a la terminal de PWD:
```
docker stop server_db1
docker rm server_db1
````
### Evidencia:
<imag!![in3 9](https://github.com/user-attachments/assets/58543d3d-f200-4699-9a59-6443bf89d137)

### Volver a crear el contenedor:
Cuando conectamos nuevamente con pgAdmin4. Veremos que la base de datos test y la tabla customer ya no existen. Esto demuestra que sin volumen, los datos no persisten.
```
docker run --name server_db1 -e POSTGRES_PASSWORD=1234 -p 5432:5432 -d postgres
````
### Evidencia:
<imag!![in3 10](https://github.com/user-attachments/assets/fbdc6225-f58c-40a7-a48c-7d51cc1e8336)

## Parte 2: Base de datos con volumen:
### Crear un volumen:
```
docker volume create pgdata
````
### Evidencia:
<imag!![in3 2 1](https://github.com/user-attachments/assets/c0db1d74-084b-4776-b177-ae50bd913e11)

### Crear el contenedor asociado al volumen:
```
docker run --name server_db2 -e POSTGRES_PASSWORD=1234 -v pgdata:/var/lib/postgresql/data -p 5433:5432 -d postgres
````
### Evidencia:
<imag!![in3 2 3](https://github.com/user-attachments/assets/ef432047-448f-474a-84fe-8a86733439f6)

### Crear base de datos y tabla igual que antes:
- Base de datos: test.
- Tabla: customer con los mismos campos.
Inserta un registro por ejemplo:
```
INSERT INTO customer (id, fullname, status) VALUES (1, 'Ana Gómez', 'activo');
````
### Evidencia:
<imag!![in3 4](https://github.com/user-attachments/assets/5c9c222e-4a36-4e24-af42-9306844ad059)

<imag!![in3 4 1](https://github.com/user-attachments/assets/7eda4fac-ea36-404c-a9f1-a890bcb9ac12)

<imag!![in3 4 3](https://github.com/user-attachments/assets/6ca578a0-be1a-45d4-b8c9-b4a274087153)

<imag!![in3 4 4](https://github.com/user-attachments/assets/8c9d4c30-892b-4741-b309-8bd950772b92)

<imag!![in3 4 5](https://github.com/user-attachments/assets/6f06eeba-1b8a-4105-a559-57690224b4af)

<imag!![in3 4 6](https://github.com/user-attachments/assets/0cfe99ca-e7e8-4768-a5a9-517d855f79fe)

<imag!![in3 4 7](https://github.com/user-attachments/assets/2db3799a-964f-4755-afff-06f26842d46a)

### Detener y eliminar el contenedor:
```
docker stop server_db2
````
```
docker rm server_db2
````
### Evidencia:
<imag!![in3 4 2 1](https://github.com/user-attachments/assets/bfb7797c-6a61-4110-b3ab-19d8961b0a3e)

### Volver a crear el contenedor usando el mismo volumen:
```
docker run --name server_db2 -e POSTGRES_PASSWORD=1234 -v pgdata:/var/lib/postgresql/data -p 5433:5432 -d postgres
````
### Evidencia:
<imag!![in3 5 1](https://github.com/user-attachments/assets/63a28fe8-ee23-4f66-b160-fc9e25b5678a)

### Conectarse otra vez desde pgAdmin4
Verificar que la base de datos test y la tabla customer con su registro siguen existiendo. Esto demuestra que con volúmenes, los datos persisten incluso si el contenedor se elimina.
### Evidencia:
<imag!![in3 3 8](https://github.com/user-attachments/assets/85cf0086-0d35-4621-9914-aa163a96e9e2)

<imag!![in3 3 8 1](https://github.com/user-attachments/assets/e421e469-c4ce-4197-ac94-feb03a43d826)

## 9. Resultados esperados:
### Parte 1: Sin Volumen (Sin Persistencia).
En esta parte, al crear el contenedor server_db1 sin asociar un volumen, se realizó la creación de la base de datos test y la tabla customer, con un registro insertado en dicha tabla. Sin embargo, al detener y eliminar el contenedor, los datos fueron perdidos. Al recrear el contenedor, la base de datos test y la tabla customer ya no existían, lo que demuestra que sin volúmenes asociados, los datos no persisten tras la eliminación del contenedor.
<imag!![resultado 1](https://github.com/user-attachments/assets/a8a08e0a-9537-49d4-88fe-0fd551d7450f)

### Parte 2: Con Volumen (Con Persistencia).
En la segunda parte, se creó el contenedor server_db2 con un volumen pgdata asociado. Los datos se almacenaron en el volumen, y al eliminar el contenedor, el volumen permaneció intacto. Al recrear el contenedor y volver a asociar el volumen, los datos, incluida la base de datos test y la tabla customer, se mantuvieron, demostrando que los volúmenes aseguran la persistencia de los datos.
<imag!![resultado 2](https://github.com/user-attachments/assets/20b90a01-e414-4ee7-a43b-87529ce3e601)

## 10. Bibliografía: 
Docker, Inc. (2025). Docker documentation: Volumes. https://docs.docker.com/storage/volumes/
The PostgreSQL Global Development Group. (2025). PostgreSQL documentation. https://www.postgresql.org/docs/
Docker, Inc. (2025). Docker Cheat Sheet. https://www.docker.com/cheatsheet/


