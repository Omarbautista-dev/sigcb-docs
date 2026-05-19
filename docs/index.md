# Manual de Capacitacion - SIG-CB Cancino Bike

## 1. Presentacion

Este manual de capacitacion esta dirigido a los usuarios que operaran el sistema SIG-CB de la Refaccionaria Cancino Bike. El sistema fue desarrollado en JavaFX y utiliza una base de datos MySQL llamada `sig_cb`.

El objetivo principal del sistema es apoyar las operaciones diarias de la refaccionaria:

- Controlar el acceso de usuarios.
- Registrar ventas de contado y a credito.
- Consultar y administrar productos del inventario.
- Administrar proveedores y ordenes de compra.
- Consultar reportes de ventas, inventario, utilidad y corte de caja.
- Administrar usuarios, privilegios y accesos.

## 2. Alcance del manual

Este documento explica el uso operativo del sistema de acuerdo con el codigo actual del proyecto. No es un manual tecnico de programacion, aunque incluye notas basicas de instalacion y configuracion para poder ejecutar el sistema durante la capacitacion.

El manual cubre estos modulos:

- Login.
- Dashboard.
- Ventas.
- Inventario.
- Proveedores.
- Reportes.
- Seguridad.

## 3. Requisitos previos

Antes de iniciar la capacitacion, el equipo debe contar con:

- Java 21 instalado.
- MySQL Server activo.
- Maven instalado, si se ejecuta desde codigo fuente.
- Base de datos `sig_cb` creada con el script `src/main/java/org/example/database/sig_cb.sql`.
- Usuario de base de datos configurado en `ConexionBD.java`:
  - Host: `localhost`.
  - Puerto: `3306`.
  - Base de datos: `sig_cb`.
  - Usuario: `sigcb_app`.
  - Password: `SigCB_2026*`.

El proyecto tambien incluye un instalador en `installer/CancinoBike-1.0.exe`, que puede usarse para una demostracion en Windows si el entorno de base de datos ya esta preparado.

## 4. Usuarios iniciales para practica

El script de base de datos crea tres usuarios iniciales:

| Usuario | Password | Rol |
| --- | --- | --- |
| `admin` | `12345` | ADMIN |
| `vendedor` | `12345` | VENDEDOR |
| `cajero` | `12345` | CAJERO |

Durante la capacitacion se recomienda iniciar con `admin`, porque tiene todos los privilegios registrados en la base de datos.

Nota importante: en el codigo actual las contrasenas se validan directamente contra la tabla `usuarios`. Para un entorno productivo se recomienda implementar cifrado/hash de contrasenas.

## 5. Roles y responsabilidades

### Administrador

Responsable de:

- Crear y actualizar usuarios.
- Activar o desactivar cuentas.
- Asignar o quitar privilegios por rol.
- Revisar historial de accesos.
- Consultar reportes generales.
- Supervisar inventario, proveedores y ventas.

### Vendedor

Responsable de:

- Buscar productos.
- Registrar ventas.
- Consultar inventario.
- Revisar reportes permitidos.

### Cajero

Responsable de:

- Registrar ventas de contado.
- Generar ventas que crean ticket digital.
- Consultar corte de caja.

## 6. Flujo general del sistema

1. El usuario inicia sesion desde la pantalla de Login.
2. El sistema valida usuario, password y estado activo.
3. Si el acceso es correcto, se registra en el historial de accesos con estado `CORRECTO`.
4. Si el acceso falla y el usuario existe, se registra como `FALLIDO`.
5. El sistema abre el Dashboard.
6. Desde el Dashboard se accede a Ventas, Inventario, Proveedores, Reportes o Seguridad.
