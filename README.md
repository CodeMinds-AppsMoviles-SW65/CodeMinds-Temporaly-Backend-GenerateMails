# Temporaly - TempMailAPI

## Descripción

Temporaly es una API para generar y recuperar información relacionada con correos electrónicos temporales. Esta API permite crear direcciones de correo electrónico desechables, acceder a mensajes en la bandeja de entrada y descargar archivos adjuntos.

## Tabla de Contenidos

- [Requisitos](#requisitos)
- [Instalación](#instalación)
- [Uso](#uso)
  - [Endpoints](#endpoints)
    - [Crear Correo Electrónico](#crear-correo-electrónico)
    - [Obtener Mensajes de la Bandeja de Entrada](#obtener-mensajes-de-la-bandeja-de-entrada)
    - [Leer Mensaje Específico](#leer-mensaje-específico)
    - [Descargar Adjuntos](#descargar-adjuntos)
- [Ejemplo de Uso](#ejemplo-de-uso)
- [Documentación Swagger](#documentación-swagger)
- [Contribuciones](#contribuciones)
- [Licencia](#licencia)

## Requisitos

- Python 3.12 o superior
- Flask
- Flasgger
- tempmail

## Instalación

1. Clona el repositorio:
   ```bash
   git clone <url-del-repositorio>
   cd <nombre-del-repositorio>
   ```
2. Crea un entorno virtual (opcional pero recomendado):
   ```bash
   python3.12 -m venv venv
   source venv/bin/activate  # En Windows usa `venv\Scripts\activate`
   ```

## Uso

Inicia la aplicación Flask:
   ```bash
   python app.py
   ```
La aplicación se ejecutará en http://127.0.0.1:5000.

## Endpoints

Crear Correo Electrónico
* URL: /api/v1/create_email
* Método: POST
* Descripción: Crea una dirección de correo electrónico temporal.
* Respuesta:
  * Código 200: Devuelve una dirección de correo electrónico temporal.
  ```json
  {
    "address": "test@example.com"
  }
  ```
  * Código 500: Error interno del servidor

Obtener mensajes de la Bandeja de Entrada
* URL: /api/v1/inbox
* Método: GET
* Descripción: Obtiene los mensajes de la bandeja de entrada del correo electrónico temporal.
* Respuesta:
  * Código 200: Devuelve una lista de mensajes.
  ```json
  [
    {
        "id": 1,
        "from_addr": "sender@example.com",
        "subject": "Hello",
        "date_str": "2024-09-26 12:34:56"
    }
  ]

  ```
  * Código 500: Error interno del servidor

Leer Mensaje Específico
* URL: /api/v1/messages/<int:message_id>
* Método: GET
* Descripción: Lee un mensaje específico por ID.
* Parámetros:
  * message_id: ID del mensaje a leer.
* Respuesta:
  * Código 200: Devuelve el contenido del mensaje.
  ```json
  {
    "id": 1,
    "from_addr": "sender@example.com",
    "subject": "Hello",
    "body": "This is the message body.",
    "date_str": "2024-09-26 12:34:56"
  }

  ```
  * Código 404: Mensaje no encontrado.
  * Código 500: Error interno del servidor.

Descargar Adjuntos
* URL: /api/v1/messages/<int:message_id>/attachments/<string:filename>
* Método: GET
* Descripción: Descarga un archivo adjunto de un mensaje.
* Parámetros:
  * message_id: ID del mensaje.
  * filename: Nombre del archivo adjunto a descargar.
* Respuesta:
  * Código 200: Devuelve el contenido del archivo adjunto.
  * Código 404: Adjunto no encontrado.
  * Código 500: Error interno del servidor.

Documentación Swagger
La documentación de la API está disponible en el siguiente enlace:

```bash
http://127.0.0.1:5000/apidocs/
```

Licencia
Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más detalles.
