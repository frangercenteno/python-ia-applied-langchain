# LangChain Memory

## Que es la memoria de contexto?

Es donde y como guardamos el historial de mensajes entre llamadas a la API.
El LLM no tiene estado. No recuerda nada entre llamadas.

### Entonces quien hace ese trabajo?

Nosotros, somos quienes debemos persistir ese historial y envarlo en cada nueva llamada

## Tipos de memoria

Vamos a definir 4 tipos de memoria:

- RAM
- DISCO
- Base de datos
- Base de datos en momoria

### In-memory (RAM)

**Se Almacenan**: Variables Python
**Ventajas**: Instantanea, sin configuraciones
**Desventajas**: Se pierde al cerrar o terminar el programa
**Usos**: Prototipado, test

### SQLITE

**Se Almacenan**: Archivo .db en el disco local
**Ventajas**: Persiste, no necesita valor
**Desventajas**: Un proceso a la vez y no es distribuida
**Usos**: Apps locales, proyectos personales, desarrollo

### POSTGRESQL

**Se Almacenan**: Servidor de base de datos
**Ventajas**: Multiples usuarios, escalable, usada para produccion
**Desventajas**: Requiere configuracion del servidor y conocimientos en bases de datos
**Usos**: Produccion, APIs con multiples usuarios, multiples consultas

### REDIS

**Se Almacenan**: Servidor en momoria con persistencia
**Ventajas**: Muy rapida para sesiones activas
**Desventajas**: Requiere servidor Redis
**Usos**: Sesiones de alta frecuencia, cache

## Conceptos

### session_id

Es el identificador unico de cada conversacion. Permite que el mismo sistema sirva multiples usuarios con historiales separados

### MessagesPlaceholder

Es el component de LangChain que le dice al prompt: "En este punto, isnerta automaticamente todos los mensajes anteriores de sesion".
LangChain los carga desde la base de datos antes de cada llamada LLM.

### RunnableWithMessageHistory

Es el wrapper que conecta una cadena con un backend de memoria. Hace tres cosas automaticamente.

1. Antes de invocar: Carga el historial de la Base de datos usando `session_id`
2. Inyecta ese historial en el MessagesPlaceholder del prompt
3. Despues de invocar: guarda el nuevo mensaje en la DB

