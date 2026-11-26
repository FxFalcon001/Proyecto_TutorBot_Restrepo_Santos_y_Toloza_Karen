# Proyecto_TutorBot_Restrepo_Santos_y_Toloza_Karen
TutorBot es una solución automatizada desarrollada en n8n que conecta a estudiantes con tutores mediante un motor de asignación inteligente.



TutorBot — Sistema Automatizado de Gestión de Tutorías (n8n + Telegram + Google Sheets)

Solución de automatización desarrollada en n8n conectada a Telegram (interfaz de usuario) y Google Sheets (TutorBot_DB) para gestionar de forma autónoma la consulta y cancelación de tutorías académicas.

Arquitectura del Sistema

Interfaz de usuario: Bot de Telegram que recibe comandos y mensajes de los estudiantes y envía respuestas de confirmación o aviso.

Lógica y automatización: Flujos de trabajo construidos en n8n con nodos de control condicional (If), procesamiento de datos en JavaScript (Code) y mensajería.

Base de datos: Libro de Google Sheets (TutorBot_DB) con las hojas TUTORES, DISPONIBILIDAD, TUTORIAS y SESSIONS.

Flujos Implementados y Validados

1. TutorBot - Consultar

Permite a los estudiantes consultar sus tutorías registradas directamente desde Telegram:

Telegram Trigger: escucha los mensajes entrantes del usuario.

If: filtra y valida si el mensaje corresponde al comando de consulta.

Get row(s) in sheet: consulta los registros de tutorías en Google Sheets.

Code in JavaScript: procesa y formatea la información de las tutorías encontradas para construir una respuesta clara.

Send a text message: envía el resultado de la consulta al chat del usuario en Telegram.

2. TutorBot - Cancelar

Permite validar y procesar la cancelación de una tutoría activa desde Telegram:

Telegram Trigger: recibe el mensaje y el código/identificador de la tutoría a cancelar.

If: verifica que el mensaje corresponda a la acción de cancelar.

Code in JavaScript: extrae y normaliza los datos del comando (chat_id, código de tutoría, etc.).

Get row(s) in sheet: obtiene las filas correspondientes desde Google Sheets.

Code in JavaScript1 validar: verifica si existe una tutoría activa asociada al usuario y al código indicado, calcula la información relevante (dia_semana, fecha, hora, materia, etc.) y define la acción a ejecutar (cancelar o mensaje).

3. If1 cancelar: evalúa si la cancelación procede:

Rama true: actualiza el estado de la fila en Google Sheets (Update row in sheet) y notifica al usuario por Telegram (Send a text message1).

Rama false: envía un mensaje informativo por Telegram (Send a text message) indicando que no se encontró una tutoría activa válida o que no aplica la cancelación.

Depuración y Mejoras Realizadas

Corrección de referencias de nodos (Referenced node doesn't exist): se ajustaron las expresiones dentro de los nodos de código para apuntar a los nombres reales de los nodos en el lienzo (por ejemplo, Code in JavaScript), evitando fallos por nombres desactualizados o inexistentes.

Validación de bifurcaciones (If): se verificó el enrutamiento de las ramas true y false para que el flujo responda adecuadamente tanto en casos exitosos como cuando no hay coincidencias.

Pruebas de ejecución: se probaron ambos flujos en n8n verificando el paso de ítems entre nodos, la lectura/actualización en Google Sheets y el envío de mensajes por Telegram.

Estructura del Repositorio

├── README.md
├── workflows/
│   ├── TutorBot_Consultar.json
│   └── TutorBot_Cancelar.json
└── docs/
    └── capturas/
