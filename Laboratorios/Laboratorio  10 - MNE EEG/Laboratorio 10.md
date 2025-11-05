# **Laboratorio 10 - Análisis de Componentes Independientes (ICA)**

## **1. Introducción**

El Análisis de Componentes Independientes (ICA) es una técnica que realiza una separación ciega de fuentes. Es una herramienta útil para el procesamiento de señales electroencefalográficas (EEG). En registros multicanal, las señales EEG representan mezclas lineales de múltiples fuentes neuronales y no neuronales, muchas de las cuales son artefactos fisiológicos como movimientos oculares, actividad muscular o interferencia eléctrica [1]. ICA permite descomponer estas señales en componentes independientes, facilitando de esta manera la identificación y eliminación de dichos artefactos sin afectar las señales cerebrales de interés [2]. 

<p align="center">
  <img src="https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%20%2010%20-%20MNE%20EEG/Multimedia/ICA%20COMPONENTS.jpg" alt="ICA Components" width="800">
  <br>
  <em>Figura 1. Componentes independientes (ICA) del registro EEG [3].</em>
</p>

Matemáticamente, ICA se basa en la estimación de una matriz de separación que maximiza la independencia entre componentes, comúnmente optimizada mediante criterios como la kurtosis o la no-gaussianidad [4]. En la práctica, esto permite reconstruir la señal EEG excluyendo las fuentes contaminantes. Actualmente, el uso de ICA se ha consolidado tanto en entornos experimentales como clínicos, siendo fundamental en estudios de conectividad funcional, neuroergonomía y diagnóstico de trastornos como epilepsia, TDAH o demencia [5,6]. Además, su integración con librerías especializadas como MNE-Python ha hecho posible su aplicación automatizada y reproducible en investigaciones con grandes volúmenes de datos [1].

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

1. **Obtención y carga de datos EEG**  
   - Los registros electroencefalográficos (EEG) se obtuvieron utilizando el equipo **Ultra Cortex Mark IV**, un dispositivo no invasivo con **16 electrodos secos** de base de **plata clorada**, operando a una **frecuencia de muestreo de 125 Hz**.  
   - Los archivos generados por el equipo fueron exportados en formato `.txt` y cargados mediante las funciones del paquete **MNE-Python**, ampliamente utilizado en neurociencia para el procesamiento y análisis de EEG.  
   - Se utilizaron las siguientes funciones:  
     - `mne.io.read_raw_edf()`: para la lectura de archivos `.edf` y conversión a objetos Raw de MNE.  
     - `mne.datasets.eegbci.load_data()`: para acceder al **dataset EEG BCI**, una base de datos de referencia en estudios de **interfaces cerebro-computadora (BCI)**.  
   - Este procedimiento permitió integrar los registros en un flujo de trabajo reproducible y compatible con las herramientas de visualización y análisis espectral de MNE.

2. **Preprocesamiento y filtrado de la señal**  
   - Con el fin de mejorar la calidad de la señal y eliminar ruido ambiental, se aplicaron filtros digitales implementados en MNE:  
     - **Filtro pasa banda (5–50 Hz):** permitió atenuar componentes de baja frecuencia (movimientos oculares, respiración) y de alta frecuencia (ruido eléctrico o muscular).  
     - **Filtro notch (60 Hz):** diseñado para eliminar interferencias provenientes de la red eléctrica de corriente alterna.  
   - Adicionalmente, se inspeccionó visualmente el registro EEG para verificar la estabilidad del ritmo basal y la presencia de posibles artefactos de origen fisiológico (como parpadeos o tensión muscular).  
   - Se segmentaron los datos en **épocas** de duración uniforme para facilitar el análisis independiente de cada bloque temporal y preparar el dataset para la aplicación del método ICA.

3. **Aplicación del Análisis de Componentes Independientes (ICA)**  
   - Se implementó el modelo ICA mediante la función `mne.preprocessing.ICA()`, especificando el número de componentes y el método de descomposición (por ejemplo, **FastICA** o **Infomax**, según la configuración).  
   - El procedimiento consistió en:  
     - Ajustar el modelo ICA sobre los datos preprocesados mediante `ica.fit(raw)`.  
     - Identificar componentes asociados a artefactos oculares (picos frontales sincronizados con el parpadeo) y musculares (alta frecuencia y baja amplitud).  
     - Excluir estos componentes utilizando `ica.exclude` y reconstruir la señal limpia con `ica.apply(raw)`.  
   - Este paso permitió separar la actividad cerebral verdadera de las señales contaminantes, mejorando la precisión del análisis posterior.

4. **Verificación y evaluación del filtrado ICA**  
   - Se compararon las trazas de EEG **antes y después del filtrado**, evaluando visualmente la reducción de artefactos.  
   - Se generaron gráficos de los **componentes independientes** y de la señal reconstruida para confirmar la correcta eliminación de interferencias sin pérdida de información neuronal relevante.  
   - Finalmente, se documentaron los resultados visuales y cuantitativos, observando una mayor estabilidad en la línea base y una mejora en la claridad de los ritmos alfa y beta, indicativos de un filtrado exitoso.

## **5. Resultados**
📘 [Acceso al código realizado](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/tree/main/Laboratorios/Laboratorio%20%2010%20-%20MNE%20EEG)


<p align="center">
  <img src="https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%20%2010%20-%20MNE%20EEG/Multimedia/ICAScores.jpg" width="800">
  <br>
  <em>Figura 2. Puntuaciones de los componentes ICA, mostrando la contribución relativa de cada componente en el registro EEG.</em>
</p>

El resultado evidencia que el método ICA permite separar la actividad cerebral de artefactos no deseados, obteniendo una señal más limpia y adecuada para las etapas siguientes de **preprocesamiento y extracción de características**.

## **6. Referencias**

[1] Dimigen O, Kliegl R. Shared EEG–eye-tracking data and online ICA artifact removal using MNE-Python. Behav Res Methods. 2021;53(2):713–730. doi:10.3758/s13428-020-01329-5.

[2] Tamburro G, Astolfi L. ICA-based artifact removal and source localization in high-density EEG: validation on simulated and real data. Biomed Signal Process Control. 2020;60:101951. doi:10.1016/j.bspc.2020.101951.

[3] Kiss Á, Huszár OM, Bodosi B, Kelemen A, et al. Automated preprocessing of 64-channel electroencephalograms recorded by Biosemi instruments. MethodsX. 2023;11(4–5):102378. doi:10.1016/j.mex.2023.102378

[4] Klug M, Gramann K. Identifying key factors for improving ICA-based decomposition of EEG data in mobile and stationary experiments. Eur J Neurosci. 2021;54(12):8406–8420. doi:10.1111/ejn.15435.

[5] Jorge J, van der Zwaag W, Figueiredo P. EEG–fMRI integration for the study of human brain function. NeuroImage. 2022;252:119027. doi:10.1016/j.neuroimage.2022.119027.

[6] Fahimi F, Saeed S, Rahman MA, Fiok K, Aslani N, Menon C. A review on machine learning models for the characterization of EEG in Parkinson’s disease. Biomed Signal Process Control. 2022;73:103459. doi:10.1016/j.bspc.2021.103459.
