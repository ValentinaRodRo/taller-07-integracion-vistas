# Taller 7 – Integración de Vistas de Arquitectura
Curso: Arquitectura Empresarial – Universidad de La Sabana  
Cliente aplicado: **CompuLens** (Laboratorio óptico – Gestión de pedidos y trazabilidad)

---

## 🎯 Objetivo del Taller

El propósito de este taller fue **integrar todas las vistas arquitectónicas trabajadas durante el curso** (negocio, información, aplicaciones, infraestructura y seguridad) en una representación única y coherente.

Esta integración permite:

- Visualizar cómo fluye la información a través de las capas.
- Entender cómo se soportan los procesos del cliente desde la tecnología.
- Evidenciar dependencias críticas, componentes clave y puntos de control.
- Representar la arquitectura futura (TO-BE) del cliente real.

---

## 📁 Estructura del Repositorio

```
taller-07-integracion-vistas/
├── README.md
├── clase/
│ ├── tablero-farmapp.drawio
│ └── notas.md
├── entrega/
│ ├── tablero-integrado-cliente.drawio
│ ├── Informe.md
│ └── Referencias.md
```

### 📌 Contenido de cada carpeta

- **clase/**  
  Contiene las notas y el tablero desarrollado en la sesión para el caso base **FarmApp**, usando las 5 vistas arquitectónicas.

- **entrega/**  
  Incluye todos los entregables del cliente real (CompuLens):
  - *tablero-integrado-cliente.drawio*: diagrama unificado con todas las vistas.
  - *Informe.md*: narrativa técnica con análisis, decisiones y reflexiones.
  - *Referencias.md*: fuentes consultadas y ejemplos reales de documentación arquitectónica.

---

## 🧪 Parte 1 – Caso Base (FarmApp)

En clase se integraron las vistas del caso FarmApp:

- **Negocio:** proceso de compra, pago, despacho y entrega.  
- **Información:** entidades como Cliente, Pedido, Inventario, Pago.  
- **Aplicaciones:** App móvil, Web, POS, CRM, API Gateway, logística.  
- **Infraestructura:** nube híbrida, replicación regional, CDN, VPN.  
- **Seguridad:** OAuth2, TLS, WAF, RBAC, monitoreo antifraude.

Todo fue consolidado en un tablero visual (incluido en `clase/tablero-farmapp.drawio`) y acompañado con notas explicativas (`clase/notas.md`).

---

## 🧠 Parte 2 – Cliente Real: CompuLens

Para el cliente real se realizó la integración completa de vistas, representando la arquitectura TO-BE del laboratorio óptico **CompuLens**, que busca digitalizar y automatizar la recepción de pedidos de sus ópticas aliadas.

### ✔ Vistas integradas en el tablero final

#### **1. Vista de Negocio**
- Recepción de pedidos vía WhatsApp o WebApp.
- Normalización del pedido y validación.
- Integración automática con ERP Ocular.
- Generación de guías y trazabilidad.
- Pagos opcionales.
- Monitoreo y operación.

#### **2. Vista de Información**
- Entidades: Pedido, Cliente Óptica, Estado, Guía, Pago, Producción.
- Base de datos de pedidos como repositorio centralizado.
- Integración de datos con ERP para estados de producción.

#### **3. Vista de Aplicaciones**
- WebApp / formulario digital.
- Orquestador de integración.
- Backend de pedidos.
- API Gateway.
- WhatsApp + OCR para pedidos automatizados.
- Sistemas externos: ERP Ocular, mensajería, pasarela de pagos.

#### **4. Vista de Infraestructura**
- CDN + WAF en la capa de borde.
- Nube para backend y orquestador.
- Sistemas del laboratorio alojados localmente (ERP).
- Conexiones seguras vía HTTPS.
- Componentes desacoplados mediante API Gateway.

#### **5. Vista de Seguridad**
- WAF para protección de entrada.
- Métricas y logs centralizados.
- SIEM para correlación de eventos.
- HTTPS en todas las integraciones.
- Auditoría y monitoreo básico.

### ✔ Resultado visual

El diagrama final se encuentra en:

> `entrega/tablero-integrado-cliente.drawio`  

y refleja todas las capas interconectadas en un único tablero arquitectónico.

---

## 📄 Informe y análisis

El documento `entrega/Informe.md` explica:

- Cómo se integraron las vistas.  
- Decisiones arquitectónicas clave.  
- Justificación de la separación por capas.  
- Reflexión crítica sobre coherencia y retos del cliente.  
- Ejemplos reales tomados como referencia.  

El archivo `Referencias.md` contiene la bibliografía y materiales utilizados.

---

## 🧩 Principales decisiones arquitectónicas del TO-BE de CompuLens

- Separar la capa de borde (CDN + WAF) para mejorar seguridad y desempeño.
- Introducir un **orquestador** que desacopla WebApp, WhatsApp y ERP.
- Mantener el ERP como *sistema de verdad*, consumiendo estados en tiempo real.
- Establecer monitoreo centralizado (métricas/logs) y un SIEM para detección de anomalías.
- Implementar entrada multicanal de pedidos (WebApp, WhatsApp + OCR).
- Cifrar todas las comunicaciones externas con HTTPS.

---

## 📝 Licencia

Este taller hace parte del curso de **Arquitectura Empresarial – Universidad de La Sabana**.  
Uso académico bajo licencia MIT.

