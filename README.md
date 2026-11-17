# Análisis del rendimiento de consultas y operaciones de gestión de inventarios en una aplicación para una tienda de productos electrónicos

**Universidad Tecnológica de El Salvador**  
**Proyecto de Investigación - Ciclo 02-2026**  
**Asignatura:** Programación III - Sección: 03  

![Estado](https://img.shields.io/badge/Estado-Entrega%20Final-success)
![Versión](https://img.shields.io/badge/Versi%C3%B3n-v1.0-blue)
![Java](https://img.shields.io/badge/Java-21-orange)

## 📖 Descripción del proyecto
Este repositorio contiene la investigación y el desarrollo de una aplicación móvil de comercio electrónico enfocada en una tienda de hardware y productos electrónicos. El proyecto busca analizar empíricamente cómo el rendimiento de las operaciones de consulta y gestión de productos influye en el tiempo de respuesta del sistema y en la eficiencia del procesamiento de la información. 

La investigación aporta evidencia técnica (mediante métricas de tiempo y memoria) que permite optimizar la arquitectura de las aplicaciones móviles, mejorando la experiencia de los usuarios y facilitando la administración eficiente de inventarios (productos, precios, características) en escenarios de bases de datos con volúmenes de 100 a 200 registros.

## 📊 Resumen de hallazgos
A través de las pruebas de rendimiento ejecutadas con *JMH Profiler* y la validación en el cliente móvil, se obtuvieron las siguientes conclusiones técnicas:
* **Acceso a Datos:** La implementación de consultas mediante JDBC (SQL Nativo) presentó una latencia significativamente menor en milisegundos por operación (ms/op) frente al uso de frameworks ORM tradicionales, logrando un control directo sobre la ejecución.
* **Consumo de Memoria:** Al utilizar volúmenes de 100 a 200 registros, la capa de persistencia en *Kotlin* optimizó el recolector de basura (GC) evitando saturaciones en la memoria del *Heap*.
* **Renderizado Móvil:** La adopción del paradigma declarativo *Jetpack Compose* junto con gráficos generados nativamente (Canvas) en la barra de navegación, eliminó el *overhead* de imágenes estáticas, manteniendo una tasa estable de 60 FPS al hacer *scroll* sobre el catálogo.

## 🛠️ Tecnologías utilizadas
* **Lenguajes:** Java 21 / Kotlin
* **Frontend Móvil:** Android con Jetpack Compose
* **Backend:** Spring Boot (API REST), Patrón DAO
* **Base de Datos:** MySQL Server 8.0
* **Benchmarking:** Java Microbenchmark Harness (JMH 1.37)
* **Entorno de Desarrollo:** IntelliJ IDEA 2026 (con Android Plugin)
* **Control de Versiones:** Git y GitHub

## ⚙️ Instrucciones de instalación y ejecución
Para desplegar localmente la arquitectura Cliente-Servidor (Base de Datos -> Backend -> Android), se debe seguir este orden estricto:

### 1. Base de Datos (MySQL)
1. Iniciar el servicio local de **MySQL 8.0**.
2. Ejecutar el script `TiendaTecnologia.sql` incluido en el repositorio. Este script recreará la base de datos `TiendaTecnologia`, generará las 6 tablas normalizadas con sus índices (`idx_producto`) y poblará los datos semilla (100 - 200 registros).

### 2. Servidor Backend (Kotlin / Java 21)
1. En IntelliJ IDEA, abrir el directorio `Proyecto-backend`.
2. En `File > Project Structure`, asegurar que el SDK está configurado en **Java 21 (OpenJDK 21)**. *(No usar Java 25 para evitar fallos con JMH).*
3. En el archivo de configuración `ConexionDB.kt`, actualizar el usuario y la contraseña de tu conexión local de MySQL.
4. Ejecutar `Main.kt` (Play verde) para levantar la API REST. **Mantener este proceso en ejecución**.

### 3. Cliente Móvil (Android)
1. Asegurar que el **Android Plugin** esté activo en IntelliJ IDEA.
2. Abrir el directorio `app-android` y esperar la sincronización de Gradle.
3. **Configuración de Red:** En el código Android, actualizar la URL base de peticiones HTTP:
   * Usar `10.0.2.2` si ejecutarás la app en el Emulador de Android.
   * Usar la IP local (ej. `192.168.1.X`) si usarás un Teléfono Físico vía USB.
4. Verificar que el SDK de Android apunte a API Level 33 (Android 13).
5. Seleccionar el módulo `app` y ejecutar (**Run**). El IDE instalará el APK y abrirá el catálogo.

## 📂 Estructura de carpetas
📦 repositorio-tienda-electronica
┣ 📂 app-android/            # Proyecto móvil nativo en Jetpack Compose
┣ 📂 Proyecto-backend/       # Servidor API REST, DAO y módulo JMH Benchmark
┣ 📂 docs/                   # Documentación, ADRs y diagramas
┃ ┣ 📂 diagramas/            # Diagrama de arquitectura y flujo
┃ ┗ 📜 ADR_Consolidados.md   # Registro de decisiones de arquitectura
┣ 📜 TiendaTecnologia.sql    # Script de creación y población de BD MySQL 8.0
┣ 📜 README.md               # Este archivo
┗ 📜 LICENSE                 # Licencia del código fuente

## 📑 Enlace a los documentos en `docs/`
Toda la documentación técnica exigida para el proyecto se encuentra en el directorio `/docs`. Puedes acceder directamente a través de los siguientes enlaces:
* [Diagrama de Arquitectura del Sistema](./docs/diagramas/arquitectura.png)
* [Decisiones de Diseño Arquitectónico (ADR)](./docs/ADR_Consolidados.md)
* [Documento de Perfil de Proyecto](./docs/Perfil_Investigacion.pdf)

## 👥 Integrantes del Grupo
| Nombre Completo | Usuario de GitHub |
| :--- | :--- |
| Darlyn Julissa Cortez Herrera | [@DarlynCortez](https://github.com/DarlynCortez) |
| Cesia Esmeralda Funes Ruiz | [@cessifr-bit](https://github.com/cessifr-bit) |
| David Enrique Gil Martínez | [@davidmartinez311](https://github.com/davidmartinez311) |
| Adrián De Jesús Jacinto Vega | [@AdrianJJV](https://github.com/AdrianJJV) |
| Hazel Daniela Jiménez Martínez | [@HazelJM](https://github.com/HazelJM) |
| Abner Danilo Morales Fuentes | [@Danilo-4](https://github.com/Danilo-4) |
| Gerardo Emilio Recinos Miranda | [@g_rm0805](https://github.com/g_rm0805) |

## 📄 Licencia

**Licencia MIT**

Copyright (c) 2026 Equipo de Investigación - Universidad Tecnológica de El Salvador

Se concede permiso, de forma gratuita, a cualquier persona que obtenga una copia de este software y de los archivos de documentación asociados (el "Software"), para utilizar el Software sin restricción, incluyendo sin limitación los derechos de usar, copiar, modificar, fusionar, publicar, distribuir, sublicenciar, y/o vender copias del Software, y para permitir a las personas a las que se les proporcione el Software a hacer lo mismo, sujeto a las siguientes condiciones:

El aviso de copyright anterior y este aviso de permiso se incluirán en todas las copias o partes sustanciales del Software.

EL SOFTWARE SE PROPORCIONA "TAL CUAL", SIN GARANTÍA DE NINGÚN TIPO, EXPRESA O IMPLÍCITA, INCLUYENDO PERO NO LIMITADO A GARANTÍAS DE COMERCIALIZACIÓN, IDONEIDAD PARA UN PROPÓSITO PARTICULAR Y NO INFRACCIÓN. EN NINGÚN CASO LOS AUTORES O TITULARES DEL COPYRIGHT SERÁN RESPONSABLES DE NINGUNA RECLAMACIÓN, DAÑOS U OTRAS RESPONSABILIDADES, YA SEA EN UNA ACCIÓN DE CONTRATO, AGRAVIO O CUALQUIER OTRO MOTIVO, QUE SURJA DE, O EN CONEXIÓN CON EL SOFTWARE O EL USO U OTROS TRATOS EN EL SOFTWARE.
