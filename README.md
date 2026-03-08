# PetCare - Sistema de Gestión Veterinaria

Sistema integral de gestión veterinaria desarrollado con **Django** (backend de [PetCare-Web](https://github.com/Sh0cko/PetCare-Web)) y diseño moderno (UI de [PetCareAlex](https://github.com/DiegoZarzaMorales/PetCareAlex)).

## Características

- 🐾 **Gestión de Pacientes**: Registro de mascotas y propietarios
- 📅 **Citas**: Calendario interactivo de citas y consultas
- 🏨 **Servicios**: Hotel para mascotas, aseo/baño veterinario
- 💊 **Historial Médico**: Consultas, vacunaciones, historiales clínicos
- 📦 **Inventario**: Productos, movimientos, reportes de stock
- 🛒 **Tienda**: Sistema de ventas con carrito y facturación
- 📊 **Reportes**: Stock bajo, caducidad, más vendidos
- 👥 **Multi-usuario**: Roles de Administrador, Staff y Usuario Normal
- 🎨 **UI Moderna**: Diseño teal con animaciones (PetCareAlex)

## Requisitos

- Python 3.10+
- PostgreSQL 13+
- pip

## Configuración Local (Desarrollo)

### 1. Clonar el repositorio

```bash
git clone https://github.com/DiegoZarzaMorales/PetCare_TemasAvanzados.git
cd PetCare_TemasAvanzados
```

### 2. Crear entorno virtual e instalar dependencias

```bash
python -m venv venv
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

pip install -r requirements.txt
```

### 3. Configurar base de datos PostgreSQL

Crear la base de datos y ejecutar los scripts SQL:

```bash
# Crear la base de datos
psql -U postgres -c "CREATE DATABASE petcare_database;"
psql -U postgres -c "CREATE USER \"petcare-administrator\" WITH PASSWORD 'root123';"
psql -U postgres -c "GRANT ALL PRIVILEGES ON DATABASE petcare_database TO \"petcare-administrator\";"

# Cargar la estructura y datos de ejemplo
psql -U petcare-administrator -d petcare_database -f PostgreDB/Estructura.sql
psql -U petcare-administrator -d petcare_database -f PostgreDB/Inserts.sql
```

### 4. Variables de entorno (opcional para desarrollo)

Crea un archivo `.env` en la raíz (o configura las variables de entorno):

```env
# Base de datos (valores por defecto ya configurados para desarrollo local)
PGDATABASE=petcare_database
PGUSER=petcare-administrator
PGPASSWORD=root123
PGHOST=localhost
PGPORT=5432

# Seguridad (en producción, cambia estos valores)
SECRET_KEY=tu-clave-secreta-aqui
DEBUG=True

# Hosts permitidos (en producción, cambia esto)
ALLOWED_HOSTS=localhost,127.0.0.1
```

> **Nota:** Sin el archivo `.env`, los valores por defecto ya están configurados para desarrollo local con `DEBUG=True`.

### 5. Ejecutar migraciones de Django

```bash
cd PetCare
python manage.py migrate
```

### 6. Crear superusuario (administrador)

```bash
python manage.py createsuperuser
```

### 7. Iniciar el servidor de desarrollo

```bash
python manage.py runserver
```

Abre tu navegador en: **http://127.0.0.1:8000**

## Estructura del Proyecto

```
PetCare_TemasAvanzados/
├── PetCare/                    # Proyecto Django principal
│   ├── manage.py
│   ├── PetCare/                # Configuración del proyecto
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── middleware.py       # Middleware de autenticación global
│   │   └── wsgi.py
│   ├── PetApp/                 # Aplicación principal
│   │   ├── models.py           # Modelos de datos
│   │   ├── views.py            # Vistas y lógica de negocio
│   │   ├── admin.py
│   │   ├── migrations/         # Migraciones de base de datos
│   │   └── templatetags/       # Tags personalizados de Django
│   ├── templates/              # Templates HTML Django
│   │   ├── base.html           # Template base con sidebar
│   │   ├── index.html          # Dashboard principal
│   │   ├── registration/       # Login, registro, password
│   │   ├── pacientes/          # CRUD de mascotas
│   │   ├── propietario/        # CRUD de propietarios
│   │   ├── citas/              # Calendario y CRUD de citas
│   │   ├── inventario/         # Gestión de inventario
│   │   ├── factura/            # Facturación
│   │   ├── tienda/             # Sistema de ventas
│   │   └── ...                 # Más módulos
│   └── static/                 # Archivos estáticos
│       ├── css/style.css       # Estilos principales (diseño PetCareAlex)
│       ├── js/paws.js          # Animaciones de huellas
│       └── img/icons/          # Iconos del sistema
├── PostgreDB/                  # Scripts SQL
│   ├── Estructura.sql          # Estructura de la base de datos
│   └── Inserts.sql             # Datos de ejemplo
├── requirements.txt            # Dependencias Python
├── Procfile                    # Para Railway/Heroku
└── railway.json                # Configuración de despliegue Railway
```

## Roles de Usuario

| Rol | Descripción | Permisos |
|-----|-------------|----------|
| **Superusuario** | Administrador total | Todas las funciones + panel admin |
| **Staff** | Personal de la veterinaria | Gestión clínica + reportes |
| **Usuario Normal** | Cliente/usuario básico | Funciones básicas + tienda |

## Despliegue en Producción (Railway)

1. Conecta el repositorio a Railway
2. Configura las variables de entorno:
   - `PGDATABASE`, `PGUSER`, `PGPASSWORD`, `PGHOST`, `PGPORT`
   - `SECRET_KEY` (genera una nueva con `python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"`)
   - `DEBUG=False`
   - `ALLOWED_HOSTS=tu-dominio.railway.app`
3. Railway ejecutará automáticamente: `python manage.py migrate && gunicorn PetCare.wsgi:application`

## Tecnologías

- **Backend**: Django 5.2, PostgreSQL
- **Frontend**: HTML5, CSS3, Font Awesome 6, Bootstrap 5
- **Despliegue**: Railway (con Whitenoise para archivos estáticos)
- **Diseño**: Inspirado en PetCareAlex (gradiente teal, animaciones modernas)
