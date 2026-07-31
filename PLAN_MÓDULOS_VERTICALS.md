# Planificación Módulos Mínimos y Verticales - ADempiere para PYMEs

## Contexto
- Proyecto: ADempiere 3.9.4-SNAPSHOT (ERP completo)
- Objetivo: Servicio para PYMEs, no implementación masiva del ERP completo
- Rama: arena/019fb876-adempiere

---

## 1. Módulos Mínimos Recomendados (Fase 1)

Basados en el código existente (`base/src/org/compiere/model` y `org/adempiere/model`):

| Módulo | Componentes del Repo | Complejidad | Prioridad |
|--------|----------------------|-------------|-----------|
| **Clientes / Proveedores** | `MBPartner`, `C_BPartner` | Baja | Alta |
| **Productos / Inventario básico** | `MProduct`, `MStorage` | Media | Alta |
| **Facturación / Pedidos** | `C_Invoice`, `C_Order` | Media | Alta |
| **Catálogo / Reportes simples** | `JasperReports` | Baja | Media |
| **Usuarios / Roles (básico)** | `MRole`, `AD_User` | Baja | Alta |

**No incluir en Fase 1**: Manufactura (`org.eevolution.manufacturing`), Nómina (`hr_and_payroll`), Almacenes avanzados (`warehouse`), Finanzas completas.

---

## 2. Arquitectura del SaaS para PYMEs

- **Multi-tenant**: Un esquema por cliente (`client_001`, `client_002`) en PostgreSQL.
- **API REST**: Nueva capa sobre `base/src` para que la UI moderna (React/Vue) consuma datos sin usar ZK directamente.
- **Contenedores**: Docker con Java 17, Tomcat actualizado, HikariCP configurado.

---

## 3. Verticales Propuestas

### Vertical A: Comercio Minorista (Retail)
- **Necesidad**: Ventas rápidas, inventario básico, facturación simple.
- **Módulos**: Clientes, Productos, Facturación (C_Invoice simplificado), Reporte de ventas diario.
- **Adaptación local**: Configurar impuestos según normativa venezolana (IVA, retenciones).

### Vertical B: Distribución / Mayorista
- **Necesidad**: Pedidos grandes, control de stock, cuentas por cobrar.
- **Módulos**: Clientes, Proveedores, Pedidos (C_Order), Inventario con alertas de mínimo.
- **Adaptación**: Integración con transportistas locales, notas de entrega.

### Vertical C: Servicios / Talleres
- **Necesidad**: Facturación por servicio, control de materiales consumidos.
- **Módulos**: Productos (materiales), Facturación por servicio, Clientes.
- **Adaptación**: Reporte de consumo de materiales por trabajo realizado.

---

## 4. Plan de Implementación Progresiva

| Semana | Acción | Entregable |
|--------|--------|------------|
| 1-2 | Extraer módulos mínimos de `base/src` y limpiar dependencias | Código base ligero |
| 3-4 | Actualizar stack (Java 17, ZK seguro, drivers modernos) | Entorno seguro |
| 5-6 | Crear API REST sobre los módulos mínimos | API funcional |
| 7-8 | Desarrollar UI simplificada (web o móvil) | Demo para PYMEs |
| 9-10 | Configurar multi-tenant y SaaS básico | Primer cliente piloto |
| 11-12 | Vertical específica (Retail o Distribución) | Versión vertical lista |

---

## 5. Riesgos y Mitigaciones

| Riesgo | Mitigación |
|--------|------------|
| Complejidad del código ADempiere | Limitar módulos; no usar Swing ni ZK avanzado |
| Dependencia de base de datos compleja | Usar esquemas aislados; no modificar core |
| Mantenimiento a largo plazo | Documentar cambios; usar commits en `arena/019fb876-adempiere` |
| Escalabilidad con ZK | Reemplazar UI por API + frontend moderno progresivamente |

---

## 6. Recomendación Final

Para sacar provecho real:
1. **No vendas ADempiere como ERP completo**; ofrece **módulos verticales como servicio**.
2. Usa el análisis técnico (`ANALISIS_SEGURIDAD_MEJORAS.md`) para garantizar que cada vertical esté segura y actualizada.
3. Inicia con una **vertical local** (ej. comercio minorista en Lara/Barquisimeto) para validar antes de escalar.
