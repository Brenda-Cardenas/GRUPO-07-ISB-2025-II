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
Una parte central de la metodología consiste en evaluar la relación entre las características temporales tradicionales y los mapas de activación generados por la CNN. Para ello, los autores utilizan la **correlación cruzada normalizada**, una medida estadística que permite cuantificar la similitud entre dos señales o vectores.

La correlación cruzada se calcula mediante la expresión:

\[
\rho = \frac{cov(X,Y)}{\sigma_X \sigma_Y}
\]

donde \(X\) representa la característica temporal extraída de la señal y \(Y\) corresponde al mapa de activación producido por un filtro específico de la CNN.

El valor de \(\rho\) varía entre -1 y 1 e indica el grado de similitud estadística entre ambas representaciones. Un valor cercano a 1 sugiere una correlación directa alta, mientras que un valor cercano a -1 indica una relación inversa. Cuando la correlación es elevada, significa que el filtro de la CNN está capturando un patrón equivalente o muy cercano al descrito por la característica temporal tradicional. Este análisis permite determinar si las primeras capas de la CNN reproducen de forma automática propiedades que usualmente se calculan mediante *feature engineering*, aportando así mayor interpretabilidad al comportamiento interno del modelo.

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

🎯 **Repositorio recomendado (cumple exactamente con lo solicitado):**  
🔗 https://github.com/mondejar/ecg-classification

Este repositorio:

✔ Trabaja específicamente con características temporales  
✔ Usa ECG MIT-BIH  
✔ Incluye notebooks en Python  
✔ Implementa extracción de:  
- RMS  
- Varianza  
- Media  
- Picos  
- Skewness  
- Kurtosis  

✔ Contiene clasificadores (MLP, CNN)

Notebook sugerido:  
`notebooks/ecg_signal_features.ipynb`  
→ Calcula características temporales y entrena modelos.

Este repositorio es ideal para cumplir el apartado solicitado por el profesor.

---

# IV. Conclusiones Generales

Las características temporales del ECG:

- Siguen siendo fundamentales en el análisis de arritmias.  
- Permiten construir clasificadores interpretables, de bajo costo computacional y adecuados para dispositivos médicos portátiles.  
- Son la base sobre la que redes profundas construyen características más complejas.  

El análisis del primer paper muestra que las CNN **efectivamente reutilizan y mejoran** estos descriptores, lo cual aporta una visión más transparente sobre cómo operan los modelos modernos en señales biomédicas.

