Perfecto ✅
Aquí tienes **el resumen completo, limpio y organizado** del proyecto **“Tienda de Magia”** con todos los pasos y estructura según tus indicaciones. Este documento puede servirte como guía práctica o para entregar como evidencia en clase.

---

## 🧙‍♂️ Proyecto: Tienda de Magia

**Lenguaje:** Python
**Framework:** Django
**Editor:** Visual Studio Code

---

### 🗂️ 1. Crear carpeta del Proyecto

```bash
Crear una carpeta llamada UIII_TiendadeMagia_0533
```

---

### 💻 2. Abrir VS Code sobre la carpeta

* Abrir VS Code
* Seleccionar **“Abrir carpeta”**
* Elegir la carpeta `UIII_TiendadeMagia_0533`

---

### 💡 3. Abrir terminal en VS Code

* Presionar `Ctrl + ñ`
  o
* Ir a **Ver → Terminal**

---

### ⚙️ 4. Crear entorno virtual

```bash
python -m venv .venv
```

---

### 🧠 5. Activar entorno virtual

```bash
.venv\Scripts\activate
```

---

### 🐍 6. Activar intérprete de Python

* Presionar `Ctrl + Shift + P`
* Escribir: **Python: Select Interpreter**
* Seleccionar el intérprete que diga `.venv`

---

### 🪄 7. Instalar Django

```bash
pip install django
```

---

### 🏗️ 8. Crear proyecto principal (sin duplicar carpeta)

```bash
django-admin startproject backend_TiendadeMagia .
```

---

### 🚀 9. Ejecutar servidor en el puerto 8007

```bash
python manage.py runserver 8007
```

---

### 🌐 10. Abrir en navegador

Copiar el enlace que aparece en la terminal:

```
http://127.0.0.1:8007/
```

---

### 🧩 11. Crear aplicación

```bash
python manage.py startapp app_TiendadeMagia
```

---

### 📦 12. models.py (dentro de app_TiendadeMagia)

```python
from django.db import models

# ==========================================
# MODELO: PRODUCTOS
# ==========================================
class Producto(models.Model):
    nombre = models.CharField(max_length=100)
    descripcion = models.TextField(blank=True, null=True)
    categoria = models.CharField(max_length=50)
    precio = models.DecimalField(max_digits=10, decimal_places=2)
    proveedor = models.CharField(max_length=100)
    fecha_ingreso = models.DateField(auto_now_add=True)
    stock = models.IntegerField()

    def __str__(self):
        return self.nombre


# ==========================================
# MODELO: ORDEN DE VENTA
# ==========================================
class OrdenDeVenta(models.Model):
    cliente = models.CharField(max_length=100)
    fecha_orden = models.DateTimeField(auto_now_add=True)
    direccion_envio = models.CharField(max_length=200)
    metodo_pago = models.CharField(max_length=50)
    total = models.DecimalField(max_digits=10, decimal_places=2)
    estado = models.CharField(max_length=50)
    comentarios = models.TextField(blank=True, null=True)
    productos = models.ManyToManyField(Producto, related_name="ordenes")

    def __str__(self):
        return f"Orden #{self.id} - {self.cliente}"


# ==========================================
# MODELO: DETALLE ORDEN
# ==========================================
class DetalleOrden(models.Model):
    orden = models.ForeignKey(OrdenDeVenta, on_delete=models.CASCADE, related_name="detalles")
    producto = models.ForeignKey(Producto, on_delete=models.CASCADE, related_name="detalles")
    cantidad = models.IntegerField()
    precio_unitario = models.DecimalField(max_digits=10, decimal_places=2)
    subtotal = models.DecimalField(max_digits=10, decimal_places=2)
    descuento = models.DecimalField(max_digits=10, decimal_places=2, default=0)
    observaciones = models.CharField(max_length=200, blank=True, null=True)

    def __str__(self):
        return f"{self.producto.nombre} x {self.cantidad}"
```

---

### ⚡ 12.5 Migraciones

```bash
python manage.py makemigrations
python manage.py migrate
```

---

### 🧱 13. Primer módulo: PRODUCTO

---

### 🧭 14. views.py — Crear funciones

En `app_TiendadeMagia/views.py`:

* `inicio_tienda`
* `agregar_producto`
* `actualizar_producto`
* `realizar_actualizacion_producto`
* `borrar_producto`

---

### 📁 15. Crear carpeta templates

Dentro de `app_TiendadeMagia`:

```
app_TiendadeMagia/
│
└── templates/
```

---

### 🧾 16. Archivos HTML base

Dentro de `templates` crear:

```
base.html
header.html
navbar.html
footer.html
inicio.html
```

---

### 💅 17. base.html

Agregar Bootstrap para CSS y JS (enlaces oficiales de Bootstrap).

---

### 🧭 18. navbar.html

Incluir opciones:

* Sistema de Administración Tienda de Magia
* Inicio
* Productos
* Órdenes
* Detalles de Órdenes

---

### ⚖️ 19. footer.html

Incluir:

```
© 2025 - Creado por Omar Carrasco, CBTis 128  
{{ fecha_actual }}
```

---

### ✨ 20. inicio.html

Colocar información general del sistema y una imagen alusiva a la magia.

---

### 📂 21. Crear subcarpeta “producto”

Dentro de:

```
app_TiendadeMagia/templates/producto/
```

---

### 📄 22. Archivos HTML del módulo Producto

* agregar_producto.html
* ver_productos.html
* actualizar_producto.html
* borrar_producto.html

---

### ⚠️ 23. No utilizar forms.py

---

### 🛣️ 24. Crear archivo urls.py en app_TiendadeMagia

---

### ⚙️ 25. Agregar app en settings.py

En `backend_TiendadeMagia/settings.py`:

```python
INSTALLED_APPS = [
    ...
    'app_TiendadeMagia',
]
```

---

### 🌍 26. Configurar urls.py principal

En `backend_TiendadeMagia/urls.py`, enlazar con las rutas de la app:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_TiendadeMagia.urls')),
]
```

---

### 🔐 27. Registrar modelos en admin.py

En `app_TiendadeMagia/admin.py`:

```python
from django.contrib import admin
from .models import Producto, OrdenDeVenta, DetalleOrden

admin.site.register(Producto)
admin.site.register(OrdenDeVenta)
admin.site.register(DetalleOrden)
```

---

### 🪶 28. Solo trabajar por ahora con el modelo Producto

---

### 🎨 29. Usar colores suaves, atractivos y modernos

---

### 🚫 30. No validar entrada de datos

---

### 🧩 31. Crear estructura completa de carpetas y archivos

---

### ✅ 32. Proyecto totalmente funcional

---

### 🔁 33. Ejecutar servidor en el puerto 8007

```bash
python manage.py runserver 8007
```

---

¿Quieres que te genere **la estructura completa de carpetas y archivos (vacíos)** con el contenido base (`views.py`, `urls.py`, `templates`, etc.) para copiarla directamente en tu proyecto Django?
Así podrías tener el sistema del CRUD de **Productos** ya funcional.
