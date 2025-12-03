# RealtyLens360 - Asistente de Reservas Automatizado

RealtyLens360 es un asistente inteligente diseñado para automatizar el proceso de reservas de servicios de videografía, fotografía, tour 360°, planos 2D y drones para bienes raíces.

## 1. Objetivo del Proyecto

El objetivo es crear un flujo automatizado que permita:

*   **Atención Automática**: Responder a clientes vía Telegram (anteriormente WhatsApp/chat).
*   **Información de Servicios**: Proporcionar detalles sobre paquetes (Básico, Premium, Comercial).
*   **Gestión de Datos**: Solicitar y validar información del cliente.
*   **Gestión de Citas**: Evitar conflictos de agenda validando duplicados.
*   **Integración**: Registrar citas en Airtable y Google Calendar.
*   **Confirmación**: Enviar mensajes finales de confirmación al cliente.

El propósito es simular un sistema real de reservas automatizadas utilizando IA (OpenAI) y n8n.

## 2. Descripción del Flujo

El workflow opera a través de los siguientes pasos:

1.  **Trigger Telegram**: El flujo se activa automáticamente cuando un cliente envía un mensaje al bot de Telegram.
2.  **Limpieza y Formateo**: Se procesa el texto para eliminar ruido y estandarizar la entrada.
3.  **AI Agent (Cerebro)**:
    *   Interpreta la intención del usuario.
    *   Identifica paquete, opción y datos personales.
    *   Genera una respuesta en lenguaje natural.
4.  **Respuesta Inmediata (Telegram)**: Se envía la respuesta generada por la IA al usuario en Telegram para mantener una conversación fluida.
5.  **Structured Output Parser**: Convierte la respuesta de la IA en datos JSON estructurados para el procesamiento interno.
6.  **Validación de Datos**: Verifica si se tienen todos los datos necesarios (Nombre, Teléfono, Fecha, Hora, etc.).
7.  **Consulta a Airtable**: Busca información detallada de los paquetes si es necesario.
8.  **Validación de Duplicados (Real-time)**:
    *   Consulta en Airtable si la fecha y hora solicitadas están disponibles internamente.
    *   **NUEVO**: Consulta en **Google Calendar** si existe algún evento en ese horario para evitar conflictos reales.
9.  **Registro y Calendario**:
    *   Guarda o actualiza el cliente y la cita en Airtable.
    *   Crea el evento correspondiente en Google Calendar.
10. **Confirmación Final (Telegram)**:
    *   Si todo es correcto, envía un mensaje de "Éxito" confirmando la reserva.
    *   Si hay conflicto (Airtable o GCal), envía un mensaje de error sugiriendo otro horario.

## 3. Instrucciones de Ejecución

1.  **Importar Workflow**: Cargar el archivo `AgenteRealtyLens360.json` en n8n.
2.  **Configurar Credenciales**:
    *   **Telegram API**: Configurar el nodo *Telegram Trigger* y *Telegram Response* con el Token de tu bot.
    *   **OpenAI**: Configurar la credencial para el modelo de chat y embeddings.
    *   **Airtable**: Conectar la API Key para lectura/escritura de la base de datos.
    *   **Google Calendar**: Autenticar para la creación de eventos.
3.  **Iniciar el Bot**: Enviar un mensaje de prueba desde Telegram (ej: "Hola, quiero información del paquete Premium").
4.  **Verificar el Flujo**:
    *   Revisar que el bot responda coherentemente.
    *   Comprobar que se cree el registro en Airtable.
    *   Validar que aparezca el evento en Google Calendar.

## 4. Buenas Prácticas Aplicadas

*   ✅ **Validación Robusta**: Asegura que todos los datos del cliente estén presentes antes de reservar.
*   ✅ **Validación Robusta**: Asegura que todos los datos del cliente estén presentes antes de reservar.
*   ✅ **Prevención de Conflictos Real**: Chequeo doble en Airtable y Google Calendar.
*   ✅ **AI Guardrails**: Reglas estrictas para que la IA no alucine confirmaciones falsas y se mantenga en el tema.
*   ✅ **Seguridad**: Manejo estructurado de datos sensibles.
*   ✅ **Experiencia de Usuario**: Respuestas naturales mediante IA y confirmaciones claras.
*   ✅ **Arquitectura Modular**: Separación de lógica de negocio (n8n) e inteligencia (OpenAI).

## 5. Conclusión

RealtyLens360 demuestra cómo integrar múltiples servicios (Telegram, OpenAI, Airtable, Google Calendar) en un flujo de trabajo cohesivo y eficiente, capaz de gestionar reservas del mundo real de manera totalmente autónoma.
