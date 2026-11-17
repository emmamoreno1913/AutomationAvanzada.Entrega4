Práctico 4 – TechSolutions Multiagente

Alumno: Emmanuel Moreno
Proyecto: Sistema de atención automatizada con n8n
Entrega: Checkpoint 4

1. Descripción del proyecto
El proyecto consiste en un sistema de atención automatizada para TechSolutions, desarrollado en n8n. Su objetivo es recibir consultas de clientes, identificar el motivo de contacto, recuperar información de conversaciones anteriores y derivar cada solicitud al circuito correspondiente.
La solución integra herramientas externas para gestionar contactos, generar borradores de correo y notificar al equipo responsable.

2. Integraciones utilizadas
Conectores principales
Salesforce CRM: consulta, creación y actualización de contactos.
Gmail: recepción de correos y generación de borradores para revisión humana.
Slack: notificaciones de casos pendientes de atención en el canal correspondiente.
Las tres integraciones principales se conectaron mediante credenciales OAuth2 en n8n.
Integraciones complementarias
Airtable: almacenamiento de información y memoria persistente de las conversaciones.
Groq: procesamiento de lenguaje natural y clasificación de consultas mediante modelos de IA.

3. Funcionamiento del workflow
El flujo principal sigue estas etapas:
Recepción del correo: Gmail Trigger detecta los nuevos mensajes.
Filtro de respuestas automáticas: un nodo IF identifica mensajes automáticos, respuestas de ausencia y correos no entregables para evitar su procesamiento.
Obtención y preparación de datos: se recupera el contenido del correo y se organizan los datos del cliente.
Gestión de contactos en Salesforce: se busca el contacto por correo electrónico. Si existe, se actualiza; si no existe, se crea uno nuevo.
Memoria conversacional: se consulta Airtable para recuperar información previa del cliente y mantener el contexto de la conversación.
Clasificación mediante IA: el modelo identifica el tipo de consulta y determina si corresponde a una consulta comercial, técnica, un reclamo o una solicitud de atención humana.
Enrutamiento: el nodo Switch dirige cada consulta al circuito correspondiente.
Ejecución de Workers: las consultas comerciales se procesan mediante Worker 1 - Consulta de Productos. Los reclamos y las consultas técnicas utilizan Worker 2 - Atención y Gestión de Consultas.
Derivación humana: cuando se requiere intervención de una persona, se prepara un borrador en Gmail y se envía una notificación a Slack.

4. Control humano (Human in the Loop)
La solución incorpora un mecanismo de revisión humana.
Los casos que requieren intervención se notifican al equipo responsable mediante Slack y generan un borrador en Gmail con los datos del cliente, el motivo de contacto y el resumen del caso.
Los correos no se envían automáticamente: quedan como borradores para que una persona pueda revisarlos y decidir su envío.

5. Pruebas realizadas
Se realizaron pruebas de funcionamiento para verificar los principales circuitos

6. Seguridad y credenciales
Las conexiones con Salesforce, Gmail y Slack se configuraron mediante OAuth2 desde el administrador de credenciales de n8n.
Se procura utilizar únicamente los permisos necesarios para las operaciones del proyecto.
Importante: el archivo JSON de entrega no debe contener contraseñas, tokens ni secretos de autenticación. Las credenciales deben estar configuradas en la instancia de n8n donde se importe el workflow.

7. Archivos de entrega
checkpoint4_emmanuel_moreno.json: exportación del workflow principal de n8n.
README.md: documentación del proyecto y descripción de su funcionamiento.

8. Evidencias
Se adjuntan capturas de pantalla que muestran:
Credencial OAuth2 de Salesforce conectada.
Credencial OAuth2 de Gmail conectada.
Credencial OAuth2 de Slack conectada.

9. Conclusion
El proyecto integra automatización, inteligencia artificial y conectores empresariales para optimizar la atención al cliente de TechSolutions.
La solución permite clasificar consultas, gestionar contactos, consultar productos, conservar información de las conversaciones y derivar los casos que requieren intervención humana, manteniendo controles de seguridad y revisión antes del envío de comunicaciones.

Proyecto: TechSolutions Multiagente
Herramienta de automatización: n8n
Estado: Implementación y pruebas funcionales realizadas.
