# adivina-mi-dibujo
Examen
#Adivina mi Dibujo Proyecto Final Individual de IA

Sistema que predice, en tiempo real mientras dibujas con el mouse, a qué categoría
pertenece tu dibujo. Usa una Red Neuronal Convolucional (CNN) entrenada con
TensorFlow/Keras sobre el dataset Quick, Draw! de Google, con una interfaz
de lienzo interactivo construida directamente en un notebook de Google Colab.

## Categorías

`gato`  · `casa` · `sol`  · `arbol` · `pez` 

## Como ejecutarlo

1. Abre `adivina_mi_dibujo.ipynb` en [Google Colab](https://colab.research.google.com/).
2. Activa GPU: Entorno de ejecución → Cambiar tipo de entorno de ejecución → GPU (T4).
3. Ejecuta todas las celdas en orden (**Entorno de ejecución → Ejecutar todas**).
4. Al llegar a la celda del lienzo, aparecerá un cuadro negro interactivo directamente
   en el output del notebook. Dibuja con el mouse dentro del cuadro y observa cómo
   las predicciones (top-3 con % de confianza) se actualizan mientras dibujas.
5. Usa el botón "Limpiar" para borrar el lienzo y probar otro dibujo.

No se requiere ninguna instalación local ni servidor — todo corre dentro de Colab.

## Por qué la interfaz es un notebook y no una app web

El enunciado del proyecto acepta explícitamente un "notebook interactivo" como
interfaz visual válida. Se optó por este camino (usando la librería `ipycanvas`
para el lienzo de dibujo) en vez de exportar el modelo a TensorFlow.js para una
app web, debido a incompatibilidades de versión entre `tensorflowjs` y las
versiones recientes de TensorFlow/Python disponibles en Colab.

## Arquitectura del modelo

CNN construida con `tensorflow.keras`:

```
Conv2D(32) → MaxPooling2D → Conv2D(64) → MaxPooling2D → Conv2D(64)
→ Flatten → Dense(128) → Dropout(0.4) → Dense(5, softmax)
```

- Optimizador: Adam
- Función de pérdida: sparse_categorical_crossentropy
- 4,000 imágenes por categoría, dividido en 70% entrenamiento / 15% validación / 15% prueba

## Dataset

[Quick, Draw! Dataset](https://github.com/googlecreativelab/quickdraw-dataset) de Google
(dominio público), subset "numpy bitmap" (imágenes de 28x28 en escala de grises,
ya preprocesadas). El notebook descarga automáticamente el subset de las 5
categorías elegidas al ejecutarse.

## Resultados

- Accuracy en test: ver `matriz_confusion.png` y `curva_accuracy.png` en este repositorio,
  generados automáticamente por el notebook.
- Meta del proyecto: accuracy de validación ≥ 75%.

## Archivos de este repositorio

| Archivo | Descripción |
|---|---|
| `adivina_mi_dibujo.ipynb` | Notebook completo: carga de datos, entrenamiento, evaluación e interfaz de dibujo |
| `modelo_dibujo.h5` | Modelo entrenado exportado |
| `matriz_confusion.png` | Matriz de confusión sobre el conjunto de prueba |
| `curva_accuracy.png` | Curva de accuracy de entrenamiento/validación por época |

## Autor
Alexander Sebastian Ipiales
Proyecto Final Individual — Asignatura de Inteligencia Artificial (Modalidad Online)
