# Data Project 4: Clasificación de Imágenes de Rayos X - PAKOTINAIKOS

---

## Índice
1. [Introducción](#introducción)
2. [Motivación y Contexto](#motivación-y-contexto)
3. [Objetivos del Proyecto](#objetivos-del-proyecto)
4. [Conjunto de Datos](#conjunto-de-datos)
5. [Preprocesamiento y Limpieza](#preprocesamiento-y-limpieza)
6. [Aumento de Datos](#aumento-de-datos)
7. [Modelos Utilizados](#modelos-utilizados)
8. [Solución Seleccionada](#solución-seleccionada)
9. [Resultados](#resultados)
10. [Conclusiones y Próximos Pasos](#conclusiones-y-próximos-pasos)

---

## Introducción

El proyecto **PAKOTINAIKOS** se centra en la clasificación de imágenes de rayos X, con el objetivo de facilitar la correcta categorización de diferentes partes del cuerpo. Esto es esencial para optimizar el flujo de trabajo clínico, permitiendo un procesamiento y diagnóstico más eficientes.

---

## Motivación y Contexto

Existen dificultades en el uso de sistemas PACS para la clasificación precisa de imágenes de rayos X, lo cual puede afectar la eficiencia de los diagnósticos. Este proyecto busca mejorar dicha clasificación, subrayando la importancia de la identificación precisa de las diferentes partes del cuerpo en estas imágenes.

---

## Objetivos del Proyecto

1. **Precisión de Clasificación**: Asegurar una alta precisión en la categorización de imágenes.
   - *Métrica*: Accuracy
2. **Eficiencia Computacional**: Mejorar la velocidad de procesamiento para una mayor escalabilidad.
   - *Métrica*: Tiempo por paso de inferencia (CPU, GPU)
3. **Interpretabilidad**: Proporcionar interpretaciones claras para los profesionales de la salud, destacando casos con incertidumbre.
4. **Adaptabilidad Clínica**: Facilitar la integración del sistema en flujos de trabajo clínicos.

---

## Conjunto de Datos

- **Cantidad**: 1278 imágenes de entrenamiento y 328 de prueba.
- **Formato**: Imágenes en formato DICOM.
- **Etiquetas**: Clasificación en 22 categorías (ej. Abdomen, Tórax, Rodilla, etc.).
- **Características Adicionales**: Cada imagen cuenta con un `SOPInstanceUID` único y una columna `target` para la categoría.

---

## Preprocesamiento y Limpieza

- **Tamaño de Imagen**: Redimensionado a 256x256 píxeles.
- **Formatos**: Conversión de DICOM a PNG y JPG.
- **Escala de Color**: Escala monocromática (`Monochrome2`) con normalización de valores entre -1 y 1 o 0 y 1 dependiendo de la versión de preprocesamiento.
- **Remoción de Datos**: Eliminación de imágenes irrelevantes, como aquellas que no correspondían a radiografías válidas.

---

## Aumento de Datos

Para mejorar la variabilidad del conjunto de entrenamiento, se aplicaron las siguientes técnicas de aumento de datos:

- **Rotaciones**: Hasta 20 grados, además de rotaciones de 90 grados.
- **Traslaciones**: Horizontales y verticales.
- **Recortes (shear)**: Modificaciones en la forma de la imagen.
- **Zoom**: Simulación de acercamientos y alejamientos.

---

## Modelos Utilizados

Se evaluaron varios modelos para determinar el más adecuado para el problema:

- **InceptionV3**: F1-Score de 93.2%
- **Xception**: F1-Score de 92.9%
- **NasnetLarge**: F1-Score de 88.9%
- **MobilenetV2**: F1-Score de 94.2%
- **Densenet201**: F1-Score de 93.9%
- **Ensamble**: Se utilizó un ensamblado de modelos, logrando un F1-Score de 95.4%.

---

## Solución Seleccionada

El modelo **MobileNetV2** fue seleccionado como la solución final debido a su equilibrio entre precisión y eficiencia computacional, con las siguientes características:

- **Tamaño del modelo**: 14 MB
- **Parámetros**: 3.5 millones
- **Profundidad**: 105 capas
- **Tiempo de Inferencia**:
  - *CPU*: 25.9 ms
  - *GPU*: 3.8 ms

---

## Resultados

El modelo seleccionado demostró una precisión y velocidad óptimas para su implementación en un entorno clínico. La arquitectura de MobileNetV2 proporciona un balance entre precisión y eficiencia, alcanzando un **F1-Score de 94.2%**.

---

## Conclusiones y Próximos Pasos

El modelo propuesto muestra un alto potencial para su aplicación en el ámbito clínico, permitiendo una integración con sistemas PACS para mejorar el flujo de trabajo médico. A futuro, se planea:

1. **Aumento de Datos**: Recolección de un conjunto de datos más amplio para mejorar la generalización.
2. **Colaboración Clínica**: Trabajar junto a profesionales de la salud para mejorar la precisión de las predicciones y ajustar las etiquetas de entrenamiento.
3. **Aplicación en Detección de Anomalías**: Integrar el clasificador en sistemas de detección de anomalías para asistir en diagnósticos automáticos.
