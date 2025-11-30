# Sistema de Gestión de Contenido Audiovisual

## 📘 Visión General del Proyecto

Este repositorio contiene la implementación de una aplicación en **Java** diseñada para administrar y catalogar una biblioteca de medios. El desarrollo se ha guiado por una estricta adhesión a los estándares de la ingeniería de software moderna, destacando la adopción integral de los principios **SOLID** y el patrón arquitectónico **Modelo-Vista-Controlador (MVC)**, además de una metodología de pruebas robusta.

---

## 🏗️ Ingeniería y Diseño de Software

### 1. Arquitectura Central (Patrón MVC)

El sistema opera bajo un esquema de tres capas bien definidas para asegurar una separación de preocupaciones limpia: 

[Image of Model-View-Controller (MVC) pattern diagram]


* **El Modelo (Datos):** Clases del paquete `uni1a` (e.g., `Pelicula`, `Documental`). Son responsables de encapsular la información y la lógica intrínseca a cada tipo de contenido.
* **La Vista (Interfaz):** La clase `ConsoleView`. Su rol se limita a interactuar directamente con el usuario, mostrando la salida formateada y recolectando la entrada de comandos.
* **El Controlador (Lógica):** La clase `ContentService`. Actúa como el puente, orquestando las acciones basadas en la entrada del usuario y mediando entre el Modelo y la capa de Persistencia.

### 2. Fundamentos de Código (Principios SOLID)

El diseño está optimizado para la flexibilidad y escalabilidad: 

* **Desacoplamiento por Dependencia (DIP):** El controlador (`ContentService`) opera contra la abstracción (`IFileHandler`), no contra la clase concreta de archivo, permitiendo sustituir fácilmente el mecanismo de almacenamiento (ej. cambiar de CSV a JSON o SQL) sin modificar la lógica de negocio.
* **Contratos de Sustitución (LSP):** Todas las entidades de contenido (`Pelicula`, `SerieDeTV`, etc.) son totalmente intercambiables con su tipo base, lo que garantiza el polimorfismo sin efectos secundarios.
* **Extensibilidad Controlada (OCP):** Añadir un nuevo tipo de medio solo requiere crear una nueva subclase, dejando las clases existentes (como el servicio principal) cerradas a la modificación.

### 3. Persistencia de Datos y Manejo de I/O

La gestión de archivos es robusta y eficiente:

* **Abstracción de Persistencia:** Se usa la interfaz **`IFileHandler`** con la implementación concreta `CsvFileHandler` para leer y escribir el archivo `contenidos.csv`.
* **Refactorización de Presentación:** El método clave `mostrarDetalles()` fue refactorizado para **devolver un `String` formateado** en lugar de imprimir, delegando la responsabilidad de I/O a la Vista y mejorando la **modularidad**.
* **Optimización de Memoria:** La generación de cadenas de texto complejas utiliza **`StringBuilder`**, lo que garantiza un manejo eficiente de la memoria y un mejor rendimiento en la concatenación.

---

## 🔬 Garantía de Calidad (Pruebas Unitarias)

La fiabilidad del sistema se verifica mediante una suite de pruebas rigurosas.

* **Frameworks Utilizados:** Se combinó **JUnit 5** con **Mockito** para la simulación de objetos.
* **Aislamiento de Lógica:** Las pruebas, como `ContentServiceTest`, utilizan *mocking* para simular la capa de persistencia (`IFileHandler`). Esto asegura que la **lógica de negocio** se pruebe de forma aislada, sin dependencia del sistema de archivos real, garantizando resultados rápidos y deterministas.

---

## 💻 Guía de Configuración y Uso

### Requisitos Técnicos

* Java Development Kit (**JDK 16 o superior**).
* Un IDE compatible con Java (Se recomienda **IntelliJ IDEA**).

### Pasos para el Despliegue

1.  **Obtención del Código Fuente:** Clone el repositorio:
    ```bash
    git clone <URL_DEL_REPOSITORIO>
    ```

2.  **Preparación del IDE:**
    * Abra el directorio del proyecto en su IDE.
    * Configure el **SDK del JDK** a la versión compatible (16+).

3.  **Ejecución Principal:**
    * Localice la clase de arranque: `MainController.java`.
    * Ejecute el método `main()` para iniciar la aplicación de consola.

### Ejecución de Pruebas

1.  **Dependencias:** Asegúrese de que las librerías de prueba (JUnit y Mockito) estén configuradas en el *classpath*.
2.  **Lanzamiento:** Navegue a la clase `ContentServiceTest.java` (ubicada en la carpeta de *tests*) y ejecute la clase completa para validar la suite de pruebas unitarias.
