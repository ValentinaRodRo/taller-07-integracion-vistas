# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 6 - Integracion_Vistas_

## 👥 Integrantes del equipo
- Juan Andres Lacouture Daza  
- Valentina Rodriguez Romero  

---

## 🧠 Descripción general del trabajo
El objetivo del taller fue integrar de manera coherente varias vistas arquitectónicas (procesos, aplicaciones, infraestructura, seguridad y datos) para representar el funcionamiento y las necesidades del cliente del caso real: **Compulens**, un laboratorio óptico que recibe pedidos de diferentes ópticas aliadas.  
Durante la actividad analizamos el proceso AS-IS, construimos vistas TO-BE, discutimos cómo se conectan entre sí y finalmente consolidamos todo en un tablero arquitectónico unificado. Esta integración permitió obtener una visión clara, no fragmentada, del negocio y de cómo la tecnología lo soporta.

---

## 🔧 Proceso de desarrollo
El trabajo se desarrolló iniciando por el entendimiento del **proceso AS-IS**, revisando los canales actuales (WhatsApp, llamadas, mensajería física, recepción presencial y digitación manual en ERP Ocular). A partir de esto, modelamos el **BPMN TO-BE**, incorporando el chatbot con OCR, la digitalización completa del pedido y las integraciones automáticas.

Posteriormente construimos la vista de **aplicaciones y componentes**, identificando los elementos críticos: Web/App de pedidos, orquestador, API Gateway, ERP Ocular y Chatbot. Luego pasamos a la vista de **infraestructura**, donde ubicamos servidores, zonas de borde (CDN, WAF), redes y bases de datos.  

Finalmente, refinamos las relaciones, flechas, flujos y responsabilidades para obtener un tablero claro, escalable y comprensible.

---

## 🧩 Análisis del modelo propuesto
El modelo está estructurado en capas:  
- **Capa Cliente:** actores principales (Óptica, Jefe Administrativo, Jefe de Producción).  
- **Ingreso/Borde:** componentes que reciben peticiones (CDN, WAF, API Gateway, Chatbot OCR).  
- **Aplicación de Pedidos:** Web/App, recepción digital, orquestador e integración, backend.  
- **Sistemas Externos:** ERP Ocular, mensajería y pasarela de pago.  
- **Datos de negocio:** base de datos de pedidos.  
- **Operación/Seguridad:** monitoreo, métricas, SIEM.

La arquitectura representa fielmente las necesidades del cliente al enfocarse en eliminar la digitación manual, reducir errores, aumentar trazabilidad y proporcionar validaciones automatizadas.  
Entre los supuestos tomados están: que el ERP ofrece APIs para integración, que la pasarela de pago puede conectarse directamente desde el backend, y que Compulens cuenta con infraestructura mínima para monitoreo centralizado.

---

## 🔗 Articulación de las vistas y decisiones clave
Las vistas se articularon a partir de elementos comunes:

- El **BPMN TO-BE** define el flujo operativo y sirvió como mapa para ubicar actores, sistemas y acciones.
- La vista de **aplicaciones** traduce cada etapa del BPMN en componentes lógicos concretos (chatbot, orquestador, backend, integraciones).
- La vista de **infraestructura** posiciona estos componentes en entornos reales (zona de borde, nube, ERP local).
- La vista de **seguridad** une todo mediante controles transversales: autenticación, HTTPS, WAF, logs, SIEM.

### Decisiones clave:
- Separar la capa de borde (CDN, WAF y API Gateway) para mitigar ataques y dar escalabilidad.  
- Centralizar la orquestación de integraciones para desacoplar el frontend del ERP.  
- Mantener el ERP externo como fuente única de verdad para datos de producción.  
- Agregar monitoreo + SIEM para reforzar la trazabilidad y la seguridad end-to-end.

---

## 🧪 Reflexión crítica sobre la coherencia de la arquitectura
La arquitectura es coherente en el sentido de que cada vista se alinea con el proceso y con las necesidades reales del cliente. Los actores, flujos y componentes se rastrean de extremo a extremo sin contradicciones. Los datos fluyen de manera natural entre vistas, y hay consistencia entre el BPMN, la aplicación y la infraestructura.

Sin embargo, hay aspectos a mejorar:  
- El modelo podría profundizar más en la autenticación y autorización granular.  
- El ERP depende de integraciones que no están totalmente definidas (API o conectores).  
- No se ilustran aspectos de resiliencia (backups, alta disponibilidad, DRP).  

En una siguiente iteración, se recomienda incluir vistas más profundas de seguridad, vista de despliegue físico y un catálogo de servicios.

---

## 🌍 Ejemplos reales de documentación de vistas
### Tema investigado
Buenas prácticas y ejemplos reales de documentación de vistas arquitectónicas en empresas de manufactura y retail (Casos: Mercado Libre, Rappi, Luxottica, DHL Supply Chain).

### Resumen
En empresas del sector manufactura y operaciones logísticas, la documentación de vistas suele seguir marcos como **C4, TOGAF, ArchiMate y BPMN**. Normalmente, combinan vistas de procesos, vistas de aplicaciones y vistas de integración para mostrar cómo se conectan sistemas legacy con nuevas capas digitales.  
Un patrón común es la separación clara entre capa de borde (API Gateway, WAF), capa de servicios (orquestación), capa de negocio (ERP) y capa de análisis/operación (monitoreo, SIEM).

También observamos que empresas como Luxottica y Rappi documentan sus vistas con diagramas integrados que muestran trazabilidad entre actores → procesos → datos → sistemas → infraestructura, lo cual coincide con el enfoque que aplicamos en este taller y fortalece la claridad arquitectónica.

---

## 📈 Diagrama final entregado
> **Inserte aquí la imagen exportada desde draw.io**  
<img width="1451" height="972" alt="Compulens-tablero drawio" src="https://github.com/user-attachments/assets/b2cb85bb-19f7-4469-b72c-96be1d13e257" />


---

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento     | Tipo        | Descripción                                              | Responsable     |
|-------------------------|-------------|----------------------------------------------------------|-----------------|
| Cliente Óptica          | Actor       | Envía pedidos mediante WhatsApp o Web/App               | Óptica aliada   |
| Chatbot + OCR           | Componente  | Interpreta formularios enviados por WhatsApp            | Compulens       |
| API Gateway             | Componente  | Expone endpoints unificados y protege el backend        | Compulens TI    |
| Orquestador/Integración | Componente  | Normaliza datos y conecta con ERP Ocular                | Compulens TI    |
| Backend de pedidos      | Servicio    | Gestiona pedidos, pagos, integraciones                  | Compulens TI    |
| ERP Ocular              | Sistema ext | Sistema principal de gestión y producción del laboratorio| Proveedor ERP   |
| Base de datos de pedidos| Datos       | Almacena pedidos digitalizados y estados                | Compulens       |


---

## 📚 Referencias
- [1] OMG. *BPMN Specification*. https://www.omg.org/spec/BPMN/  
- [2] TOGAF Standard, Open Group. 2023.  
- [3] Simon Brown. *The C4 Model*. https://c4model.com/  
- [4] Luxottica Tech Blog – Case Studies de Integración.  
- [5] Mercado Libre Arquitectura – Public Docs.

---

_Este documento hace parte de la entrega del taller 6 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
