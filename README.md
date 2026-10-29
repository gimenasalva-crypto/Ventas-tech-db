# Checkpoint Módulo 3 · Ventas_Tech_DB (TechStore)

**Autora:** Salva, María Gimena

**Motor:** SQL Server Express 17, ejecutado en SQL Server Management Studio 22

## Qué hace el script

`ventas_tech_db.sql` crea la base `Ventas_Tech_DB` de TechStore, con un modelo relacional normalizado hasta 3NF:

```
categorias (1) ──── (N) productos (1) ──── (N) ventas (N) ──── (1) clientes
```

| Tabla | Tipo | Clave primaria | Claves foráneas |
|---|---|---|---|
| `categorias` | Dimensión | `id_categoria` | — |
| `clientes` | Dimensión | `id_cliente` | — |
| `productos` | Dimensión | `id_producto` | `id_categoria` → `categorias` |
| `ventas` | Hechos | `id_venta` | `id_cliente` → `clientes`, `id_producto` → `productos` |

## Estructura del script

1. **DROP:** elimina las tablas si existen, en orden inverso a las dependencias (ventas → productos → clientes → categorias). Por eso el script es repetible.
2. **CREATE:** crea primero las dimensiones y al final la tabla de hechos, con PK, FK, `UNIQUE` en el email y valores por defecto en `stock` y `activo`.
3. **INSERT:** carga los 25 registros (4 categorías, 5 clientes, 6 productos y 10 ventas) con las columnas explicitadas.
4. **VALIDACIÓN:** cuatro `SELECT` que deben devolver 4, 5, 6 y 10 filas.

Los precios usan `DECIMAL(10,2)` y las fechas `DATE`, para poder sumar, promediar y analizar en el tiempo sin errores de redondeo.

## Ejecución y validación

El script se ejecutó completo en SQL Server dos veces seguidas, sin errores. Las consultas de validación devolvieron 4, 5, 6 y 10 filas.

Evidencia: `ejecucion_ventas_tech.png`.

## Cómo ejecutarlo

1. Abrir `ventas_tech_db.sql` en SSMS (Archivo → Abrir → Archivo).
2. Ejecutar todo con **F5**. El script crea la base si no existe y la selecciona.
3. Revisar la pestaña **Resultados**: aparecen las cuatro tablas con 4, 5, 6 y 10 filas.
