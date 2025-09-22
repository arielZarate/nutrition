# NUTRITION API- Arquitectura Hexagonal

<img src="./images/logo.jpg" alt="Logo"  height="300" />

## Descripción

**Nutrition API** es un proyecto personal que implementa una **API REST de nutrición** usando **arquitectura hexagonal**.
Permite generar menús y sugerencias nutricionales en base a ingredientes o restricciones del usuario. La API está preparada para integrar en el futuro un motor de IA (ej. ChatGPT) para generar recetas dinámicas.

El objetivo del proyecto es mostrar buenas prácticas de diseño, separación de capas y clean code en un microservicio real.

---

## Arquitectura

El proyecto sigue la **arquitectura hexagonal**, con separación clara entre dominio, casos de uso y adaptadores:

  ```bash
  

nutrition
│
├── application/                  # Casos de uso / services de aplicación
│   └── GenerateMenuService.java
│
├── domain/                       # Lógica de negocio pura
│   ├── model/                    # Entidades y DTOs
│   │   └── Menu.java
│   ├── ports/                    # Interfaces / contratos
│   │   └── MenuGeneratorPort.java
│   └── services/                 # Reglas de negocio específicas
│       └── MenuDomainService.java
│
├── infrastructure/               # Implementaciones concretas (adapters)
│   ├── adapters/                 # Integraciones con sistemas externos
│   │   └── AIAdapter.java
│   ├── repositories/             # Repositorios JPA
│   │   └── MenuRepository.java
│   └── rest/                     # Clientes externos (ej. API de IA)
│       └── AIClient.java
│
├── interfaces/                   # Entrada al sistema (controladores, config)
│   ├── rest/                     # Controllers REST
│   │   └── MenuController.java
│   ├── config/                   # Configuración general
│   │   ├── LoggingConfig.java
│   │   └── IAConfig.java
│   └── middleware/               # Manejo global de errores/excepciones
│       └── ExceptionHandler.java
│
├── resources/                    # Recursos del proyecto
│   ├── application.properties    # Configuración general (DB, logging, etc)
│   ├── data.sql                   # Datos iniciales para pruebas (opcional)
│   └── images/                    # Logo u otras imágenes para README
│       └── logo.jpg
│
├── test/                          # Pruebas unitarias e integración
│   └── ...
│
├── pom.xml / build.gradle          # Dependencias y build
├── README.md
├── HELP.md
└── .gitignore

---
  
  ```

| Capa / Paquete                  | Qué va allí                                              | Ejemplo                            |
| ------------------------------- | -------------------------------------------------------- | ---------------------------------- |
| **application**                 | Casos de uso, coordina la lógica entre domain y adapters | `GenerateMenuService`              |
| **domain/model**                | Entidades y DTOs                                         | `Menu`, `Ingredient`               |
| **domain/ports**                | Interfaces que definen contratos de entrada/salida       | `MenuGeneratorPort`                |
| **domain/services**             | Reglas de negocio puras                                  | `MenuDomainService`                |
| **infrastructure/adapters**     | Implementaciones concretas de ports                      | `AIAdapter` (llama a motor de IA)  |
| **infrastructure/repositories** | Persistencia de datos                                    | `MenuRepository` (Spring Data JPA) |
| **infrastructure/rest**         | Clientes externos                                        | `AIClient`                         |
| **interfaces/rest**             | Controllers que exponen endpoints al mundo               | `MenuController`                   |
| **interfaces/config**           | Configuraciones varias                                   | Logging, Beans, API clients        |
| **interfaces/middleware**       | Manejo global de errores, excepciones, filtros           | `ExceptionHandler`                 |



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


git clone https://github.com/arielZarate/nutrition

cd nutrition
```
