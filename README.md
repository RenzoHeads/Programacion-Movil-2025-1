
# 📱 Proyecto de Aplicación Móvil - Asignación 1


**Integrantes del grupo:**
- Cabezas Diaz Renzo Edgar 20224558
- David Vela Larrea 20202209
- Diego Arturo Huaman Bonilla 20211287
- Rodrigo Alonso Lara Camacho 20211415
- Rodrigo Gabriel Pérez Peña 20191544
---

## 🛠️ Entorno de Desarrollo
El entorno de desarrollo de nuestra aplicación móvil para la administración de tareas está compuesto por una combinación de tecnologías orientadas al desarrollo multiplataforma, backend robusto y servicios en la nube. A continuación, detallamos cada una de las herramientas que estamos definiendo para utilizar, su propósito y cómo fueron configuradas para el proyecto.

### 1.Flutter
Descripción: Framework de código abierto desarrollado por Google, permite crear aplicaciones móviles nativas para Android e iOS a partir de un único código base.

Instalación:
Descargar el SDK desde flutter.dev.
Agregar Flutter al PATH del sistema.
Ejecutar flutter doctor para verificar dependencias y configuraciones necesarias.
Instalar un editor como Visual Studio Code o Android Studio, con el plugin de Flutter y Dart.

### 2. Ruby (Backend con Sinatra)
Descripción: Framework minimalista escrito en Ruby, ideal para desarrollar APIs RESTful de forma rápida y ligera.

Instalación:
Instalar Ruby (vía RVM o rbenv).
Instalar Sinatra mediante el comando gem install sinatra.
Crear el proyecto inicial con main.rb y config.ru para definir la API.
Configurar rutas para comunicar con la app Flutter.

### 3.Base de Datos PostgreSQL (Azure Database for PostgreSQL)
Descripción: Sistema de gestión de bases de datos relacional, utilizado para almacenar los datos estructurados de la aplicación como usuarios, tareas y categorías.

Instalación:
Crear una instancia en el portal de Azure.
Configurar firewall para permitir acceso desde el backend.
Usar el cliente psql o herramientas como PgAdmin para gestionar la base de datos.
Configurar las credenciales en el archivo database.yml del backend Ruby.

### 4.Azure Blob Storage
Descripción: Servicio de almacenamiento de objetos no estructurados en la nube, usado para guardar imágenes asociadas a las tareas o categorías.

Instalación:
Crear una cuenta de almacenamiento en Azure.
Crear un contenedor para las imágenes.
Generar SAS Tokens para acceso seguro desde el backend.
Integrar con el backend utilizando gemas como azure-storage-blob.

### 5.Servicio LLM (Large Language Model) Externo
Descripción: Modelo de lenguaje con IA usado para generar automáticamente listas de tareas personalizadas según las necesidades del usuario.

Integración:
Acceso vía API RESTful.
Configuración de autenticación con API Key o Bearer Token.
Uso de la biblioteca Net::HTTP o HTTParty en Ruby para enviar solicitudes al modelo.

### 6.Microsoft Azure (Plataforma de Despliegue)
Descripción: Plataforma cloud donde se alojan todos los servicios: backend, base de datos y almacenamiento.

Configuración:
Uso del Servicio de Aplicaciones de Azure para desplegar el backend Ruby.
Configuración de variables de entorno (por ejemplo, claves y URIs).
Uso de GitHub Actions para automatizar despliegues.


---
## 🚀 Diagrama de Despliegue

![Diagrama de Despliegue](diagramadespliegue3.png)

#### El diagrama de despliegue representa la arquitectura de una aplicación móvil desarrollada en Flutter que se comunica con un backend Ruby a través de solicitudes HTTP API. Este backend está desplegado en un Servicio de Aplicaciones dentro de la nube de Azure. La aplicación maneja datos estructurados mediante una base de datos PostgreSQL alojada en Azure Database for PostgreSQL, y archivos multimedia (como imágenes) a través de Azure Blob Storage. Además, el sistema integra un servicio LLM (modelo de lenguaje) externo, encargado de generar listas de tareas utilizando inteligencia artificial, al cual el backend envía solicitudes específicas. La arquitectura sigue un enfoque modular que separa claramente los componentes de cliente, lógica de negocio, almacenamiento, base de datos y generación inteligente.
---

## ☁️ Requisitos No Funcionales

### Autenticación segura entre cliente y servidor:
La aplicación móvil en Flutter debe comunicarse con el backend mediante HTTPS cada solicitud enviada al servidor Ruby.

### Disponibilidad del backend:
El Servicio de Aplicaciones de Azure que ejecuta el backend Ruby garantiza disponibilidad continua.

### Acceso rápido a imágenes:
El acceso a imágenes almacenadas en Azure Blob Storage debe realizarse mediante URLs firmadas (SAS tokens).

### Tolerancia a fallos en la generación IA:
Las solicitudes al servicio LLM deben manejar errores y tiempos de espera, permitiendo mostrar mensajes adecuados al usuario si el generador falla o demora.

