# Laboratorio 12 - Características Temporales / Estadísticas aplicadas al Análisis y Clasificación de Señales ECG  

## I. Teoría
### 1. Introducción al análisis temporal en ECG  
La señal ECG es una señal que se caracteriza por ser unidimensional, no estacionaria y fisiológicamente interpretable, cuya morfología contiene información sobre el estado eléctrico del corazón. Tradicionalmente, el análisis para clasificación o detección de arritmias se divide en:
- Dominio del tiempo (temporal)
- Dominio de la frecuencia (por transformadas)
- Dominio tiempo–frecuencia (wavelets)

En el presente laboratorio se discutirá sobre papers relacionados a las características temporales, estas son descriptores estadísticos derivados directamente de los valores de amplitud de la señal en el tiempo dentro de una ventana que representa un latido o segmento del ECG.

### 2. Características temporales
Son métricas calculadas directamente sobre los valores de una señal segmentada. Permiten cuantificar:
- Intensidad (media, RMS, pico)
- Variabilidad (varianza, desviación estándar)
- Forma (crest factor, shape factor)
- Distribución estadística (skewness, kurtosis, momentos de orden superior)

Estas características no requieren transformaciones complejas y son computacionalmente eficientes. Por eso se utilizan ampliamente en:
- Diagnóstico de arritmias  
- Sistemas embebidos (wearables, IoT)  
- Clasificadores de tiempo real  

### 3. Lista detallada de características temporales más usadas en ECG
#### **3.1 Amplitud y medida central**
- **Media**: es el nivel promedio, indica desplazamientos en la línea base.
- **Máximo y mínimo**: amplitud de los picos.

#### **3.2 Energía**
- **RMS (Root Mean Square):** Captura la energía cuadrática del segmento. Es sensible a picos del QRS.
- **SMR (Square Mean Root):** Variante del RMS, pero promediando raíces antes de elevar.
- 
#### **3.3 Medidas de dispersión**
- **Varianza y desviación estándar:** Indican cuánta variación existe dentro del latido. Los latidos clasificados como patológicos suelen presentar mayor dispersión.

#### **3.4 Factores de forma**
- **Crest factor**: Max/RMS, es la diferencia entre picos y energía total.
- **Shape factor**:  Mide cuán puntiaguda o plana es la forma general del pulso.

#### **3.5 Estadística de distribución**
- **Skewness (asimetría)**: Detecta inclinación del pulso hacia izquierda/derecha (ondas P o T anormales).
- **Kurtosis**: Cuantifica qué tan afilado es el pulso (picos agudos o QRS estrechos).
- **Momentos de orden 5 y 6**: Capturan detalles finos de la distribución del segmento.
- 
### 4. Importancia de estas características en ECG  
Estas features describen matemáticamente los elementos más relevantes del latido:
- Picos del QRS  
- Amplitud global  
- Energía del circuito eléctrico  
- Forma general del ciclo cardíaco  
- Diferencias entre latidos normales y anormales  

Y se utilizan en:
- Clasificación supervisada (MLP, SVM, Random Forest)  
- Algoritmos de detección temprana  
- Análisis comparativo con redes profundas (1D-CNN)  
- Interpretabilidad de modelos de Deep Learning  


## II. Papers que utilizan características temporales para ECG
## **Paper 1: Towards Uncovering Feature Extraction From Temporal Signals in Deep CNN: the ECG Case Study**

#### 🌟 1. Objetivo del paper  
El objetivo del estudio es comprender qué características temporales de la señal ECG aprende una red neuronal convolucional unidimensional cuando se le entrega la señal en su forma original. Se comparan las activaciones internas de la red con un conjunto de características temporales clásicas como la media, el valor máximo, el RMS, la varianza, la skewness y la kurtosis, que son ampliamente utilizadas en el análisis tradicional del ECG. Esta comparación permite evaluar si la CNN está capturando los mismos patrones que normalmente identifican los especialistas, lo cual es relevante porque, aunque estos modelos alcanzan un rendimiento elevado en la clasificación de arritmias, su funcionamiento interno suele ser difícil de interpretar. De esta manera, el estudio busca ofrecer una visión más clara y comprensible sobre cómo las redes profundas procesan y extraen información de señales biomédicas.

#### 🌟 2. Dataset utilizado  
Dataset MIT-BIH Arrhythmia Database (PhysioNet)  
- 48 pacientes  
- 360 Hz de muestreo  
- ~109,000 latidos  
- 16 clases  
- Segmentación: 1–2 s alrededor del QRS (~500 samples)

