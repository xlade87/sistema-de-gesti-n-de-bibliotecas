# Sistema de Gestión de Biblioteca Personal

## Descripción del Proyecto

Sistema desarrollado en Python con interfaz gráfica Tkinter para la gestión completa de una biblioteca personal. Permite administrar libros, usuarios, autores, préstamos y reseñas mediante una aplicación de escritorio con base de datos MySQL.

##  Características Principales

- **Gestión completa de libros** (agregar, editar, eliminar, buscar)
- **Registro y administración de usuarios**
- **Catálogo de autores** 
- **Sistema de préstamos y devoluciones** con control de disponibilidad
- **Sistema de reseñas y calificaciones**
- **Interfaz intuitiva** organizada en módulos
- **Base de datos MySQL** con procedimientos almacenados
- **Validación de datos** en tiempo real

## Tecnologías Utilizadas

- **Lenguaje de programación:** Python 3.x
- **Interfaz gráfica:** Tkinter
- **Base de datos:** MySQL
- **Servidor local:** XAMPP
- **Gestor de BD:** HeidiSQL
- **Control de versiones:** Git

## Requisitos del Sistema

### Software Requerido
- Python 3.8 o superior
- XAMPP (para servidor MySQL)
- HeidiSQL (opcional, para gestión de BD)
- Git (para control de versiones)

### Dependencias Python
- mysql-connector-python

##  Instalación y Configuración

### Paso 1: Clonar el Repositorio
```bash
git clone https://github.com/tuusuario/biblioteca-management-system.git
cd biblioteca-management-system
```

### Paso 2: Instalar Dependencias
```bash
pip install mysql-connector-python
```

### Paso 3: Configurar XAMPP
1. Descargar e instalar XAMPP 
2. Iniciar el panel de control de XAMPP
3. Activar los módulos **Apache** y **MySQL**

### Paso 4: Configurar la Base de Datos
1. Abrir HeidiSQL o phpMyAdmin
2. Conectarse al servidor MySQL (127.0.0.1, usuario: root, sin contraseña)
3. Ejecutar el script `database-schema.sql` ubicado en la carpeta `docs/`

### Paso 5: Ejecutar la Aplicación
```
python src/sistema de gestion de biblioteca.py
```

##  Estructura de la Base de Datos

### Tablas Principales

####  Libros
- `id` (INT, PRIMARY KEY, AUTO_INCREMENT)
- `titulo` (VARCHAR(100), NOT NULL)
- `autor` (VARCHAR(100), NOT NULL)
- `genero` (VARCHAR(50))
- `año_publicacion` (INT)
- `isbn` (VARCHAR(20))
- `disponible` (BOOLEAN, DEFAULT TRUE)

####  Usuarios
- `id` (INT, PRIMARY KEY, AUTO_INCREMENT)
- `nombre` (VARCHAR(100), NOT NULL)
- `email` (VARCHAR(100), UNIQUE, NOT NULL)
- `telefono` (VARCHAR(15))
- `fecha_registro` (DATE, DEFAULT CURRENT_DATE)

####  Autores
- `id` (INT, PRIMARY KEY, AUTO_INCREMENT)
- `nombre` (VARCHAR(100), NOT NULL)
- `nacionalidad` (VARCHAR(50))
- `fecha_nacimiento` (DATE)

####  Préstamos
- `id` (INT, PRIMARY KEY, AUTO_INCREMENT)
- `libro_id` (INT, FOREIGN KEY)
- `usuario_id` (INT, FOREIGN KEY)
- `fecha_prestamo` (DATE, DEFAULT CURRENT_DATE)
- `fecha_devolucion` (DATE)
- `devuelto` (BOOLEAN, DEFAULT FALSE)

#### Reseñas
- `id` (INT, PRIMARY KEY, AUTO_INCREMENT)
- `libro_id` (INT, FOREIGN KEY)
- `usuario_id` (INT, FOREIGN KEY)
- `calificacion` (INT, CHECK 1-5)
- `comentario` (TEXT)
- `fecha_reseña` (DATE, DEFAULT CURRENT_DATE)

##  Procedimientos Almacenados

La base de datos incluye 11 procedimientos almacenados para operaciones avanzadas:

### Operaciones CRUD
- `sp_InsertarLibro()` - Insertar nuevo libro
- `sp_ActualizarLibro()` - Actualizar libro existente
- `sp_EliminarLibro()` - Eliminar libro con validaciones
- `sp_InsertarUsuario()` - Registrar nuevo usuario
- `sp_InsertarAutor()` - Agregar autor al catálogo

### Gestión de Préstamos
- `sp_RealizarPrestamo()` - Realizar préstamo con validaciones
- `sp_DevolverLibro()` - Gestionar devolución de libro

### Consultas y Reportes
- `sp_ObtenerEstadisticas()` - Estadísticas del sistema
- `sp_BuscarLibrosPorTitulo()` - Búsqueda avanzada
- `sp_ObtenerPrestamosActivos()` - Consultar préstamos activos
- `sp_InsertarReseña()` - Agregar reseñas con validación

##  Uso de la Aplicación

### Módulo de Libros
1. Navegar a la pestaña "Libros"
2. Completar el formulario con los datos del libro
3. Hacer clic en "Guardar" para agregar al sistema
4. Usar "Buscar por ID" para localizar libros existentes

### Módulo de Usuarios
1. Acceder a la pestaña "Usuarios"
2. Registrar nuevos usuarios con sus datos de contacto
3. El sistema valida automáticamente emails duplicados

### Módulo de Préstamos
1. Ir a la pestaña "Préstamos"
2. Ingresar ID de libro y usuario para realizar préstamo
3. El sistema verifica disponibilidad automáticamente
4. Para devoluciones, ingresar ID del préstamo

### Módulo de Autores
1. Navegar a "Autores"
2. Mantener el catálogo de escritores de forma independiente
3. Gestionar información biográfica de autores

## 🔧 Funcionalidades Avanzadas

### Validaciones Implementadas
- Campos obligatorios en todos los formularios
- Validación de formato de email
- Control de duplicados en usuarios
- Verificación de disponibilidad de libros
- Validación de calificaciones (1-5 estrellas)

### Características de Seguridad
- Transacciones ACID en la base de datos
- Validación en el servidor mediante procedimientos almacenados
- Manejo de errores y excepciones
- Confirmaciones antes de eliminaciones

## Datos de Ejemplo Incluidos

El sistema incluye datos de demostración:
- 5 autores literarios reconocidos
- 6 libros clásicos de la literatura
- 4 usuarios de prueba
- 3 préstamos de ejemplo
- 3 reseñas demostrativas

## Desarrollo

### Estructura del Código
El proyecto sigue una arquitectura en tres capas:
1. **Capa de Presentación:** Interfaz gráfica con Tkinter
2. **Capa de Lógica de Negocio:** Funciones Python y procedimientos almacenados
3. **Capa de Datos:** Base de datos MySQL
