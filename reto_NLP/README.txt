Durante el desarrollo de nuestro proyecto, use diferentes modelos de procesamiento de lenguaje natural basados en transformers, una tecnología de vanguardia en el campo de NLP. 

Durante el desarrollo de mi proyecto, utilicé una división de datos en una proporción del 80% para entrenamiento y el 20% restante para evaluación. Sin embargo, antes de realizar esta división, me aseguré de abordar el balanceo de clases en mis datos.

Observé que mis datos de entrenamiento no estaban equilibrados en términos de la distribución de clases. Algunas clases tenían más ejemplos que otras, lo que podría sesgar el modelo hacia las clases dominantes.

Para abordar esta situación, apliqué una técnica de balanceo de clases llamada "muestreo estratificado". Esta técnica garantiza que la proporción de ejemplos de cada clase se mantenga tanto en el conjunto de entrenamiento como en el conjunto de evaluación. De esta manera, el modelo se entrena y evalúa de manera equitativa en todas las clases, lo que mejora la generalización y evita sesgos hacia las clases más numerosas.

Utilicé diversos modelos basados en transformers para abordar el desafío de análisis de sentimientos en textos. En particular, aproveché la biblioteca Transformers de Hugging Face.

Para comenzar, utilicé el modelo `AutoModelForSequenceClassification` de la biblioteca Transformers. Este modelo es compatible con tareas de clasificación de secuencias y puede adaptarse para el análisis de sentimientos. 

En mi implementación, configuré el número de etiquetas de salida (`num_labels`) en 5, ya que deseaba clasificar los textos en cinco categorías emocionales diferentes. 

Posteriormente, realicé un proceso de afinamiento del modelo pre-entrenado. Esto implica tomar un modelo pre-entrenado en un corpus grande y ajustarlo a nuestro conjunto de datos específico para mejorar su rendimiento en la tarea de análisis de sentimientos.

También configuré el tamaño de lote (batch size), el número de épocas de entrenamiento y la tasa de aprendizaje para optimizar el rendimiento del modelo. 

Además, implementé métricas de evaluación, como precisión, recuperación y puntuación F1, para evaluar el desempeño del modelo en el conjunto de datos de prueba. Estas métricas me permitieron medir la capacidad del modelo para clasificar correctamente los textos según las emociones correspondientes.

Finalmente, para generar los resultados requeridos para el reto, guardé las predicciones del modelo en un archivo de texto. Cada línea del archivo contiene el identificador de la instancia y la clase de emoción asignada, separados por una tabulación (`\t`), tal como se solicitó en el formato especificado.


