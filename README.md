Pre-entrega – Workflow de control de encaje diario


Nombre del caso
Control automático de movimiento de efectivo y alerta de encaje.
Descripción general
Este workflow automatiza el control diario de efectivo registrado en una planilla de Google Sheets.
Cuando se agrega una nueva fila con los saldos del día, el sistema calcula el movimiento de efectivo respecto al día anterior y evalúa si el saldo supera el encaje definido. En caso de detectarse una situación que requiera revisión, el sistema envía una notificación por email.
Trigger del workflow
El workflow se dispara automáticamente mediante Google Sheets Trigger – “On Row Added”.
Cada vez que se agrega una nueva fila en la planilla, n8n detecta el cambio y ejecuta el flujo de automatización.

Descripción de los nodos
1. Google Sheets Trigger
Detecta cuando se agrega una nueva fila en la hoja de cálculo que contiene los saldos diarios.
2. HTTP Request (Time API)
Consulta una API pública de tiempo para obtener la fecha actual de Argentina. Esto demuestra la integración del workflow con un servicio externo.
3. Edit Fields / Set (Cálculo de movimiento)
Se procesan los datos recibidos desde Google Sheets y se calcula el campo movimiento, que representa la diferencia entre el saldo del día actual y el saldo del día anterior.

4. IF (Condición de encaje)
Evalúa si el saldo supera el límite definido de encaje.
Si el saldo es mayor al encaje permitido, se considera que puede ser necesario retirar efectivo.
5. Email
En caso de cumplirse la condición del IF, el workflow envía un correo electrónico notificando que se debe verificar la necesidad de solicitar un retiro de efectivo.
6. Update Row (Google Sheets)
Se actualiza la fila correspondiente en la planilla para registrar los resultados del proceso, incluyendo el movimiento calculado y el estado de procesamiento.

Condición evaluada
El nodo IF verifica si el saldo del día supera el encaje definido.
Si esto ocurre, el sistema genera una alerta para revisar la necesidad de gestionar un retiro de efectivo.
Configuración de la notificación
La notificación se implementa mediante el nodo Email, que envía un correo automático cuando se detecta una situación que requiere revisión. El mensaje informa que el saldo supera el encaje establecido.

Buenas prácticas aplicadas
•	Uso de trigger automático para evitar ejecuciones manuales.
•	Integración con API externa para demostrar consumo de servicios externos.
•	Control de ejecución mediante campo de procesamiento para evitar loops en el workflow.
•	Separación de lógica y datos mediante nodos de transformación (Edit Fields).
•	Uso del gestor de credenciales de n8n para manejar de forma segura las credenciales del email sin exponerlas en el código del workflow.


