# Volúmenes para persistir base de datos.
## 1.Titulo
Persistencia de datos en contenedores Docker: uso de volúmenes con PostgreSQL y pgAdmin4 en Play With Docker.
## 2. Tiempo de duración
Tiempo en minutos usados para desarrollar la práctica es de 120 minutos.
## 3. Fudamentos
Docker es una plataforma de contenedores que permite empaquetar aplicaciones y sus dependencias en un entorno portátil y aislado. Uno de los desafíos comunes al trabajar con contenedores es la persistencia de datos. Por defecto, los contenedores son efímeros, lo que significa que los datos se eliminan cuando un contenedor se detiene o se borra. Para solucionar esto, Docker ofrece el uso de volúmenes.
Los volúmenes permiten almacenar datos de forma persistente fuera del ciclo de vida del contenedor. Se almacenan en una ubicación controlada por Docker en el sistema host. Esto es especialmente útil al trabajar con bases de datos, como PostgreSQL.
PostgreSQL es un sistema de gestión de bases de datos relacional de código abierto. En esta práctica, se ejecutará PostgreSQL dentro de contenedores Docker en la plataforma Play With Docker (PWD), y se usará pgAdmin4 como cliente para conectarse, manipular y comprobar la persistencia de los datos.
### Docker ofrece tres tipos principales de almacenamiento:
- Volúmenes nombrados (Named Volumes)
- Volúmenes anónimos (Anonymous Volumes)
- Bind mounts
## 4. Conocmientos previos
Para completar esta práctica, el estudiante debe tener conocimientos en:
1. Manejo de navegador.
2. Comandos fundamentales de Docker.
3. Instalación y uso de clientes de base de datos como pgAdmin4.
4. Conceptos básicos de bases de datos relacionales y SQL.
## 5. Objetivo a alcanzar
1. Comprender la diferencia entre contenedores con y sin volúmenes en términos de persistencia de datos.
2. Crear y administrar contenedores PostgreSQL usando Docker.
3. Crear y administrar volúmenes en Docker.
4. Verificar la persistencia de una base de datos utilizando pgAdmin4 como herramienta cliente.
## 6. Eqipo necesario
1. Computador con sistema operativo Windows.
2. Navegador web moderno (Chrome, Firefox, etc.)
3. Acceso a la plataforma https://labs.play-with-docker.com.
4. Docker versión 20.x (PWD ya lo incluye).
5. pgAdmin4 (local o versión online).
## 7. Material de apoyo
1. Documentación oficial de Docker: https://docs.docker.com/storage/volumes/
2. Documentación de PostgreSQL: https://www.postgresql.org/docs/
3. Guía de la asignatura
4. Cheat Sheet de comandos Linux y Docker
## 8. procedimiento
### Parte 1: Base de datos sin volumen:
Paso 1: Ejecutar el contenedor sin volumen
´´´´
docker run --name server_db1 -e POSTGRES_PASSWORD=admin -p 5432:5432 -d postgres
´´´´
## 9. Resultados esperados
## 10. Bibliografía
