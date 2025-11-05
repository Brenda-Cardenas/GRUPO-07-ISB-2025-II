# **Laboratorio 10 - Análisis de Componentes Independientes (ICA)**

## **1. Introducción**

El procesamiento de señales electroencefalográficas (EEG) es una etapa esencial en la neuroingeniería y en aplicaciones de interfaces cerebro-computadora (BCI). Las señales EEG suelen contener artefactos provenientes del parpadeo, movimiento ocular, contracciones musculares o interferencias eléctricas, los cuales pueden distorsionar la interpretación de la actividad cerebral.  
Para mitigar estos efectos, se aplican técnicas de **filtrado y limpieza** de la señal. Entre ellas, el **Análisis de Componentes Independientes (ICA)** es una de las más efectivas, pues permite separar las fuentes de señal mezcladas y eliminar aquellas que no son de origen cerebral.

Este informe describe el procedimiento de filtrado ICA aplicado a señales EEG, correspondiente a la etapa inicial del pipeline de procesamiento del proyecto (ver Figura 1), previo al preprocesamiento y extracción de características.

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
| **Python 3.10** | Lenguaje de programación utilizado para aplicar los filtros y el método ICA. |
| **Archivo `.txt` del Ultracortex** | Contiene los registros crudos de la señal EEG capturados por el dispositivo Ultra Cortex Mark IV. |
| **MNE-Python** | Librería empleada para el procesamiento, visualización y limpieza de señales EEG. |
| **Filtros digitales (pasa banda y notch)** | Implementados para eliminar ruido de baja frecuencia y la interferencia de 60 Hz. |

## **4. Metodología**

1. **Carga de datos EEG:**  
   Se importaron los datos utilizando la función `mne.io.read_raw_edf()` o `mne.datasets.eegbci.load_data()` para cargar los registros EEG crudos desde el archivo `.txt`.

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

[1] Víctor Asanza, et al. “MILimbEEG: A Dataset of EEG Signals Related to Upper and Lower Limb Execution of Motor and Motor Imagery Tasks.” *Data in Brief*, 2023.  
[2] C. S. Nayak & A. C. Anilkumar. “EEG Normal Waveforms.” *NIH*, 2023.  
[3] X. Li et al. “The Effects of Notch Filtering on Electrically Evoked Myoelectric Signals.” *J. NeuroEngineering and Rehabilitation*, 2011.  
[4] “IAC: On the Feasibility of Utilizing Neural Signals for Access Control.” *ResearchGate*, 2018.  
[5] “SmartHelm: User Studies from Lab to Field for Attention Modeling.” *ResearchGate*, 2022.
