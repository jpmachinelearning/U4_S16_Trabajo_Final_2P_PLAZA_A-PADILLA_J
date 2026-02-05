# Análisis de Opinión en Repositorios Git

## 🏫 Información Académica
**Universidad:** Universidad de Guayaquil
**Facultad:** Facultad de Ciencias Matemáticas y Físicas
**Carrera:** Ciencia de Datos & IA
**Asignatura:** Procesamiento de Lenguaje Natural
**Proyecto:** Trabajo Parcial II - Observatorio de Opinión y Salud del Proyecto

### 👥 Integrantes:
| Nombre y Apellido | Rol / Contribución |
| :--- | :--- |
| **JUAN PADILLA M.** | RF–01 Recolección de datos, RF–02 Preprocesamiento, RF–03 Representación (TF-IDF), RF–04 Sentimiento, RF–05 Temas |
| **ALEXANDER PLAZA J.** | RF–06 Similitud textual, Documentación, Análisis de Hallazgos |

---

## 📖 1. Contexto del Proyecto
En el desarrollo de software colaborativo, plataformas como GitHub y GitLab almacenan una gran cantidad de información textual en forma de issues, pull requests (PR) y comentarios. Estos textos reflejan problemas técnicos, decisiones de diseño, nivel de satisfacción del equipo y momentos críticos del proyecto.

El presente proyecto propone aplicar técnicas clásicas de **Procesamiento de Lenguaje Natural (PLN)** para analizar, clasificar y comparar dichos mensajes, con el fin de evaluar la opinión expresada y la salud general del proyecto. El enfoque es exclusivamente analítico, prescindiendo del uso de modelos de Deep Learning, Transformers o agentes conversacionales.

## 🎯 2. Objetivos
### Objetivo General
Aplicar técnicas clásicas de PLN para analizar el sentimiento, los temas recurrentes y la similitud textual en mensajes de un repositorio Git, con el fin de generar un observatorio de opinión y salud del proyecto.

### Objetivos Específicos
1. **Recolección**: Obtener mensajes reales (issues, PRs y comentarios) mediante APIs o archivos CSV.
2. **Preprocesado**: Aplicar técnicas de limpieza y normalización clásicas.
3. **Representación**: Vectorizar los textos utilizando el modelo **TF–IDF**.
4. **Sentimiento**: Clasificar mensajes en positivo, neutral o negativo mediante modelos supervisados.
5. **Categorización**: Identificar temas mediante agrupamiento (K-Means) o reglas de palabras clave.
6. **Similitud**: Implementar similitud coseno para encontrar mensajes similares.

## 📂 3. Estructura del Repositorio
data/: Contiene el dataset datos_github_proyecto_final.csv con los datos recolectados.
src/: Código fuente del proyecto.
    * eda_limpieza.py: Filtrado de ruido, bots e idioma.
    * preprocesado.py: Pipeline de normalización y tokenización.
README.md: Documentación completa del proyecto.

## ⚙️ 4. Pipeline de Procesamiento (Flujo de Trabajo)

El sistema sigue un flujo estrictamente secuencial para garantizar la calidad de los datos antes del análisis:

### Fase I: EDA y Filtrado Crítico (eda)
Antes del preprocesado de PLN, los datos pasan por un filtrado de "calidad humana":
1. **Limpieza de Nulos**: Se eliminan registros sin contenido en el campo comentario.
2. **Filtro de Bots**: Se identifican y saltan mensajes generados automáticamente (ej. ocabot, logs de servidores, comandos de merge).
3. **Detección de Idioma y Código**: Se aplica una heurística de **frecuencia de Stopwords**. Si el texto no contiene palabras funcionales del español (el, de, que, etc.) o tiene mayor proporción de palabras en inglés, se descarta para evitar analizar código de programación o mensajes en otros idiomas.

### Fase II: Preprocesado de Texto (preprocesado)
Cada registro se trata como un "documento" dentro de una "colección". El proceso incluye:
**Normalización**: Conversión total a minúsculas.
**Tokenización**: División por palabras usando nltk.word_tokenize.
**POS Tagging**: Etiquetado gramatical para identificar y remover signos de puntuación complejos.
**Limpieza de Caracteres**: Eliminación manual de corchetes, guiones repetidos y símbolos especiales.
**Remoción de Stopwords**: Eliminación de palabras vacías del español.
**Filtro Alfanumérico**: Se conservan solo tokens que contienen caracteres alfanuméricos, eliminando basura técnica residual.

### Fase III: Representación y Análisis (RF-03 a RF-06)
**Vectorización**: Uso de **TF-IDF** para transformar la colección de documentos en matrices numéricas.
**Sentimiento**: Clasificación mediante modelos clásicos como Logistic Regression o Linear SVM.
**Similitud**: Implementación de **Similitud Coseno** para comparar documentos entre sí.

## 🛠️ 5. Requerimientos Funcionales (Alcance)
**RF–01 Recolección**: Conexión a API y almacenamiento en CSV.
**RF–02 Preprocesado**: Limpieza, normalización, remoción de puntuación y stopwords.
**RF–03 Representación**: Uso de modelo TF-IDF (unigramas/bigramas).
**RF–04 Sentimiento**: Clasificación supervisada clásica.
**RF–05 Identificación de Temas**: Clustering (K-Means) o reglas basadas en palabras clave.
**RF–06 Similitud Textual**: Cálculo de similitud coseno entre mensajes.
