# MinimarketPro — Demo Comercial v0.6

Demo web interactivo para presentar la idea del sistema a un dueño de minimarket.

## Qué incluye
- Dashboard del dueño
- POS / ventas
- Búsqueda por nombre y código
- Selección de lote/vencimiento
- Pagos simulados: efectivo, Yape/Plin, tarjeta y mixto
- Catálogo de productos
- Inventario por lote y vencimiento
- Compras y recepción
- OCR de factura simulado
- Proveedores
- Cuentas por pagar
- Promociones
- Incidencias y devoluciones a proveedor (flujo demo)
- Reportes y recomendaciones
- Asistente de voz simulado
- Migración de datos simulada
- Usuarios/roles
- Seguridad y respaldos
- SUNAT simulado
- Actualizaciones
- Página de diferencias/propuesta de valor

## Importante
Este proyecto es SOLO un demo comercial:
- Los datos son ficticios y están en memoria.
- No emite comprobantes reales.
- No procesa pagos reales.
- No se conecta realmente a SUNAT.
- OCR y voz son simulaciones.
- No debe usarse para operar una tienda real.

## Ejecutar localmente
```cmd
python -m pip install -r requirements.txt
python -m uvicorn backend.app.main:app --host 127.0.0.1 --port 8000
```
Abrir:
http://127.0.0.1:8000

## Publicación
Incluye Dockerfile y render.yaml para dejarlo listo para un servicio web compatible. Para una demo pública, desplegarlo en una cuenta de hosting y compartir la URL.

## Siguiente etapa
Usar esta demo para validar con el dueño qué pantallas y flujos le resultan más útiles. La versión final tendrá base de datos, usuarios reales, auditoría, backups, integraciones, SUNAT, pagos, sincronización, migración y actualizaciones.

## Pagos e Izipay
Esta versión de demo incorpora el flujo de selección de:
- Efectivo, con monto recibido y cálculo de vuelto.
- QR para Yape/Plin, con QR simulado y confirmación simulada.
- Tarjeta mediante POS Izipay, con flujo de envío de monto → procesamiento → resultado, todo simulado.
- Pago mixto.

La integración real con Izipay no se activa en este demo. Requiere afiliación del comercio, credenciales y validación técnica del dispositivo/servicio de pago elegido.

## Corrección del flujo de cobro
En v0.6 seleccionar un método NO registra automáticamente la venta.
- Efectivo: solicita monto recibido, calcula vuelto y bloquea el cierre si falta dinero.
- QR Yape/Plin: espera una confirmación simulada antes de registrar.
- Tarjeta Izipay: muestra el flujo terminal → resultado y requiere aprobación simulada.
- Mixto: solicita las dos partes y exige que sumen exactamente el total.

## Corrección v0.6
Se corrigió el cierre de venta después de la confirmación del método de pago. Ahora:
- Efectivo valida el monto recibido y registra la venta al confirmar.
- QR Yape/Plin registra la venta al pulsar la aprobación simulada.
- Tarjeta Izipay registra la venta al pulsar la aprobación simulada.
- Mixto valida que las dos partes sumen exactamente el total y luego registra.
- Al registrar una venta, el demo descuenta las unidades del lote seleccionado y del stock del producto.
