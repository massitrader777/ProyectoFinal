1. OBJETIVO DEL PROYECTO 
RealtyLens360 es un asistente inteligente diseñado para automatizar el proceso de reservas de servicios de videografía, fotografía, tour 360°, planos 2D y drones para bienes raíces, según las necesidades del cliente.

El objetivo del proyecto es crear un flujo que permita:
●	Atender clientes automáticamente via WhatsApp/chat.

●	Proporcionar información sobre los paquetes (Básico, Premium, Comercial).

●	Solicitar y validar datos del cliente.

●	Evitar choques de agenda con validación de citas duplicadas.

●	Registrar la cita en una base de datos (Airtable).

●	Responder con un mensaje final de confirmación.

El propósito es simular un sistema real de reservas automatizadas usando IA y automatización.

2. DESCRIPCIÓN DEL FLUJO 
El workflow funciona mediante los siguientes pasos:
1.	Trigger WhatsApp / Chat

 El flujo se activa automáticamente cuando un cliente envía un mensaje.

2.	Limpieza y formateo del texto

 Se elimina ruido, espacios y datos innecesarios antes de procesarlo.

3.	AI Agent (Interpretación del mensaje)

 La IA identifica el paquete solicitado, la opción, la intención del usuario y los datos proporcionados.

4.	Structured Output Parser

 Convierte la respuesta de la IA en datos estructurados (paquete, opción, nombre, teléfono, fecha, hora).

5.	Consulta a Airtable (List Records)

 Se busca la información del paquete y su descripción en la base de datos.

6.	Validación de datos con IF

 El flujo revisa si el cliente ya dio todos los datos necesarios o si falta alguno.

7.	Validación de citas duplicadas

 Se busca en Airtable si ya existe una cita en la misma fecha y hora para evitar choques en la agenda.

8.	Registro de la cita (Upsert Record)

 Se guarda o actualiza la información del cliente y la cita en Airtable.

9.	Mensaje final de confirmación

 El flujo envía al cliente un mensaje con el paquete elegido y la fecha y hora confirmada.

Este flujo representa una automatización completa y funcional para gestionar citas reales.

3. INSTRUCCIONES DE EJECUCIÓN 
1.	Abrir el workflow principal en la herramienta (n8n o la plataforma correspondiente).

2.	Verificar que las credenciales de Airtable están correctamente configuradas.

3.	Activar el webhook o trigger para recibir mensajes desde WhatsApp/chat.

4.	Enviar un mensaje de prueba desde el cliente, por ejemplo:

○	“Quiero el paquete Básico opción 1”

5.	Verificar:

○	Interpretación de la IA

○	Consulta a Airtable

○	Validación de datos

○	Registro de la cita

○	Respuesta del bot

6.	Confirmar que se evita una cita duplicada enviando una fecha/hora ya ocupada.

7.	Revisar que el mensaje final incluya toda la información de manera correcta.


4. DIAGRAMA DEL WORKFLOW
 
5. Buenas prácticas aplicadas
✔ Validación de datos del cliente
✔ Evitar duplicados mediante búsquedas en Airtable
✔ Separación clara de lógica y procesamiento
✔ Manejo seguro de datos sensibles (nombre, teléfono)
✔ Respuestas limpias, sin filtrar datos innecesarios
✔ IA con salida estructurada para evitar errores de interpretación
6. Conclusión
RealtyLens360 representa una solución automatizada capaz de gestionar reservas para servicios inmobiliarios de manera inteligente y eficiente.
El flujo integra IA, validación de datos, manejo de base de datos y mensajería automática, simulando un sistema real en producción.
Gracias a esta arquitectura, un tercero puede replicar y adaptar el proyecto con facilidad.
 
7. Proceso detallado (con capturas de pantalla)
Trigger del Sistema
Cuando un cliente envía un mensaje por WhatsApp.
📸 Inserta aquí captura del nodo Trigger
Explicación:
Este nodo recibe el mensaje y activa todo el flujo.
 
Limpieza del Mensaje
Edición del texto para evitar errores.
📸 Inserta aquí captura del nodo Edit / Transform
Explicación:
Se eliminan caracteres innecesarios para mejorar la interpretación del modelo.
 
Interpretación con AI Agent
El modelo analiza la intención y los datos.
📸 Inserta aquí captura del nodo AI Agent
Explicación:
El asistente detecta: nombre, paquete, opción, fecha, hora e intención del cliente.
 
Conversión a Datos Estructurados
Parser que organiza la salida de la IA.
📸 Inserta captura del Structured Output Parser
Explicación:
Convierte el texto del modelo en JSON limpio para uso interno del flujo.
 
Validación de Datos del Cliente
Verifica que no falte nombre, teléfono, fecha u hora.
📸 Inserta captura del nodo IF (Datos completos?)
Explicación:
Si falta algún dato, el sistema detecta que debe pedirlo.
 
Consulta a Airtable
Obtiene información del paquete solicitado.
📸 Inserta captura del nodo List Records
Explicación:
El sistema busca la descripción del paquete desde la base de datos.
 
Prevención de Citas Duplicadas
Revisa si ya hay otra cita en la misma fecha y hora.
📸 Inserta captura del nodo IF (Cita duplicada?)
Explicación:
Si existe una cita duplicada, el flujo responde que esa hora no está disponible.
 
Registro de la Cita en Airtable
Se crea o actualiza el registro del cliente.
📸 Inserta captura del nodo Upsert Record
Explicación:
Se guardan los datos del cliente, fecha, hora y servicio solicitado.
 
Respuesta Final al Cliente
El bot confirma la reserva.
📸 Inserta captura del nodo final de mensaje
Explicación:
Se envía mensaje automático según la acción realizada.
 Respuesta Final WhatsApp 
Respuesta Final Citas Registro en AirTable 


