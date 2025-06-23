Resumen de Pipeline: Reviews de Pueblos Mágicos a Predicciones

Proyecto inspirado en el paper "REST-MEX: Sentiment Analysis of Mexican Restaurants"
https://ceur-ws.org/Vol-3496/restmex-paper14.pdf

1. Descripción de alto nivel
Este pipeline implementa un flujo de análisis de sentimiento para reseñas de Pueblos Mágicos. Comienza cargando y preprocesando los datos de reseñas, aplica balanceo de clases mediante back-translation, adapta un modelo de lenguaje al dominio, afina el modelo con validación cruzada y finalmente genera predicciones guardadas en un archivo .txt.

2. División de datos y balanceo de clases
Durante el desarrollo de mi proyecto, utilicé una división de datos en una proporción del 80% para entrenamiento y el 20% restante para evaluación. Observé que los datos de entrenamiento estaban desbalanceados en la distribución de clases, por lo que apliqué balanceo de clases mediante back-translation (MarianMT) para garantizar una representación equitativa de cada etiqueta.

3. Pasos principales
1. Instalación de dependencias: pandas, datasets, transformers, torch, evaluate.
2. Carga de datos: lectura de archivos Excel de entrenamiento y prueba.
3. Preprocesamiento: limpieza de texto y normalización.
4. Balanceo de datos: back-translation usando MarianMT.
5. Adaptación al dominio: masked language modeling (MLM) con PlanTL-GOB-ES/roberta-base-bne.
6. Fine-tuning con validación cruzada: entrenamiento de clasificación en 5 folds.
7. Entrenamiento final y predicciones: entrenamiento con todo el conjunto balanceado y guarda de resultados.

4. Modelos y parámetros

4.1 Back-Translation (MarianMT)
| Parámetro                       | Valor                                                         |
|---------------------------------|---------------------------------------------------------------|
| Modelos                         | Helsinki-NLP/opus-mt-es-en → Helsinki-NLP/opus-mt-en-es      |
| batch_size                      | 128                                                           |
| max_length (es→en y en→es)      | 128                                                           |

4.2 Adaptación al Dominio (Masked LM)
| Parámetro            | Valor                             |
|----------------------|-----------------------------------|
| base_model           | PlanTL-GOB-ES/roberta-base-bne    |
| checkpoint_dir       | domain_adapted_model              |
| epochs               | 3                                 |
| batch_size           | 32                                |
| learning_rate        | 2e-5                              |
| weight_decay         | 0.01                              |
| logging_steps        | 100                               |
| save_steps           | 500                               |

4.3 Fine-tuning con Validación Cruzada
| Parámetro       | Valor                |
|-----------------|----------------------|
| base_model      | domain_adapted_model |
| num_labels      | 5                    |
| epochs          | 4                    |
| batch_size      | 8                    |
| learning_rate   | 2e-5                 |
| weight_decay    | 0.01                 |
| logging_steps   | 200                  |
| save_strategy   | no                   |

4.4 Entrenamiento Final y Predicción
| Parámetro     | Valor            |
|---------------|------------------|
| output_dir    | final_train      |
| epochs        | 3                |
| batch_size    | 8                |
| save_strategy | no               |

5. Resultados finales
Las predicciones del modelo se guardan en un archivo de texto llamado `Moodhacker_con_4_neuronas.txt`, donde cada línea contiene el identificador de la instancia y la clase asignada.
