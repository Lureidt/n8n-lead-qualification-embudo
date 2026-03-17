# n8n-lead-qualification-embudo
Captación y Filtrado de Clientes cualificados al Instante, para comprobar que son el tipo de cliente objetivo para la constructora
Automatización de captación y filtrado de leads (n8n + Telegram)

El problema que quería resolver
En la gestión de clientes, revisar solicitudes de presupuesto a mano es un cuello de botella. Creé este flujo en n8n para eliminar por completo el data entry y asegurarme de que el equipo comercial reciba una alerta inmediata solo cuando entra un cliente de alto valor (VIP).

Stack utilizado: n8n, API de Telegram, Tally Forms y Google Sheets.

Cómo funciona la arquitectura:

Captura y trazabilidad: El usuario inicia la conversación con un bot en Telegram, que le devuelve un enlace a un formulario de Tally. Para mantener la trazabilidad, configuré el enlace para que inyecte el chat_id de Telegram de forma oculta en el formulario.

Extracción (Webhook): Al enviar el formulario, n8n captura la respuesta en tiempo real.

Guardado y enrutamiento en paralelo: A partir de aquí, el flujo hace dos cosas a la vez para evitar bloqueos:

Por un lado, mapea los datos y actualiza una fila en Google Sheets usando el ID oculto para encontrar al usuario.

Por otro, evalúa la respuesta del presupuesto. Si el cliente seleccionó la opción superior a 300.000€, el sistema dispara una alerta prioritaria a mi Telegram. Si el presupuesto es menor, el bot le envía un mensaje automático de seguimiento al cliente.
