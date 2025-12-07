# 🐍 LangChain: Fundamentos para la Construcción de Aplicaciones con LLM

Este repositorio contiene una serie de cuadernos Jupyter que exploran los **bloques de construcción fundamentales** para crear aplicaciones robustas y modulares con Large Language Models (**LLMs**) utilizando la librería **LangChain** y la API de **OpenAI**.

## 🎯 Objetivos del Proyecto

El objetivo principal es pasar de las llamadas directas a la API de OpenAI a un enfoque estructurado y modular, aprendiendo a gestionar el **contexto** (Memoria), el **flujo** (Cadenas) y la **estructura de datos** (Parsers).

---

## ⚙️ Estructura del Repositorio y Conceptos Clave

| Cuaderno | Conceptos Cubiertos | Enfoque Principal |
| :--- | :--- | :--- |
| `L1-Model_prompt_parser.ipynb` | Modelos, Prompts y Parsers de Salida | **Estructuración de la Entrada y Salida (I/O).** |
| `L2-Memory.ipynb` | Tipos de Memoria | **Persistencia del Contexto Conversacional.** |
| `L3-Chains.ipynb` | Tipos de Cadenas (*Chains*) | **Automatización de Flujos de Trabajo Inteligentes.** |

---

## 1. 📝 Módulo de I/O: Modelos, Prompts y Parsers (L1)

Este módulo cubre la preparación de la entrada para el LLM y la interpretación de su salida.

| Componente | Función Técnica | Propósito Sencillo |
| :--- | :--- | :--- |
| **Prompts** | Clase `ChatPromptTemplate`. Define plantillas con *placeholders* (`{variable}`) para crear instrucciones reutilizables. | Separar la **instrucción fija** (la tarea) de las **entradas variables** (el texto del usuario, el estilo). |
| **Output Parsers** | Clases `ResponseSchema` y `StructuredOutputParser`. Fuerza al LLM a generar una salida en formato **JSON** y la convierte en un objeto usable de Python (`dict`). | Tomar la respuesta del robot (que es texto) y convertirla en una **estructura de datos** fácil de manipular. |
| **Modelos (LLMs)** | Clase `ChatOpenAI`. Es la interfaz estándar de LangChain para interactuar con los modelos de chat. | El "control remoto" para enviar y recibir datos del robot inteligente. |

---

## 2. 🧠 Módulo de Memoria (L2)

Este módulo se enfoca en dotar a los *chatbots* de **contexto**, resolviendo el problema de que los LLMs son inherentemente "sin estado" (*stateless*).

| Tipo de Memoria | Función Principal | Control de Longitud |
| :--- | :--- | :--- |
| **`ConversationBufferMemory`** | Almacena el **historial completo**. | **Ninguno.** El historial crece indefinidamente. |
| **`ConversationTokenBufferMemory`** | Limita el historial según el **número total de *tokens*** consumidos. | **Estricto por Costo/Tamaño.** Recorta mensajes antiguos para ajustarse al límite. |
| **`ConversationSummaryBufferMemory`** | **Resume** las partes más antiguas de la conversación (usando el LLM) y mantiene explícitas las interacciones recientes. | **Inteligente.** Mantiene el contexto relevante y el resumen informativo. |

---

## 3. ⛓️ Módulo de Cadenas (*Chains*) (L3)

El módulo de Cadenas cubre la automatización de flujos de trabajo al permitir enlazar múltiples operaciones con LLMs. 

| Tipo de Cadena | Función Principal | Control de Flujo |
| :--- | :--- | :--- |
| **`LLMChain`** | La cadena más básica. Combina un LLM con una plantilla de prompt para una **tarea única**. | Directo. |
| **`SequentialChain`** | Permite **flujos de trabajo complejos** donde se combinan subcadenas con múltiples entradas y salidas. | Secuencial (Múltiples entradas/salidas). |
| **`RouterChain`** | Utiliza un **Agente LLM** para analizar la entrada y **decidir a qué subcadena especializada** debe enrutar la petición. | **Decisión Inteligente.** (Ej., enrutar preguntas de Física a la cadena de Física). |
