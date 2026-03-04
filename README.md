# ProyectoTerminal-NPC-con-Modelo-LLM
Sistema de recorrido virtual con integración de Inteligencia Artificial para Universidad Autonoma Metropolitana
#Descripcion
Este proyecto implementa un sistema de **NPCs (Non-Player Characters)** inteligentes dentro de un recorrido virtual. A diferencia de los diálogos preprogramados, estos agentes utilizan un **LLM (Large Language Model)** para interactuar con los usuarios (estudiantes/profesores) de forma contextual.
El sistema permite realizar preguntas técnicas específicas. Por ejemplo, si un usuario tiene dudas sobre "proceso o sistema operativo" en una asignatura de sistemas operativos, el NPC asignado a ese tema responderá utilizando información precisa extraída de documentos académicos previamente procesados.

rquitectura Técnica
* **Modelo de Lenguaje:** LLM alojado localmente mediante contenedores (**Docker**), garantizando privacidad y soberanía de los datos.
* **Arquitectura RAG (Retrieval-Augmented Generation):** El sistema conecta el modelo con una base de datos de conocimientos.
* **Ingesta de Datos:** Los documentos se procesaron en **chunks** (fragmentos) y se almacenaron en un motor de búsqueda vectorial.
* **Comunicación:** El modelo se conecta a través de una **API** que solicita los fragmentos más relevantes a la consulta del usuario para generar una respuesta clara, concisa y con contexto real.

* Csos de purbea y resultados
Para validar la precisión del sistema **RAG**, se realizaron pruebas con diferentes perfiles de conocimiento (NPCs):

  > <img width="1664" height="815" alt="Coleccion-sistemaOperativo" src="https://github.com/user-attachments/assets/9951fb76-fc60-4e2a-bded-895dc48e23b1" />

* Se realizaron varias pruebas, para diferentes tipos de NPC con enfoques academicos disntintos
  > <img width="1660" height="987" alt="Coleccion-geometria" src="https://github.com/user-attachments/assets/3b0858e2-ae74-442c-a28d-50bb768039bc" />
* Se configuró un **System Prompt** estricto para que el modelo no genere información falsa (alucinaciones). Si el tema no está en la base de datos de **Qdrant**, el NPC delega la respuesta de forma honesta.

  ><img width="1659" height="909" alt="Coleccion-geometria-negativa" src="https://github.com/user-attachments/assets/458e803c-8e68-4f81-aea2-c5c3c2dde921" />
  ><img width="1652" height="795" alt="Coleccion-sistemaOperativonegativa" src="https://github.com/user-attachments/assets/877d5df5-ca73-48ce-a2f6-3b09339185ed" />

## Stack Tecnológico
* **Motor de Videojuegos:** Unity (C#) para el entorno 3D.
* **LLM:** `Gemma-2B` (Google) cuantizado para ejecución local.
* **Base de Datos Vectorial:** `Qdrant` para la gestión de embeddings y RAG.
* **API / Backend:** `FastAPI` (Python).
* **Infraestructura:** `Docker` para la contenedorización de servicios.

## Funcionamiento del Sistema
1. **Consulta:** El usuario escribe una pregunta en Unity.
2. **Búsqueda Vectorial:** FastAPI recibe la consulta, genera un embedding y busca en **Qdrant** los fragmentos (*chunks*) de texto más similares.
3. **Inferencia:** Se envía el contexto recuperado + la pregunta al modelo **Gemma-2B**.
4. **Respuesta:** El NPC muestra la respuesta generada basada exclusivamente en los documentos académicos.

## Logros del Proyecto
* **Privacidad Total:** Al correr el LLM localmente en Docker, los datos de la universidad nunca salen del servidor.
* **Cero Alucinaciones:** Gracias al *System Prompt* y la arquitectura RAG, los NPCs admiten cuando no conocen un tema en lugar de inventar información.
* **Escalabilidad:** El script de ingesta permite añadir nuevas materias o facultades simplemente soltando archivos en una carpeta.

*Nota: El código fuente de este proyecto es de carácter privado por políticas institucionales, pero se adjunta esta documentación como evidencia de la implementación técnica.*