Se realizó:
- Normalización estadística  
- Data augmentation (10% overlap)  
- Split: 90% train – 10% test  

#### 🌟 3. Metodología
##### A. Características temporales empleadas
El estudio utiliza un conjunto de **quince características temporales** ampliamente empleadas en el análisis del ECG. Estas características permiten describir propiedades estadísticas fundamentales del segmento de señal, tales como amplitud, energía, variabilidad y forma. Entre las principales se encuentran:

- Media  
- Valor máximo  
- RMS  
- SMR  
- Varianza  
- Desviación estándar  
- Skewness  
- Kurtosis  
- Crest factor  
- Momentos centrales de quinto y sexto orden  

Todas estas características se encuentran definidas matemáticamente en el artículo y representan el enfoque tradicional de *feature engineering* aplicado a señales biomédicas.

##### B. Representaciones aprendidas por la CNN 1D
De manera complementaria, los autores analizan las representaciones internas generadas por la **red neuronal convolucional unidimensional (1D-CNN)**. Para ello estudian los **mapas de activación** producidos por cada filtro en las capas convolucionales.  
Estos mapas representan los patrones que la red considera relevantes al procesar directamente la señal ECG en su forma cruda.

##### C. Comparación entre ambas representaciones
Para determinar el grado de similitud entre las características temporales tradicionales y las características aprendidas por la CNN, el estudio emplea un análisis de **correlación cruzada normalizada**.  
Este procedimiento compara cada característica temporal con cada mapa de activación, permitiendo identificar si la red está aprendiendo patrones equivalentes a los utilizados en métodos clásicos.  
Una correlación elevada indica que la CNN captura propiedades similares a las que se obtienen mediante *feature engineering* manual.

#### 🌟 4. Arquitectura de la 1D-CNN  
La arquitectura está diseñada para aumentar progresivamente la complejidad:

| Capa | # Filtros | Tamaño kernel |
|------|-----------|----------------|
| Conv1 | 4 | 8 |
| Conv2 | 8 | 8 |
| Conv3 | 8 | 16 |
| Conv4 | 16 | 16 |
| Conv5+ | ... | ... |
| Total: 10 capas convolucionales |

Además:
- Max pooling intercalado  
- Capa fully connected  
- Softmax final (16 clases)  
- Dropout para evitar overfitting  

#### 🌟 5. Análisis de correlación cruzada (clave del paper)  
Para comparar las características temporales tradicionales con las características aprendidas por la CNN, los autores utilizan la correlación cruzada normalizada, que permite medir qué tan parecidas son dos señales.

La fórmula empleada es: ρ = cov(X, Y) / (σ_X · σ_Y)

Aquí, **X** es la característica temporal calculada del ECG y **Y** es el mapa de activación de un filtro de la CNN.  
El valor de ρ va de -1 a 1: valores cercanos a 1 indican alta similitud y valores cercanos a 0 indican poca relación.

Este análisis permite identificar si la CNN está aprendiendo patrones similares a los que se obtienen mediante métodos clásicos de *feature engineering*, ayudando a entender mejor cómo procesa la red la señal ECG.

#### 🌟 6. Resultados principales del paper
##### **6.1 Las primeras capas aprenden características temporales humanas**
Las características con mayor correspondencia fueron:

| Feature humana | Correlación | Capa/Filtro |
|----------------|-------------|-------------|
| **Media (F1)** | -0.882 | Conv1-Filter1 |
| **Máximo (F2)** | -0.808 | Conv1-Filter1 |
| **RMS (F3)** | +0.875 | Conv1-Filter2 |
| **SMR (F4)** | +0.882 | Conv1-Filter2 |
| **Crest Factor (F9)** | -0.838 | Conv1-Filter1 |

Esto demuestra que **la CNN está replicando el análisis estadístico humano**.

###### **6.2 Las capas profundas aprenden características abstractas**
Luego de capturar:
- energía  
- picos  
- amplitud  
la red genera características **propias** no triviales.

###### **6.3 Comparación con MLP basado solo en características**
- MLP (usando solo features humanas): **96% accuracy**  
- CNN (crudo + filtros): **99.6% accuracy**

Esto confirma que:
1. Las características temporales son relevantes.  
2. La CNN las usa, pero las mejora.  

---
## 📘 **Paper 2: A Simple Time-Domain Algorithm for the Detection of Ventricular Fibrillation in ECG**  

---
# III. Repositorio de GitHub relacionado (incluye Notebook)
