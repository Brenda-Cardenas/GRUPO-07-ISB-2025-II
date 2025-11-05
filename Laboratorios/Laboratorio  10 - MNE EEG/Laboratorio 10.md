# **Laboratorio 10 - Análisis de Componentes Independientes (ICA)**

## **1. Introducción**

El Análisis de Componentes Independientes (ICA) es una técnica que realiza una separación ciega de fuentes. Es una herramienta útil para el procesamiento de señales electroencefalográficas (EEG). En registros multicanal, las señales EEG representan mezclas lineales de múltiples fuentes neuronales y no neuronales, muchas de las cuales son artefactos fisiológicos como movimientos oculares, actividad muscular o interferencia eléctrica [1]. ICA permite descomponer estas señales en componentes independientes, facilitando de esta manera la identificación y eliminación de dichos artefactos sin afectar las señales cerebrales de interés [2]. 

Matemáticamente, ICA se basa en la estimación de una matriz de separación que maximiza la independencia entre componentes, comúnmente optimizada mediante criterios como la kurtosis o la no-gaussianidad [3]. En la práctica, esto permite reconstruir la señal EEG excluyendo las fuentes contaminantes. Actualmente, el uso de ICA se ha consolidado tanto en entornos experimentales como clínicos, siendo fundamental en estudios de conectividad funcional, neuroergonomía y diagnóstico de trastornos como epilepsia, TDAH o demencia [4,5]. Además, su integración con librerías especializadas como MNE-Python ha hecho posible su aplicación automatizada y reproducible en investigaciones con grandes volúmenes de datos [1].

## **2. Objetivos**

- **Objetivo general:**  
  Implementar un proceso de limpieza de señales EEG utilizando el método de Análisis de Componentes Independientes (ICA).

- **Objetivos específicos:**  
  - Aplicar un filtro pasa banda para eliminar ruido de baja y alta frecuencia.  
  - Incorporar un filtro notch de 60 Hz para reducir la interferencia de la red eléctrica.  
  - Utilizar ICA para identificar y eliminar artefactos fisiológicos como parpadeos o movimientos musculares.  
  - Visualizar la señal antes y después del proceso de filtrado.

## **3. Materiales**

| **Elemento** | **Descripción / Uso** |
|---------------|-----------------------|
| **Laptop personal** | Se utilizó para ejecutar el código y procesar las señales EEG. |
| **Python 3.13** | Lenguaje de programación utilizado para aplicar los filtros y el método ICA. |
| **Archivo `.txt` del Ultracortex** | Contiene los registros crudos de la señal EEG capturados por el dispositivo Ultra Cortex Mark IV. |
| **MNE-Python** | Librería empleada para el procesamiento, visualización y limpieza de señales EEG. |
| **Filtros digitales (pasa banda y notch)** | Implementados para eliminar ruido de baja frecuencia y la interferencia de 60 Hz. |

## **4. Metodología**

1. **Obtención y carga de datos EEG:**  
   Los datos electroencefalográficos (EEG) fueron obtenidos utilizando el equipo **Ultra Cortex Mark IV**, que cuenta con **16 electrodos secos** de base de **plata clorada** y una **frecuencia de muestreo de 125 Hz**. Para la carga de los registros EEG crudos se emplearon las funciones de la librería **MNE-Python**, específicamente:  
  - `mne.io.read_raw_edf()`: para leer archivos en formato `.edf`.  
  - `mne.datasets.eegbci.load_data()`: para acceder directamente a los registros del **conjunto de datos EEG BCI**, ampliamente utilizado en investigaciones sobre **interfaces cerebro-computadora (BCI)** y otros estudios neurocientíficos.  

  Esta función facilita la descarga y carga de los datos EEG de la competencia BCI, integrándose de forma eficiente al flujo de análisis en MNE.  

2. **Filtrado de la señal:**  
   - **Filtro pasa banda (5–50 Hz):** Se aplicó para eliminar componentes de baja frecuencia (movimientos oculares, respiración) y de alta frecuencia (ruido eléctrico).  
   - **Filtro notch (60 Hz):** Se utilizó para eliminar la interferencia proveniente del sistema eléctrico.

3. **Aplicación de ICA:**  
   - Se ajustó un modelo ICA con `mne.preprocessing.ICA()`.  
   - Se identificaron los componentes correspondientes a artefactos oculares y musculares.  
   - Dichos componentes fueron excluidos de la reconstrucción de la señal limpia mediante `ica.apply()`.

4. **Verificación del filtrado:**  
   Se graficaron los datos antes y después del filtrado para evaluar la eliminación de artefactos.

## **5. Resultados**

Tras aplicar ICA, la señal EEG mostró una notable reducción en los picos relacionados con parpadeos y contracciones musculares. La figura siguiente ilustra la diferencia entre la señal cruda y la señal filtrada:

| **Señal sin filtrar** | **Señal filtrada con ICA** |
|------------------------|-----------------------------|
| ![EEG cruda](imagenes/figura_1.png) | ![EEG filtrada](imagenes/figura_2.png) |

El resultado evidencia que el método ICA permite separar la actividad cerebral de artefactos no deseados, obteniendo una señal más limpia y adecuada para las etapas siguientes de **preprocesamiento y extracción de características**.

## **6. Conclusiones**

- El método ICA es eficaz para eliminar artefactos fisiológicos y eléctricos en señales EEG.  
- Su implementación requiere un filtrado previo (pasa banda + notch) para garantizar estabilidad numérica.  
- La señal limpia obtenida es fundamental para asegurar la validez de las características extraídas en el análisis posterior (por ejemplo, Wavelet o PSD).

## **7. Referencias**

[1] Dimigen O, Kliegl R. Shared EEG–eye-tracking data and online ICA artifact removal using MNE-Python. Behav Res Methods. 2021;53(2):713–730. doi:10.3758/s13428-020-01329-5.
[2] Tamburro G, Astolfi L. ICA-based artifact removal and source localization in high-density EEG: validation on simulated and real data. Biomed Signal Process Control. 2020;60:101951. doi:10.1016/j.bspc.2020.101951.
[3] Klug M, Gramann K. Identifying key factors for improving ICA-based decomposition of EEG data in mobile and stationary experiments. Eur J Neurosci. 2021;54(12):8406–8420. doi:10.1111/ejn.15435.
[4] Jorge J, van der Zwaag W, Figueiredo P. EEG–fMRI integration for the study of human brain function. NeuroImage. 2022;252:119027. doi:10.1016/j.neuroimage.2022.119027.
[5] Fahimi F, Saeed S, Rahman MA, Fiok K, Aslani N, Menon C. A review on machine learning models for the characterization of EEG in Parkinson’s disease. Biomed Signal Process Control. 2022;73:103459. doi:10.1016/j.bspc.2021.103459.
