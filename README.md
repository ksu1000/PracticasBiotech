# PracticasBiotech
## 1.	Introducción
Estas prácticas se llevaron a cabo en la empresa Biotech Digital Solutions, S.L., una Empresa de Base Tecnológica (EBT) especializada en la implantación de sistemas digitales basados en tecnologías 3D, orientadas al sector protésico-dental, clínico y hospitalario. El objetivo principal de mis prácticas fue aplicar y expandir los conocimientos adquiridos durante el máster en un entorno profesional real.
Durante el periodo de prácticas, me integré en el Departamento de I+D+i (Investigación, Desarrollo e Innovación) de Biotech Digital Solutions, S.L. Las actividades que realicé se centraron en desarrollar un sistema automatizado para la segmentación de mandíbulas utilizando imágenes médicas. Este sistema podría ser útil al mejorar el diagnóstico y tratamiento, facilitar la planificación quirúrgica, optimizar el desarrollo de prótesis y ortodoncia, y reducir tiempo y costos, haciendo los servicios de salud más accesibles y eficientes.
Trabajé utilizando los lenguajes Python, Keras y TensorFlow para tareas de preprocesamiento de imágenes, deep learning y segmentación de imágenes. Investigué y apliqué arquitecturas de redes neuronales como CNN, redes preentrenadas y arquitecturas U-net para realizar predicciones. Evalué los resultados utilizando métricas específicas aplicadas a tareas de segmentación de imágenes.
Estas actividades estaban directamente relacionadas con los contenidos y asignaturas cursadas en el máster, particularmente con Minería de Datos (05MBID) y Redes Neuronales y Deep Learning (12MBID). No obstante, requirieron no solo aplicar lo aprendido, sino también investigar por mi cuenta y ampliar mis conocimientos en estos campos. Por ejemplo, durante la asignatura de Redes Neuronales y Deep Learning, trabajamos principalmente en la clasificación de imágenes, que consiste en asignar una etiqueta a una imagen completa según su contenido. Sin embargo, en este proyecto necesitaba aprender técnicas más avanzadas como la segmentación de imágenes, que consiste en asignar una etiqueta a cada píxel de la imagen. En la asignatura de Minería de Datos usábamos métricas como precisión para clasificación, pero en esta tarea necesité aprender y aplicar métricas específicas para la evaluación de segmentación de imágenes, como el coeficiente de Dice.
En resumen, estas prácticas fueron una oportunidad invaluable para aplicar los conocimientos teóricos adquiridos en el máster en un entorno profesional altamente especializado. Además de contribuir al avance de la empresa en el desarrollo de soluciones tecnológicas innovadoras, este período de prácticas me permitió crecer profesionalmente al enfrentarme a desafíos reales y aprender nuevas técnicas y metodologías.

Tabla 1. Descripción de experimentos con arquitecturas. Elaboración propia.
Núm	Arquitectura	Descripción y cambios comparando con la prueba anterior	Resultados	Código Disponible
1	Unet sin backbone	rquitectura básica sin backbone. Datos de entrada: 1620 imágenes 2D convertidas de nii.gz a png. Normalización al rango [0,1] y Data Augmentation aplicados.. 	Solo permite batch size muy bajo: 2, debido a las limitaciones de recursos computacionales	Anexo 1
2	Unet con ResNet	Utiliza ResNet50 pre-entrenado como base con conexiones skip. Datos de entrada preprocesados según requisitos de ResNet. Normalización al rango [0,1] y Data Augmentation aplicados.	Solo permite batch size muy bajo: 2	Anexo 1
3	Unet con EfficientNet	Utiliza EfficientNet pre-entrenado como base con conexiones skip. Datos de entrada preprocesados según requisitos de EfficientNet. Normalización al rango [0,1] y Data Augmentation aplicados.	Solo permite batch size muy bajo: 2	Anexo 1
4	SALT	Modelo pre-entrenado para segmentar 145 estructuras corporales. Datos de entrada: 1 imagen nii.gz para prueba. Transformación al formato channel first aplicada.	No funciona bien para la segmentación de mandíbula y dientes, porque no tiene clases tan específicas, sino huesos, órganos y tejidos. Los resultados de prueba visualmente están muy lejos del nivel óptimo.	Anexo 2
5	nnUnet	Datos de entrada: 46 imágenes médicas 3D .mha sin transformación, 42 clases de etiquetas originales (background, cada diente, mandíbula), 1000 épocas preestablecidas por el modelo	Se interrumpe ejecución por falta de RAM	Anexo 3
6	nnUnet	Datos de entrada: 5 imágenes médicas 3D .mha sin transformación, número de clases de etiquetas sin cambio. El problema de 1000 épocas se resuelve introduciendo una nueva clase de entrenador que hereda propiedades de la clase original sobrescribiendo el número de épocas. Se utiliza 1 época para debugging. Nueva clase: class nnUNetTrainer_1epoch(nnUNetTrainer).	1 época dura más de 1 hora y para algunos folds de cross-validation no se finaliza	-
7	nnUnet	Datos de entrada: 2 imágenes médicas 3D .mha. Se introduce transformación de imágenes de 3D a 2D utilizando código en Python dividiendo en slices: 274 slices en formato .nii.gz para cada imagen mha. En vez de 42 clases, se utilizan solo 4 juntando clases de menor interés, se utiliza técnica de Region-based training. Entrenamiento sigue con 1 época.	Se finalizó el entrenamiento con Dice, se realizó la predicción con la imagen de test	Código de transformación Anexo 4, Código de entrenamiento Anexo 5
8	nnUnet	Épocas aumentadas a 20 utilisando nueva clase: class nnUNetTrainer_20epoch(nnUNetTrainer), aumentado número de imágenes de entrada de 2 a 6 imágenes .mha, lo que equivale a 1620 imágenes 2D. Preprocesamiento según requesitos de nnUnet	Mejores resultados de todas las Arquitectura	Código de transformación Anexo 6, Codigo de entrenamiento Anexo 7

