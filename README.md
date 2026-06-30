# Sistema de Gestión de Ventas — Supermercado

Proyecto integrador desarrollado para la materia **Base de Datos Aplicadas** en la Universidad Nacional de la Maranza (UNlaM). Sistema completo de gestión de ventas para una cadena de supermercados, implementado íntegramente en **Microsoft SQL Server**.

## Descripción

Base de datos relacional diseñada para administrar las operaciones de una cadena de supermercados con múltiples sucursales. El sistema abarca desde la gestión de empleados y productos hasta el registro de ventas, facturación, importación de datos desde Excel y generación de reportes.

## Tecnologías utilizadas

- **Microsoft SQL Server** — motor de base de datos
- **SQL Server Management Studio (SSMS)** — entorno de desarrollo
- **T-SQL** — lenguaje de consulta y programación
- **OLE DB / ACE.OLEDB 16.0** — importación de archivos Excel (.xlsx)

## Arquitectura — Esquemas de la base de datos

El sistema está organizado en **esquemas separados** que dividen responsabilidades entre la lógica de negocio y el acceso a datos:

| Esquema | Descripción |
|---|---|
| `gestion_tienda` / `datos_tienda` | Sucursales, puntos de venta, empleados, cargos |
| `gestion_productos` / `datos_productos` | Catálogo de productos y líneas de producto |
| `gestion_ventas` / `datos_ventas` | Ventas, facturas, detalle de venta, medios de pago |
| `gestion_clientes` / `datos_clientes` | Clientes (miembro / regular) |
| `reportes` | Stored Procedures de reportes gerenciales |
| `datos_notas_credito` | Emisión y gestión de notas de crédito |
| `encriptacion` | Encriptación de datos sensibles de empleados |
| `inserts` | Importación masiva de datos desde archivos Excel |

## Funcionalidades principales

### Gestión de entidades
- ABM completo (Alta, Baja lógica y Modificación) de **sucursales**, **puntos de venta**, **empleados**, **productos** y **clientes**, implementado mediante Stored Procedures con validaciones de negocio.

### Ventas y Facturación
- Registro de ventas con detalle por producto, medio de pago (efectivo, tarjeta, etc.) y empleado.
- Generación de **facturas** (tipo A, B o C) con cálculo de IVA.
- Control de estados de factura: Pendiente, Pagada y Cancelada.
- Soporte de precios en pesos (ARS) y dólares, con tabla de cotización USD actualizable.

### Importación de datos
- Stored Procedures para importar el **catálogo de productos**, datos de **clientes** y registros de **ventas históricas** desde archivos `.xlsx` mediante OLE DB.

### Reportes
- Reporte de ventas con información cruzada de factura, sucursal, cliente, producto, empleado, medio de pago, fecha y hora.

### Roles y permisos
- Esquema de seguridad con dos roles diferenciados:
  - **`cajeros`**: acceso a operaciones de ventas y clientes.
  - **`supervisores`**: acceso completo al sistema, incluyendo reportes y notas de crédito.

### Encriptación
- Encriptación **AES-256** de datos personales de empleados (CUIL, documento, dirección) mediante clave simétrica protegida por certificado X.509.

### Backups
- Stored Procedures para la gestión y automatización de copias de seguridad de la base de datos.

### Notas de crédito
- Stored Procedures para la emisión y administración de notas de crédito asociadas a facturas.

## Estructura del repositorio

```
COM2900_02_proyecto/
├── E03_01_Creacion_BD.sql          # Creación de la BD, esquemas y tablas
├── E03_02_Funciones.sql            # Funciones auxiliares de validación
├── E03_03_SP_Tienda.sql            # SPs: sucursales, puntos de venta, empleados
├── E03_04_Test_Tienda.sql          # Tests de tienda
├── E03_05_SP_Cliente.sql           # SPs: clientes
├── E03_06_Test_clientes.sql        # Tests de clientes
├── E03_07_SP_Producto.sql          # SPs: productos y líneas de producto
├── E03_08_Test_productos.sql       # Tests de productos
├── E03_09_SP_ventas.sql            # SPs: ventas, facturas y medios de pago
├── E03_10_Test_ventas.sql          # Tests de ventas
├── E04_01_SP_Importacion.sql       # SPs: importación de catálogo y clientes (XLSX)
├── E04_02_SP_importacion.sql       # SPs: importación de ventas históricas (XLSX)
├── E04_03_SP_reportes.sql          # SPs: reportes de ventas
├── E04_04_Test_reportes.sql        # Tests de reportes
├── E05_01_Creacion_Roles.sql       # Roles y permisos (cajeros / supervisores)
├── E05_02_Test_usuarios.sql        # Tests de usuarios y roles
├── E05_03_SP_notaCredito.sql       # SPs: notas de crédito
├── E05_04_Test_notaCredito.sql     # Tests de notas de crédito
├── E05_05_SP_Encriptacion.sql      # SPs: encriptación AES-256 de empleados
├── E05_06_Test_Encriptacion.sql    # Tests de encriptación
├── E05_07_SP_Backups.sql           # SPs: gestión de backups
├── E05_08_Tests_Backups.sql        # Tests de backups
└── Inserts.sql                     # Datos iniciales del sistema
```

## Cómo ejecutar

1. Abrir **SQL Server Management Studio (SSMS)**.
2. Ejecutar los scripts en orden numérico, comenzando por `E03_01_Creacion_BD.sql`.
3. Verificar la ejecución con los scripts de test correspondientes (`*_Test_*.sql`).

> Los scripts de importación (`E04_01` y `E04_02`) requieren tener instalado el proveedor **Microsoft ACE OLE DB 16.0** y acceso a los archivos `.xlsx` de datos.

**Materia:** Base de Datos Aplicadas 
**Universidad:** Universidad Nacional de la Matanza (UNlaM) 
**Fecha de entrega:** Noviembre 2024
