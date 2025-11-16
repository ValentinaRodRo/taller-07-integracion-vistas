# Notas de Clase – Taller 7: Integración de Vistas de Arquitectura  
Caso Base: FarmApp (Cadena de Farmacias con E-Commerce)

Estas notas registran el análisis realizado en clase durante la construcción del tablero de vistas integradas de FarmApp. El objetivo fue entender cómo se conectan las capas de negocio, información, aplicaciones, infraestructura y seguridad dentro de una arquitectura empresarial.

---

## 1. Objetivo de la Actividad
Integrar en un único tablero las vistas arquitectónicas de FarmApp para:
- Visualizar relaciones entre capas.
- Identificar dependencias críticas.
- Entender cómo la tecnología soporta los procesos del negocio.
- Practicar la representación integrada (similar a TOGAF + ArchiMate).

---

## 2. Vista de Negocio (Procesos Principales)

**Proceso de compra de medicamentos:**
1. Cliente consulta productos (web/app).
2. Cliente agrega productos al carrito.
3. Validación de receta (cuando aplica).
4. Confirmación del pedido.
5. Pago digital.
6. Preparación del pedido en farmacia.
7. Despacho o recogida en tienda.
8. Entrega y notificación al cliente.

**Observaciones:**
- La validación de receta genera flujo alterno.
- El proceso depende de inventario en tiempo real.
- El despacho involucra logística externa/interna según ubicación.

---

## 3. Vista de Información (Modelo ERD Simplificado)

**Entidades clave discutidas:**
- **Cliente**
- **Producto**
- **Inventario**
- **Pedido**
- **DetallePedido**
- **Pago**
- **Dirección**
- **Receta**
- **Entrega**
- **Promoción**

**Relaciones destacadas:**
- Cliente realiza pedidos.
- Pedido contiene productos.
- Producto depende del inventario.
- Pedido genera pago y entrega.
- Receta se asocia a ciertos tipos de productos.

**Conclusión:**  
Los datos transaccionales (Pedido, Pago, Entrega) se mueven entre múltiples aplicaciones, por lo que necesitan consistencia y sincronización.

---

## 4. Vista de Aplicaciones (Sistemas Involucrados)

Aplicaciones identificadas y su rol:

- **App móvil FarmApp:** interfaz principal de clientes.
- **Web E-Commerce:** canal digital alterno.
- **POS en tienda:** ventas presenciales y control de inventario local.
- **CRM:** gestión de clientes, promociones y fidelización.
- **Sistema de inventario:** control de stock, sincronización entre tiendas.
- **Sistema de logística / tracking:** seguimiento del pedido.
- **Pasarela de pagos:** validación y procesamiento de transacciones.
- **Motor de recomendaciones:** personalización de productos.
- **API Gateway:** punto central de integración.

**Puntos clave:**
- El API Gateway es el integrador principal entre aplicaciones digitales y backend.
- POS e inventario local requieren replicación periódica.
- CRM alimenta descuentos y campañas personalizadas.

---

## 5. Vista de Infraestructura

Infraestructura identificada:

- **Nube (híbrida):**
  - Backend y API Gateway.
  - Base de datos principal.
  - Motor de recomendaciones.
  - Servidor web.
- **Infraestructura en tiendas físicas:**
  - POS.
  - Servidor local con BD replicada.
  - Conectividad VPN.
- **Servicios externos:**
  - CDN para contenido estático.
  - Pasarela de pagos.
  - Sistema de mensajería (notificaciones).
  
**Observación:**  
La replicación en tiendas permite continuidad del negocio, incluso con fallos de red.

---

## 6. Vista de Seguridad

Controles discutidos:

- **Autenticación:** OAuth2/JWT para apps móviles y web.
- **Autorización:** RBAC para empleados (POS) y perfiles de clientes.
- **Cifrado en tránsito:** HTTPS/TLS 1.2+.
- **Cifrado en reposo:** BD de clientes y pagos protegida.
- **WAF:** protección para la plataforma e-commerce.
- **Firewall + segmentación:** sedes y nube.
- **Monitoreo y alertas:** eventos de fraude, uso anómalo, intentos de acceso.
- **Auditoría:** registros de transacciones y movimientos de inventario.

**Conclusión:**  
Seguridad no debe verse como una capa final, sino como una envoltura que cubre todas las demás vistas.

---

## 7. Integración entre las Vistas

Durante el ejercicio se identificaron relaciones importantes:

- **Negocio → Aplicaciones:** el proceso de compra define qué módulos del backend existen.
- **Información → Aplicaciones:** las entidades determinan los endpoints y modelos de datos.
- **Aplicaciones → Infraestructura:** la réplica del inventario requiere servidores locales + nube.
- **Todo → Seguridad:** cualquier flujo de datos de cliente implica cifrado y control de acceso.

Una decisión clave:  
> La sincronización del inventario debe ser casi en tiempo real para evitar ventas de productos agotados.

---

## 8. Conclusiones de Clase

- La arquitectura integrada ofrece una visión 360° del funcionamiento de FarmApp.
- El API Gateway es un punto crítico que conecta casi todas las capas.
- La replicación de inventario y la logística son los principales retos tecnológicos.
- La seguridad debe abarcar todos los flujos, no solo la aplicación web.

Estas notas acompañan al archivo `tablero-farmapp.drawio`.

