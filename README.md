# NUTRITION API- Arquitectura Hexagonal



<img src="./images/logo.jpg" alt="Logo"  height="300" />

## Descripción
**Nutrition API** es un proyecto personal que implementa una **API REST de nutrición** usando **arquitectura hexagonal**.  
Permite generar menús y sugerencias nutricionales en base a ingredientes o restricciones del usuario. La API está preparada para integrar en el futuro un motor de IA (ej. ChatGPT) para generar recetas dinámicas.

El objetivo del proyecto es mostrar buenas prácticas de diseño, separación de capas y clean code en un microservicio real.

---

## Arquitectura

El proyecto sigue la **arquitectura hexagonal**, con separación clara entre dominio, casos de uso y adaptadores:


```java

       +-------------------+
       |   Controller /    |
       |   REST Adapter    |
       +---------+---------+
                 |
      +----------v----------+
      |  Application / Use  |
      |       Cases         |
      +----------+----------+
                 |
       +---------v---------+
       |      Domain       |
       |  (Entidades y    |
       |   Reglas de negocio)
       +---------+---------+
                 |
      +----------v----------+
      |   Adapters / Infra  |
      | (DB, clientes API, |
      |  mappers, logging) |
      +-------------------+


```



- **Domain**: entidades y lógica de negocio pura (`User`, `Menu`, `Ingredient`).
- **Application / Use Cases**: casos de uso, por ejemplo `GenerateMenuService`.
- **Ports / Interfaces**: definiciones de entrada y salida para desacoplar la lógica de negocio de la infraestructura.
- **Adapters / Infraestructura**: controladores REST, repositorios JPA, mapeo DTOs con MapStruct, logging y persistencia en DB.

---

## Tecnologías utilizadas
- **Java 21**
- **Spring Boot 3.4.x**
- **Spring Web**
- **Spring Data JPA**
- **PostgreSQL** y **H2** (desarrollo)
- **Lombok**
- **MapStruct**
- **JUnit / Spring Boot Test**

---

## Funcionalidades actuales
- Endpoint `/menu` que recibe una lista de ingredientes y devuelve un menú sugerido.
- Persistencia de consultas en base de datos.
- Arquitectura hexagonal aplicada para mantener separación de capas y facilidad de mantenimiento.

---

## Cómo correr el proyecto

### Requisitos
- Java 21
- Gradle o Maven
- PostgreSQL (opcional, H2 funciona para pruebas)

### Pasos
1. Clonar el repositorio:
```bash

```java

git clone https://github.com/arielZarate/nutrition

cd nutrition
```