### Eficiencia en consultas a la base de datos:
Las consultas del backend Ruby hacia PostgreSQL deben estar optimizadas con índices y paginación para garantizar tiempos de respuesta bajos, incluso con grandes volúmenes de datos.

### Escalabilidad del sistema:
Cada componente (backend, base de datos, almacenamiento y servicio IA) debe poder escalarse de forma independiente según la demanda de usuarios o procesamiento.



---

## ✅ Diagrama de Casos de Uso

![Diagrama de Casos de Uso Simplificado](diagrama_simplificado.png)

### Casos de Uso 

| Caso de Uso                                 | Descripción |
|----------------------------------------------|-------------|
| Registro de Usuario                         | Permite al usuario registrarse en el sistema proporcionando sus datos personales. |
| Inicio de Sesión                            | Permite al usuario iniciar sesión en la aplicación. |
| Restablecer Contraseña                      | Permite al usuario recuperar el acceso a su cuenta mediante el restablecimiento de contraseña. |
| Actualizar Datos del Usuario                | Permite al usuario actualizar su información personal. |
| Crear Tarea                                 | Permite al usuario crear una nueva tarea. |
| Editar Tarea                                | Permite al usuario editar una tarea existente. |
| Eliminar Tarea                              | Permite al usuario eliminar una tarea existente. |
| Visualizar todas las tareas                 | Permite al usuario ver todas las tareas disponibles. |
| Marcar tarea como completada                | Permite al usuario marcar una tarea como completada. |
| Buscar tareas y listas                      | Permite al usuario buscar tareas y listas específicas. Ademas de poder usar buscar por categorias o etiquetas. |
| Crear lista                                 | Permite al usuario crear una nueva lista de tareas. |
| Editar lista                                | Permite al usuario editar el nombre, color o descripción de una lista. |
| Eliminar lista                              | Permite al usuario eliminar una lista existente. |
| Ver detalles de lista                       | Permite al usuario ver los detalles de una lista específica. |
| Visualizar todas las listas                 | Permite al usuario visualizar todas las listas creadas. |
| Asignar/desasignar tareas de una lista       | Permite al usuario asignar o desasignar tareas a/de una lista. |
| Generar Lista con Tareas usando IA           | Permite generar automáticamente una lista de tareas utilizando Inteligencia Artificial. |
| Visualizar Notificaciones                   | Permite al usuario visualizar sus notificaciones. |
| Configurar Notificaciones                   | Permite al usuario configurar cómo desea recibir notificaciones. |
| Recibir Notificaciones                      | Permite al usuario recibir notificaciones de eventos importantes. |

---

## 📸 Imágenes de Casos de Uso



### Autenticación y Perfil
- ![Registro de Usuario](diagramasCU/1_registro_usuario.png)  
  **Registro de Usuario**
- ![Inicio de Sesión](diagramasCU/2_inicio_sesion.png)  
  **Inicio de Sesión**
- ![Restablecer Contraseña](diagramasCU/3_restablecer_contrasena.png)  
  **Restablecer Contraseña**
- ![Actualizar Datos del Usuario](diagramasCU/4_actualizar_datos_usuario.png)  
  **Actualizar Datos del Usuario**

### Gestión de Tareas
- ![Crear Tarea](diagramasCU/5_crear_tarea.png)  
  **Crear Tarea**
- ![Editar Tarea](diagramasCU/6_editar_tarea.png)  
  **Editar Tarea**
- ![Eliminar tarea](eliminarTarea.png)  
  **Eliminar Tarea**
- ![Visualizar tareas](visualizarTareas.png)  
  **Visualizar Tareas**
- ![Marcar tarea completada](marcarTareaCompletada.png)  
  **Marcar Tarea como Completada**
- ![Buscar tareas](buscarTareas.png)  
  **Buscar Tareas y Listas**

### Gestión de Listas
- ![Crear lista](crearLista.png)  
  **Crear Lista**
- ![Editar lista](editarLista.png)  
  **Editar Lista**
- ![Eliminar lista](eliminarLista.png)  
  **Eliminar Lista**
- ![Ver lista](verLista.png)  
  **Ver Detalles de Lista**
- ![Ver todas las listas](verTodasListas.png)  
  **Visualizar Todas las Listas**
- ![Asignar/desasignar tareas](asignarTarea.png)  
  **Asignar/Desasignar Tareas de una Lista**
- ![Generar Lista con Tareas usando Inteligencia Artificial](diagramasCU/7_generar_lista_con_ia.png)  
  **Generar Lista con Tareas usando Inteligencia Artificial**

### Gestión de Notificaciones
- ![Visualizar Notificaciones](diagramasCU/8_visualizar_notificaciones.png)  
  **Visualizar Notificaciones**
- ![Configurar Notificaciones](diagramasCU/9_configurar_notificaciones.png)  
  **Configurar Notificaciones**
- ![Recibir Notificaciones](diagramasCU/10_recibir_notificaciones.png)  
  **Recibir Notificaciones**

---

## 📚 Diagrama de clases

![Diagrama de clases](diagrama_clases.png)  
---
---

## 📚 Descripción de Casos de Uso


---
