# Poncho Digital

Plataforma web para la **Fiesta del Poncho**: permite que los artesanos se postulen, que un administrador evalúe las solicitudes y asigne stands, y que los visitantes recorran un catálogo público de productos.

Proyecto de la materia **Programación III** (UNCA), desarrollado con **Django** y **PostgreSQL**.

## Funcionalidades

**Artesanos**
- Solicitud de participación con datos personales y del emprendimiento.
- Consulta del estado de la solicitud mediante DNI.
- Alta, modificación y baja de sus productos, con imagen.
- Edición del perfil público: datos del emprendimiento, horarios y redes sociales.

**Visitantes (sin cuenta)**
- Catálogo con filtro por categoría y buscador de texto.
- Detalle del producto y perfil del artesano.
- "Me gusta" y comentarios, controlados con una cookie anónima (UUID).

**Administrador**
- Evaluación de solicitudes: aprobar, rechazar o pedir modificaciones.
- Alta, modificación, baja, asignación y liberación de stands.
- Reportes operativos y tendencias de búsqueda.

**Cliente institucional**
- Panel con ocupación de stands, artesanos por localidad y rubro, y estadísticas por artesano.

## Arquitectura

Aplicación Django organizada en tres apps, con el patrón MVT:

| App | Responsabilidad |
|---|---|
| `usuarios` | Usuario personalizado, roles y control de acceso |
| `artesanos` | Solicitudes, artesanos, stands, paneles y reportes |
| `productos` | Catálogo, gestión de productos, perfil público, "Me gusta" y comentarios |

El acceso se controla con un modelo de **roles** (`ADMINISTRADOR`, `ARTESANO`, `CLIENTE`) y un decorador propio, `rol_requerido`.

## Tecnologías

- Python y Django 6.1
- PostgreSQL
- HTML, CSS y JavaScript `[agregar Bootstrap si se usa]`

## Instalación

```bash
git clone https://github.com/victoryapura15JV/Lab_Prog3.git
cd Lab_Prog3/laboratorio        # [ajustar si cambia la estructura]

python -m venv venv
source venv/bin/activate         # en Windows: venv\Scripts\activate
pip install django psycopg2-binary   # [o: pip install -r requirements.txt]
```

1. Crear una base de datos PostgreSQL y configurar la conexión en `settings.py` `[o en variables de entorno]`.
2. Aplicar las migraciones:

```bash
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

3. Cargar los roles iniciales `[completar cómo: admin, script o fixture]`.

La aplicación queda disponible en `http://127.0.0.1:8000/`.

## Estructura

```
laboratorio/
├── usuarios/      # cuentas, roles y permisos
├── artesanos/     # solicitudes, stands, paneles y reportes
├── productos/     # catálogo, "Me gusta", comentarios y perfil
├── static/        # CSS y JavaScript
├── templates/     # plantillas base
└── media/         # imágenes subidas (no se versiona)
```

## Limitaciones conocidas

- Con el modo incógnito o sin cookies, un visitante cuenta como otro: no se puede evitar sin exigir inicio de sesión.
- Los reportes son fijos y no admiten filtros.
- Las imágenes se validan por extensión y tamaño, sin verificar el contenido.
- El catálogo no tiene paginación ni hay pruebas automáticas.

## Equipo

Bravo Nicolás — MU: 01805
Escalante Judith Griselda — MU: 01862
Yapura Fuenzalida Victor — MU: 01913

Materia: Programación III · UNCA · `2026`
