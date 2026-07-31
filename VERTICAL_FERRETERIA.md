# Vertical: Ferretería (PYME)

## Qué necesita una ferretería
- Productos por categoría (tornillos, pintura, herramientas)
- Ventas al mostrador (rápido)
- Control básico de stock (no quedarse sin productos)
- Facturación simple con impuestos
- Cuenta por cobrar básica (clientes que pagan después)

## Módulos a usar del repo ADempiere
- `MBPartner` (clientes)
- `MProduct` (productos con categorías)
- `C_Invoice` (ventas/facturas simples)
- `C_Order` (pedidos rápidos)
- `JasperReports` (reporte de ventas del día)

## Qué NO usar
- Manufactura (`org.eevolution.manufacturing`)
- Nómina (`hr_and_payroll`)
- Almacén avanzado (`warehouse`)
- Finanzas completas

## Funcionalidades de la página web
1. Buscar producto por nombre
2. Agregar al carrito / factura
3. Imprimir factura simple
4. Ver cuánto queda en inventario
5. Reporte: ventas del día y productos más vendidos

## Modelo de venta
- Servicio mensual para ferreterías locales
- El cliente entra con usuario, factura y listo
- Tú administras todo (multi-tenant)
