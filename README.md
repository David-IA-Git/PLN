# PLN
Fine-tuning y comparativa de modelos Transformer (BERT, RoBERTa, DistilBERT).

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1-FXh6mlc-GdXplpKtIoXZFwmxEMXw87J?usp=sharing)
> **Nota:** Haz clic en el botón de arriba para abrir el notebook directamente en Google Colab.
> 
> **Advertencia**: El renderizado de este notebook en GitHub puede mostrar un error ("Invalid Notebook") debido a metadatos de widgets; por favor, utiliza el botón "Open in Colab" para la visualización correcta del notebook.

---

## Introducción y Objetivo

Este proyecto de **Procesamiento de Lenguaje Natural (PLN)** se centra en la aplicación de la técnica de **Fine-Tuning** a tres arquitecturas de modelos Transformer: **BERT**, **RoBERTa**, y **DistilBERT**.

El objetivo principal es realizar una **comparativa de rendimiento y eficiencia** entre estos modelos en la tarea de **Clasificación de Sentimientos** (Sentiment Analysis) multiclase (5 estrellas) utilizando un subconjunto del dataset **Yelp Review Full**.

## Metodología

### 1. Dataset y Preprocesamiento
* **Dataset:** `yelp_review_full` (Reseñas con 5 clases de sentimiento, de 1 a 5 estrellas).
* **Muestra:** Se utiliza una porción del dataset (20k ejemplos para entrenamiento, 2k para validación) para asegurar la comparabilidad de los resultados.
* **Tokenización:** Cada modelo se tokeniza con su **tokenizador específico** (`bert-base-cased`, `roberta-base`, `distilbert-base-cased`) para preservar las propiedades de su preentrenamiento.

### 2. Fine-Tuning
* **Framework:** **Hugging Face Transformers** y la clase `Trainer`.
* **Tarea:** `Sequence Classification` (Clasificación de Secuencias).
* **Head:** El "head" pre-entrenado de cada modelo se reemplaza por uno de **Clasificación con 5 salidas** (`num_labels=5`).
* **Hiperparámetros:** El entrenamiento se realiza durante **5 épocas**, optimizando en base a la métrica **Accuracy**.

---

## Análisis de Resultados (Precisión vs. Eficiencia)

La comparativa evalúa el impacto de las **mejoras arquitectónicas** (BERT vs. RoBERTa) y la **destilación del conocimiento** (BERT vs. DistilBERT) en la tarea de clasificación.

| Modelo | Arquitectura | Precisión (Accuracy) | Tiempo por Época (Minutos) | Razón de Eficiencia (vs BERT) |
| :--- | :--- | :--- | :--- | :--- |
| **RoBERTa** | Optimización de BERT | **0.669** | ~32.7 min | Mayor Precisión |
| **BERT** | Línea Base (Transformer) | 0.638 | ~31.9 min | Referencia |
| **DistilBERT** | Destilación de BERT | 0.610 | **~16.4 min** | 2x más rápido |

### Conclusiones Clave

* **Rendimiento Superior:** **RoBERTa** obtuvo la mayor precisión (0.669). Esto se atribuye a su estrategia de preentrenamiento mejorada (mayor corpus de texto y lotes más grandes) en comparación con BERT.
* **Compensación de Eficiencia:** **DistilBERT** es el modelo más rápido, reduciendo el tiempo de entrenamiento y validación **a casi la mitad** en comparación con BERT. Esta mayor eficiencia tiene un coste aceptable de rendimiento (solo una ligera bajada del Accuracy).
* **Implicación Práctica:** La elección del modelo debe alinearse con las prioridades del proyecto: usar **RoBERTa** para la máxima **precisión** a costa de más tiempo de cálculo, o **DistilBERT** para una alta **eficiencia** en entornos de recursos limitados.
