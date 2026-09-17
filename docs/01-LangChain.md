# LangChain

## Que es el LangChain

Es un framework opensource creado en 2022 por Harrison Chase. Su proposito es simplificar la construccion de aplicaciones que usan modelos lenguaje (Ej. GPT)

### Sin LangChain

Cada desarrollador manejaba el historial de mensajes, conecta con las bases de datos vectoriales, implementar tools, gestopmar errpres de la API y todo lo relacionado desde CERO.

### Con LangChain

Se tiene estandarizado esos patrones que haciamos desde cero y se empquetaron en components reutilizables.

LangChain es la libreria mas usada en el ecosistema de AI Aplicada

### Par que sirve

Ayuda a construir aplicaciones que combinan modelos de lenguaje con otras herramientas y datos. Ejemplo:

- Chatbots avanzados
- Asistentes de consulta
- Sitema de proguntas y respuestas sobre documentos
- Automatizacion de tareas con IA

### Como funciona?

LangChain organiza el uso de modelos de lenguaje en componentes reutilizables:

- Models: como OpenAI o Anthropic
- Prompts: Instrucciones que les da al modelo
- Chains: Secuencias de pasos (Ej. Preguntas->procesar->responder)
- Agents: Sistema que deciden que hacer segun la situacion
- Memory: permite recordar informacion en una conversacion

### Que es LCEL?

Son las siglas de LangChain Expression Language. Es la sintaxis de LangChain que usa el operador pipe "|" para encadenar componentes
de forma declarativa

Pipes en Unix

``
cat file.txt | grep "error" | sort
``

Pipes en LCEL

``
prompt | llm | parser
``

### Que es Runnable?

Todos los componentes de LangChain implementan la interfaz Runnable.
Significa que tienen los mismos metodos:
`.invoke()`, `.batch()`, `stream()`

Esto es lo que hace posible encadenarlos con un piple "|"

ChatPromptTemplate -> Runnable (dict -> messages)
ChatOpenAI -> Runnable (messages -> AIMessage)
StrOutputParser -> Runnable (AIMessage -> string)

Encadenadors: dict -> [prompt] -> message -> [llm] -> AIMessage -> [parser] -> string

## Layered Architecture

La arquitectura del proyecto esta organizada en capas dentro de `src/langchain_section/`:

```text
src/
langchain_section/
|-- config/     # Capa de configuracion
|-- core/       # Capa nucleo
|-- memory/     # Capa de memoria
|-- chains/     # Capa de cadenas
|-- graphs/     # Capa de grafos
`-- demos/      # Capa de demos
```

### Capas

- **config**: configura los valores y dependencias compartidas de la aplicacion.
- **core**: contiene los componentes fundamentales, como modelos, embeddings y carga de documentos.
- **memory**: implementa la persistencia y el historial de las conversaciones.
- **chains**: define cadenas reutilizables para componer prompts, modelos y parsers.
- **graphs**: organiza flujos con estados y nodos para procesos mas complejos.
- **demos**: contiene ejemplos ejecutables que muestran como usar los componentes.

Cada capa tiene una responsabilidad concreta y puede reutilizar las capas inferiores. Esto mantiene separada la configuracion, la logica central y los flujos de aplicacion.
> Regla: los demos consumen las capas de aplicacion y las capas de aplicacion reutilizan los componentes del nucleo.
---

