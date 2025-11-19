# Características Temporales y Estadísticas del ECG Enfocado en Inteligencia Artificial

## I. Marco Teórico

### 1. Teoría Breve

Las características temporales y estadísticas del electrocardiograma (ECG) constituyen descriptores cuantitativos fundamentales para caracterizar la actividad eléctrica del corazón a lo largo del tiempo. Estos parámetros representan la base del análisis automatizado de señales cardíacas mediante técnicas de inteligencia artificial, capturando tanto las propiedades morfológicas como las variaciones dinámicas de la señal.

<img src="https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Caracteristicas_ECG_IA/figura1_forma_onda_ecg.jpg" alt="Forma de onda ECG típica" width="600">

*Figura 1. Forma de onda de un latido cardíaco único con intervalos clave: PR, QT y segmento ST [1].*

En el dominio temporal, las características principales incluyen los intervalos RR, la duración del complejo QRS, los segmentos ST, y los intervalos PR y QT, los cuales reflejan diferentes fases del ciclo cardíaco. La variabilidad de estos intervalos proporciona información valiosa sobre el tono autonómico y la función cardiovascular. Las características estadísticas abarcan medidas como la media, desviación estándar, curtosis, asimetría, valores máximos y mínimos, así como percentiles de la señal, que permiten cuantificar la distribución y comportamiento general de los datos [2].

<img src="https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Caracteristicas_ECG_IA/figura2_arritmias.jpg" alt="Tipos de arritmias" width="600">

*Figura 2. Ejemplos de señales de latidos cardíacos con diferentes tipos de arritmias [1].*

La extracción de estas características es crucial en sistemas de diagnóstico asistido por computadora, donde los algoritmos de aprendizaje automático requieren representaciones numéricas compactas de las señales para realizar tareas de clasificación, detección de anomalías y predicción de eventos cardíacos. Los métodos modernos de deep learning han demostrado capacidad para aprender automáticamente estas representaciones, aunque las características diseñadas manualmente siguen siendo relevantes para modelos interpretables y con conjuntos de datos limitados [3].

El análisis de características temporales permite la detección de arritmias, isquemia miocárdica y otras patologías cardiovasculares mediante la identificación de patrones anormales en la morfología de las ondas P, complejos QRS y ondas T. Las métricas estadísticas complementan este análisis al proporcionar información sobre la estabilidad de la señal, presencia de ruido y variabilidad inherente al ritmo cardíaco. La combinación de ambos tipos de características ha demostrado eficacia en la construcción de modelos robustos de clasificación con alta precisión diagnóstica.

La selección adecuada de características impacta directamente el rendimiento del modelo en aplicaciones de inteligencia artificial sobre señales ECG. Las técnicas de reducción de dimensionalidad como PCA (Principal Component Analysis) y métodos de selección de características basados en información mutua o importancia de features permiten identificar los descriptores más relevantes para cada tarea específica, mejorando la eficiencia computacional y la generalización del modelo.

### 2. Papers que Han Usado el Análisis Temporal y Estadístico del ECG

#### Paper 1: Metodologías para el Procesamiento de la Señal Electrocardiográfica: Análisis Temporal y Estadístico

**Objetivo del Estudio:**

Este estudio presenta metodologías diferenciadas para el procesamiento de señales ECG según su aplicación: un enfoque clínico orientado a la detección de patologías mediante análisis de características temporales, y un enfoque biométrico para identificación de personas basado en descriptores estadísticos de la señal.

**Metodología:**

**1. Análisis de Características Temporales (Enfoque Clínico)**

El análisis temporal se centra en la morfología de la onda y la duración precisa de los eventos cardíacos. Para lograr una medición efectiva, se emplean técnicas de filtrado digital y la Transformada Wavelet Continua (CWT), la cual permite descomponer la señal en diferentes escalas para facilitar la detección de los puntos fiduciales (ondas P, Q, R, S, T).

Los principales parámetros extraídos mediante este método incluyen:

- **Intervalo RR:** Definido como la distancia temporal entre picos R consecutivos, es la base para el cálculo de la frecuencia cardíaca instantánea y el análisis de su variabilidad.
- **Intervalo QT:** Comprende desde el inicio del complejo QRS hasta el final de la onda T. Dado que este intervalo varía con el ritmo cardíaco, es imperativo su corrección (QTc) para el diagnóstico de patologías como arritmias. Para ello, se utiliza habitualmente la Fórmula de Bazett:

