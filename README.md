# CNN-Lentes-Gravitacionales-Clasificador

## Descripción del Proyecto

Este proyecto desarrolla una red neuronal convolucional (CNN) para la clasificación automática de lentes gravitacionales fuertes utilizando imágenes astronómicas de banda única (r-band) de 41×41 píxeles. El modelo clasifica imágenes en dos categorías: lentes gravitacionales y no lentes, logrando una precisión de prueba del 90.9% y un AUC de 0.965.

El trabajo se basa en datos del desafío Static Strong Lenses Finding Challenge Dataset (LSST), que incluye observaciones reales del Hyper Suprime-Cam (HSC) y simulaciones generadas por SIMCT. Se utiliza un subconjunto de 20,000 imágenes (10,000 lentes y 10,000 no lentes) para entrenar y evaluar el modelo.

## Antecedentes y Motivación

Las lentes gravitacionales ocurren cuando un objeto masivo deforma el espacio-tiempo, causando que la luz se curve, distorsione y amplifique. Estas lentes son cruciales para estudios en materia oscura, exoplanetas y la expansión del universo. Tradicionalmente, la detección se realiza manualmente, lo que es ineficiente para grandes volúmenes de datos de encuestas como LSST o Euclid.

Este proyecto aplica aprendizaje profundo para automatizar la detección, reduciendo el tiempo de análisis y mejorando la precisión en la identificación de arcos y anillos de Einstein.

## Conjunto de Datos

- **Fuente**: Desafío LSST DESC/SLSC.
- **Formato**: Imágenes FITS de 41×41 píxeles en banda r.
- **Categorías**:
  - Lentes reales HSC
  - No lentes reales HSC
  - Lentes simuladas SIMCT
  - No lentes simuladas SIMCT
- **Tamaño**: Reducido a 20,000 imágenes (10,000 por clase) debido a limitaciones computacionales.
- **Preprocesamiento**: Normalización a [0,1], división estratificada (80% entrenamiento, 20% prueba), con 15% de validación.

## Metodología

### Arquitectura de la CNN
- **Capas convolucionales**: Tres bloques con filtros crecientes (32, 64, 128), kernels 3×3, Batch Normalization y ReLU.
- **Pooling**: MaxPooling2D (2×2) después de cada bloque.
- **Global Average Pooling**: Para reducir dimensionalidad.
- **Dropout**: Tasa 0.5 para regularización.
- **Capa densa**: 64 unidades con ReLU, salida sigmoide para clasificación binaria.
- **Regularización**: L2 weight decay (1e-4), Batch Normalization, Dropout.

### Entrenamiento
- **Optimizador**: Adam (lr=1e-3).
- **Pérdida**: Binary Crossentropy.
- **Métricas**: Accuracy, AUC.
- **Épocas**: Máximo 50, con early stopping (paciencia=6).
- **Callbacks**: ModelCheckpoint, ReduceLROnPlateau, CSVLogger.
- **Hardware**: CPU (Intel Core i7, 8GB RAM).

## Resultados

- **Precisión de prueba**: 0.909
- **AUC de prueba**: 0.965
- **Matriz de confusión**: 1818/2000 lentes correctas, 1820/2000 no lentes correctas.
- **Reporte de clasificación**:
  - Lentes: Precisión 0.910, Recall 0.909, F1 0.909
  - No lentes: Precisión 0.909, Recall 0.910, F1 0.910
- El modelo generaliza bien a datos no vistos, con bajo sobreajuste.

## Conclusiones

El modelo demuestra la viabilidad de CNNs compactas para detectar lentes gravitacionales en imágenes de baja resolución. Los resultados validan el uso de aprendizaje profundo en astronomía, potencialmente escalable para encuestas futuras.

## Trabajo Futuro

- Integración multi-banda (g, i, z, y).
- Aumento de datos y adaptación de dominio.
- Arquitecturas más profundas (ResNet) y transfer learning.
- Técnicas de explicabilidad (Grad-CAM).
- Extensión a ranking de candidatos para encuestas a gran escala.
- Tareas de regresión para predicción de fuerza de lente.

## Autor
- **Estudiante**: Macías Macías Francisco Uriel
- **Asesor**: Dr. Cuevas Tello Juan Carlos
- **Institución**: Universidad Autónoma de San Luis Potosí, Facultad de Ingeniería
- **Curso**: Aprendizaje Automático (Diciembre 2025)

## Cómo Ejecutar

1. Clona el repositorio.
2. Instala dependencias: `pip install tensorflow keras numpy astropy scikit-learn`.
3. Ejecuta el notebook `Classificador Lentes Gravitacionais.ipynb` en Jupyter.
4. Asegúrate de tener acceso al dataset LSST (no incluido en el repo).

## Referencias

- Rubio Viana, M. (2023). Explorando nuevos modelos de materia oscura...
- Efecto de lente gravitacional — Centro de Astrofísica — Harvard & Smithsonian.
- Johana González, E. (2017). Observación y análisis de sistemas astrofísicos...
- Artificial Intelligence Analyzes Gravitational Lenses... — SLAC.
- The AGEL Survey... (2022).
- Magro et al. (2021). A comparative study of convolutional neural networks...