$$QT_c = \frac{QT}{\sqrt{RR}}$$

**2. Análisis de Características Estadísticas (Enfoque Biométrico)**

Para aplicaciones de identificación de personas, se recurre a descriptores estadísticos que caracterizan la distribución de amplitudes de la señal en el dominio del tiempo, independientemente de su morfología clínica estricta.

Se destacan dos grupos de características:

- **Parámetros de Hjorth:** Son descriptores basados en la varianza y sus derivadas.
  - *Actividad:* Representa la potencia o energía promedio de la señal (varianza).
  - *Movilidad:* Estima la frecuencia media de la señal, calculada mediante la razón entre la desviación estándar de la primera derivada y la desviación estándar de la señal original.
  - *Complejidad:* Cuantifica la similitud de la señal con una onda sinusoidal pura.

- **Estadísticas de Orden Superior:**
  - *Asimetría (Skewness):* Evalúa el grado de simetría de la distribución de datos respecto a la media.
  - *Curtosis:* Mide el grado de apuntamiento o concentración de los datos. En el ECG, este parámetro es particularmente relevante debido a la naturaleza impulsiva de los complejos QRS frente a la línea isoeléctrica.

**Dataset empleado:** Se utilizaron sistemas de adquisición tipo Holter y bases de datos estandarizadas como MIT-BIH para validación clínica. Para el enfoque biométrico, se trabajó con un vector inicial de 18 características estadísticas.

**Resultados Obtenidos:**

**Validación Clínica:**
- La implementación de algoritmos basados en Wavelets, integrados en sistemas de adquisición tipo Holter, demostró eficacia en la eliminación de ruido (interferencia de red y línea base) y en la detección precisa de intervalos RR y QT corregidos.
- Los resultados fueron validados satisfactoriamente frente a bases de datos estandarizadas como MIT-BIH.

**Optimización Biométrica:**
- Mediante el Análisis de Varianza (ANOVA) aplicado a un vector inicial de 18 características, se determinó que la **Movilidad** y la **Curtosis** son las características estadísticamente más significativas para la discriminación entre individuos.
- El uso exclusivo de estas dos características optimizadas permitió mantener una exactitud de identificación superior al 99% **(99.07% para ECG)**.
- Se demostró que es posible lograr un alto rendimiento con una baja carga computacional, reduciendo el conjunto de características de 18 a 2 sin pérdida significativa de precisión.

**Conclusiones Principales:**

- La Transformada Wavelet Continua resulta efectiva para la extracción precisa de características temporales relevantes en el contexto clínico, permitiendo una detección confiable de intervalos críticos para el diagnóstico de arritmias.
- Los parámetros de Hjorth, específicamente la Movilidad y la Curtosis, son suficientes para lograr una identificación biométrica altamente precisa basada en ECG.
- La optimización mediante selección de características estadísticamente significativas reduce la complejidad computacional manteniendo el rendimiento, lo que facilita la implementación en sistemas de tiempo real.
- Ambos enfoques (clínico y biométrico) demuestran que el análisis temporal y estadístico del ECG puede adaptarse efectivamente a diferentes aplicaciones mediante la selección apropiada de características.

---

#### Paper 2: Towards Uncovering Feature Extraction From Temporal Signals in Deep CNN: the ECG Case Study

**Autores:** No especificado en la fuente consultada

**Publicación:** IEEE

**Año:** 2020

**Documento:** DOI: 10.1109/EMBC44109.2020.9207360

**Objetivo del Estudio:**

El objetivo de este estudio es comprender qué características temporales de la señal ECG aprende una red neuronal convolucional unidimensional (1D-CNN) cuando procesa la señal en su forma original. Se realiza una comparación entre las activaciones internas de la red y un conjunto de características temporales clásicas como la media, valor máximo, RMS, varianza, skewness y kurtosis, ampliamente utilizadas en el análisis tradicional del ECG. Esta comparación permite evaluar si la CNN está capturando los mismos patrones que normalmente identifican los especialistas, aportando interpretabilidad a modelos que, aunque alcanzan alto rendimiento en clasificación de arritmias, suelen ser difíciles de comprender en su funcionamiento interno.

**Metodología:**

**Dataset empleado:**
- MIT-BIH Arrhythmia Database (PhysioNet)
- 48 pacientes
- Frecuencia de muestreo: 360 Hz
- Aproximadamente 109,000 latidos
- 16 clases de arritmias
- Segmentación: 1-2 segundos alrededor del QRS (~500 muestras)
- Preprocesamiento: normalización estadística, data augmentation (10% overlap)
- División: 90% entrenamiento - 10% prueba

**Características temporales empleadas (15 en total):**

El estudio utiliza características que describen propiedades estadísticas fundamentales del segmento de señal:

- **Amplitud y medida central:** Media, valor máximo, valor mínimo
- **Energía:** RMS (Root Mean Square), SMR (Square Mean Root)
- **Medidas de dispersión:** Varianza, desviación estándar
- **Factores de forma:** Crest factor (Max/RMS), Shape factor
- **Estadística de distribución:** Skewness (asimetría), Kurtosis
- **Momentos de orden superior:** Momentos centrales de quinto y sexto orden

**Arquitectura 1D-CNN implementada:**

La red convolucional está diseñada para aumentar progresivamente la complejidad:

| Capa | Número de Filtros | Tamaño de Kernel |
|------|-------------------|------------------|
| Conv1 | 4 | 8 |
| Conv2 | 8 | 8 |
| Conv3 | 8 | 16 |
| Conv4 | 16 | 16 |
| Conv5+ | ... | ... |

- Total: 10 capas convolucionales
- Max pooling intercalado
- Capa fully connected
- Softmax final (16 clases)
- Dropout para evitar overfitting

**Análisis de correlación cruzada:**

Se empleó correlación cruzada normalizada para cuantificar la similitud entre características temporales tradicionales y mapas de activación de la CNN:

$$\rho = \frac{cov(X,Y)}{\sigma_X \sigma_Y}$$

donde *X* representa la característica temporal y *Y* el mapa de activación. Un valor cercano a 1 indica que el filtro CNN captura un patrón equivalente a la característica temporal tradicional.

**Resultados Obtenidos:**

**Correlación entre características humanas y filtros CNN:**

Las primeras capas de la red mostraron alta correlación con características temporales tradicionales:

| Característica Temporal | Correlación | Capa/Filtro |
|------------------------|-------------|-------------|
| Media (F1) | -0.882 | Conv1-Filter1 |
| Máximo (F2) | -0.808 | Conv1-Filter1 |
| RMS (F3) | +0.875 | Conv1-Filter2 |
| SMR (F4) | +0.882 | Conv1-Filter2 |
| Crest Factor (F9) | -0.838 | Conv1-Filter1 |

**Comparación de rendimiento:**
- MLP (usando solo características temporales humanas): **96% accuracy**
- 1D-CNN (procesando señal cruda): **99.6% accuracy**

Las capas profundas generan características abstractas no triviales después de capturar energía, picos y amplitud en las capas iniciales.

**Conclusiones Principales:**

- Las primeras capas de la CNN replican automáticamente el análisis estadístico humano, aprendiendo características temporales clásicas como media, RMS, varianza y factores de forma sin necesidad de feature engineering manual.
- La red no solo reproduce estas características, sino que las utiliza como base para generar representaciones más complejas y abstractas en capas profundas, lo que explica su rendimiento superior.
- Las características temporales tradicionales siguen siendo fundamentales y relevantes para el análisis de arritmias, ya que proporcionan la base interpretable sobre la cual los modelos profundos construyen su conocimiento.
- Este enfoque aporta transparencia e interpretabilidad a los modelos de deep learning en señales biomédicas, demostrando que las CNN efectivamente reutilizan y mejoran los descriptores temporales tradicionales.
- Es posible construir sistemas híbridos que combinen la interpretabilidad de las características temporales con el alto rendimiento de las redes profundas, siendo adecuados para dispositivos médicos portátiles y sistemas de tiempo real

---

## II. Repositorio de GitHub Seleccionado

**Nombre del Repositorio:** Heart-Rate-features

**Autor:** Kimia Rezaei

**URL:** https://github.com/kimiarezaei/Heart-Rate-features

**Descripción del Proyecto:**

Este repositorio implementa un pipeline completo para la extracción de características temporales y de frecuencia de señales de frecuencia cardíaca, facilitando el análisis de variabilidad del ritmo cardíaco (HRV). El proyecto demuestra todo el proceso desde el preprocesamiento de señales ECG, detección de picos R, cálculo de intervalos RR, hasta la extracción de 16 características relevantes para aplicaciones de diagnóstico médico mediante inteligencia artificial [4].

**Lenguaje Principal:** Python

**Notebooks Incluidos:**

- `HRV calculation and feature extraction.ipynb`: Notebook principal que demuestra el flujo completo de trabajo, incluyendo preprocesamiento, detección de picos, cálculo de frecuencia cardíaca y extracción de características con visualizaciones detalladas.

**Características del Repositorio:**

- **Dataset utilizado:** Señal ECG de ejemplo incluida en el repositorio para demostración del proceso completo
- **Técnicas de preprocesamiento:** Filtrado de señal, normalización y interpolación de intervalos RR
- **Características temporales extraídas:**
  - Media de intervalos NN (muNN)
  - Desviación estándar de intervalos NN (SDNN)
  - Raíz cuadrada media de diferencias sucesivas (RMSSD)
  - Índice triangular (TRindex)
  - Curtosis y asimetría
  - Entropía aproximada (ApEn)
  - Parámetros del diagrama de Poincaré (SD1, SD2, SD ratio)
  - Índice simpático cardíaco modificado (CSI_Modified)
  - Índice vagal cardíaco (CVI)

- **Características de frecuencia computadas:**
  - Potencia de muy baja frecuencia (VLF)
  - Potencia de baja frecuencia (LF)
  - Potencia de alta frecuencia (HF)
  - Relación LF/HF

- **Bibliotecas utilizadas:** PyHRV, BioSPPy, NeuroKit2, Nolds, Spectrum, NumPy, SciPy, Pandas, Matplotlib

- **Aplicación clínica:** Las características extraídas se validaron mediante clasificadores de Random Forest para evaluar su efectividad como herramienta de diagnóstico de lesiones cerebrales en bebés, específicamente para la clasificación de encefalopatía hipóxico-isquémica y detección de convulsiones [4].

**Relevancia:**

El repositorio aborda de manera exhaustiva el análisis de características temporales y estadísticas del ECG mediante la implementación de algoritmos especializados para la extracción de HRV. La combinación de características en dominios temporal y frecuencial permite capturar información complementaria sobre la regulación autonómica cardíaca. El código está estructurado de forma modular, facilitando su reutilización en diferentes contextos clínicos y de investigación.

**Ventajas del Repositorio:**

- Implementación completa con visualizaciones paso a paso del proceso de extracción de características
- Código bien documentado con descripciones claras de cada parámetro calculado
- Utiliza bibliotecas validadas científicamente para el análisis de señales biomédicas
- Incluye características avanzadas como entropía aproximada y análisis de Poincaré
- Aplicación clínica demostrada en el paper asociado con resultados experimentales publicados en IEEE EMBC 2024
- Fácil adaptación para diferentes datasets de ECG mediante una interfaz de función simple

---

## Referencias

[1] J. Chen, H. Pu, and D. Wang, "Artificial intelligence analysis of EEG amplitude in intensive heart care," *Journal of Healthcare Engineering*, vol. 2021, Article ID 6284035, 2021. doi: 10.1155/2021/6284035.

[2] M. F. Safdar, R. M. Nowak, and P. Pałka, "Pre-processing techniques and artificial intelligence algorithms for electrocardiogram (ECG) signals analysis: A comprehensive review," *Computers in Biology and Medicine*, vol. 170, Article 107908, Mar. 2024. doi: 10.1016/j.compbiomed.2023.107908.

[3] U. R. Acharya et al., "A deep convolutional neural network model to classify heartbeats," *Computers in Biology and Medicine*, vol. 89, pp. 389-396, 2017.

[4] K. Rezaei, K. Yu, S. R. Mathieson, A. Flynn, G. Lightbody, G. B. Boylan, and W. P. Marnane, "Assessing the effectiveness of heart rate variability as a diagnostic tool for brain injuries in infants," in *Proc. 46th Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC)*, Orlando, FL, USA, 2024, pp. 1-4. doi: 10.1109/EMBC53108.2024.10782021.

[5] "Towards uncovering feature extraction from temporal signals in deep CNN: The ECG case study," in *Proc. 42nd Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC)*, 2020, pp. 1-4. doi: 10.1109/EMBC44109.2020.9207360.
