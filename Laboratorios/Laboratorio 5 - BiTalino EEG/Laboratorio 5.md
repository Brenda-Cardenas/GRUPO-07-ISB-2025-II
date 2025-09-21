# 🧠 LABORATORIO 5: Uso de BiTalino para adquisición de señales EEG

---

## Índice

- [1. Introducción](#1-introducción)  
- [2. Objetivos](#2-objetivos)  
  - [2.1 Objetivo general](#21-objetivo-general)  
  - [2.2 Objetivos específicos](#22-objetivos-específicos)  
- [3. Materiales e Instrumentos](#3-materiales-e-instrumentos)  
- [4. Metodología](#4-metodología)  
  - [4.1 Preparación del software](#41-preparación-del-software)  
  - [4.2 Montaje de electrodos](#42-montaje-de-electrodos)  
  - [4.3 Secuencia experimental](#43-secuencia-experimental)  
  - [4.4 Ejercicios de análisis](#44-ejercicios-de-análisis)  
- [5. Resultados](#5-resultados)  
  - [5.1 Repositorio de vídeos](#51-repositorio-de-vídeos)  
  - [5.2 Gráficas obtenidas](#52-gráficas-obtenidas)  
    - [5.2.1 Señales EEG crudas y filtradas durante reposo (ojos cerrados) y fijación visual (ojos abiertos)](#521-señales-eeg-crudas-y-filtradas-durante-reposo-ojos-cerrados-y-fijación-visual-ojos-abiertos)  
    - [5.2.2 Densidad espectral de potencia (PSD) de EEG](#522-densidad-espectral-de-potencia-psd-de-eeg)  
    - [5.2.3 Potencia relativa (%) por banda](#523-potencia-relativa--por-banda)  
    - [5.2.4 Comparación de potencia α: ojos cerrados vs ojos abiertos](#524-comparación-de-potencia-α-ojos-cerrados-vs-ojos-abiertos)  
    - [5.2.5 Tarea cognitiva: Resta 100-7](#525-tarea-cognitiva-resta-100-7)  
    - [5.2.6 Comparación de potencia β durante tarea cognitiva](#526-comparación-de-potencia-β-durante-tarea-cognitiva)  
    - [5.2.7 Detección de parpadeos](#527-detección-de-parpadeos)  
- [6. Discusión e interpretación](#6-discusión-e-interpretación)  
  - [6.1 Señales crudas vs. filtradas (0.8–48 Hz + notch)](#61-señales-crudas-vs-filtradas-08-48-hz--notch)  
  - [6.2 PSD por grabación](#62-psd-por-grabación)  
  - [6.3 Potencia relativa por banda (Δ, θ, α, β, γ)](#63-potencia-relativa-por-banda-δ-θ-α-β-γ)  
  - [6.4 Comparación de α (8–13 Hz): Ojos cerrados (EC) vs. Ojos abiertos (EO)](#64-comparación-de-α-813-hz-ojos-cerrados-ec-vs-ojos-abiertos-eo)  
  - [6.5 Tarea cognitiva (resta 100–7) y comparación en β (13–30 Hz)](#65-tarea-cognitiva-resta-100-7-y-comparación-en-β-1330-hz)  
  - [6.6 Detección de parpadeos (EOG) en frontal](#66-detección-de-parpadeos-eog-en-frontal)  
  - [6.7 Actividad cognitiva libre: Escuchar música](#67-actividad-cognitiva-libre-escuchar-música)  
- [7. Limitaciones y mejoras](#7-limitaciones-y-mejoras)  
- [8. Conclusiones](#8-conclusiones)  
- [9. Aporte de los integrantes](#9-aporte-de-los-integrantes)  

---

## 1. Introducción
La electroencefalografía (EEG) registra la actividad cerebral eléctrica usando electrodos en el cuero cabelludo. Posee un alta resolución temporal, debido a que su frecuencia se encuentra en el rango de milisegundos, lo que la ha llevado a convertirse en el instrumento principal del diagnóstico clínico, del desarrollo de interfaces de crecimiento del cerebro-computer (BCI) y del uso en investigación en neurociencia cognitiva [1].

### 1.1 Generación de la señal EEG

La corteza cerebral es la capa más externa del encéfalo, formada por sustancia gris con un grosor de 2 a 4 mm. Está organizada en seis capas histológicas que contienen diferentes tipos de neuronas y conexiones, siendo que en las capas III y V dónde se encuentran las neuronas de interés para el EEG, que son las piramidales. 

<p align="center">
  <img src="Multimedia/Neuronas%20piramidales%20en%20corteza%20cerebral.png" alt="Neuronas" width="400"/><br>
  <em>Figura 1. Ubicación de neuronas piramidales en corteza cerebral. Adaptado de: 
  <a href="https://www.kenhub.com/en/library/anatomy/cortical-cytoarchitecture">Kenhub (2025)</a>
  </em>
</p>

El EEG refleja principalmente la actividad dendrítica de las neuronas piramidales orientadas perpendicularmente a la superficie cortical. Al activarse en modo sincrónico, que producen dipolos eléctricos capaces de transmitirse hasta el cuero cabelludo [1]. 

<p align="center">
  <img src="Multimedia/location%20of%20neurons.jpg" alt="Location of neurons" width="400"/><br>
  <em>Figura 2. Localización de neuronas en la corteza cerebral. Recuperado de: 
  <a href="https://www.researchgate.net/publication/317390321_Single-axon_level_morphological_analysis_of_corticofugal_projection_neurons_in_mouse_barrel_field/figures?lo=1">ResearchGate</a>
  </em>
</p>

Estas señales están de muy baja amplitud (10–100 µV) y requieren la activación simultánea de enormes poblaciones neuronales para que sean trasmisibles [1]. Además, no solo factor del estado fisiológico (estado de alerta, edad) sino del entorno (ruido eléctrico) incidirán en la calidad de la señal. En años ulteriores, reinterpretaciones han relevado cómo el modelado informático y la utilización de redes neuronales ayudan a entender mejor la dinámica de las señales del cortex en aplicaciones de BCI.

### 1.2 Bandas y reactividad alfa (EO vs EC)

Las oscilaciones EEG se agrupan en bandas de frecuencia asociadas a estados mentales:

<p align="center">
  <img src="Multimedia/waveforms.jpg" alt="EEG Waveforms" width="400"/><br>
  <em>Figura 3. Ondas cerebrales registradas en EEG. Recuperado de: 
  <a href="https://www.sciencedirect.com/topics/agricultural-and-biological-sciences/brain-waves">ScienceDirect</a>
  </em>
</p>

Delta (0.5–4 Hz): sueño profundo.

Theta (4–8 Hz): somnolencia y meditación.

Alfa (8–13 Hz): relajación y atención pasiva.

Beta (13–30 Hz): actividad cognitiva y alerta.

Gamma (>30 Hz): integración sensorial y procesos de conciencia.

La banda alfa mide el reflejo de reactividad al estado ocular: aumento con ojos cerrados (EC) y disminución con ojos abiertos (EO) como testimonio de bloqueo de procesamiento visual. Esta reactividad alfa se ha usado como biomarcador de integridad funcional y de estado del estado de la relajación [2].

### 1.3 Sistema 10–20, Fp1/Fp2 y artefactos oculares

El sistema internacional 10–20 asegura estandarización en la colocación de electrodos, permitiendo la comparabilidad entre estudios. Las posiciones Fp1 y Fp2, ubicadas en la región frontal, son sensibles a artefactos oculares, como parpadeos y movimientos sacádicos, que pueden superar en amplitud a la señal cerebral. Para mitigar estos artefactos se aplican algoritmos de Independent Component Analysis (ICA) y enfoques basados en atención profunda y redes neuronales que logran una supresión más efectiva conservando las señales neuronales [3], [4].

<p align="center">
  <img src="Multimedia/posicionamiento%2010%2020.jpg" alt="Sistema internacional 10-20" width="400"/><br>
  <em>Figura 4. Sistema internacional 10-20 para posicionamiento de electrodos en EEG. Recuperado de: 
  <a href="https://www.researchgate.net/publication/328629992_Desarrollo_de_una_BCI_utilizando_el_potencial_P300_y_la_diadema_MindwaveR/figures?lo=1">ResearchGate</a>
  </em>
</p>

### 1.4 Electrodos: húmedos vs secos

Los electrodos húmedos de Ag/AgCl con gel conductor continúan siendo el estándar clínico por su baja impedancia y fidelidad en la captura de señales, aunque requieren preparación y mantenimiento, lo que limita su portabilidad [4]. Los electrodos secos han evolucionado usando materiales conductores flexibles y estructuras multipin, alcanzando así un desempeño comparable al de los húmedos en muchos escenarios. Estas innovaciones permiten aplicaciones portátiles y de larga duración en EEG móvil y monitoreo continuo [4], [5].

### 1.5 Muestreo, referencia y filtrado

La frecuencia de muestreo debe respetar el teorema de Nyquist, siendo habituales 256, 512 o 1024 Hz para capturar adecuadamente bandas de hasta 40–50 Hz [1]. La elección del electrodo de referencia, pudiendo ser mastoidales, Cz o promedio común, va a condicionar la topografía y también la amplitud de las señales. El filtrado digital constituye un paso crítico en el preprocesamiento:

- Pasabanda (0.5–45 Hz): elimina deriva y ruido de alta frecuencia.
- Notch (50/60 Hz): suprime la interferencia eléctrica de la red.
- Filtros adaptativos: corrigen artefactos dinámicos (p. ej., EOG o ECG).

Recientemente se han desarrollado métodos de aprendizaje profundo para la eliminación de artefactos que mejoran la relación señal/ruido frente a los filtros clásicos [6].

---

## 2. Objetivos

### 2.1 Objetivo general
Registrar, procesar y analizar señales EEG mediante el uso del sistema BITalino (r)evolution y el software OpenSignals, con el fin de comprender la dinámica de las bandas cerebrales bajo diferentes condiciones (reposo, tarea cognitiva y artefactos controlados) y aplicar técnicas de filtrado y cuantificación espectral para su interpretación.

### 2.2 Objetivos específicos
- Montar y configurar un BITalino (r)evolution Board Kit BLE/BT para registrar señales EEG.
- Identificar las ubicaciones Fp1, Fp2 y O2 del sistema internacional 10‑20 y colocar electrodos correctamente.
- Adquirir segmentos EEG en condiciones: basal (ojos abiertos/cerrados), tarea cognitiva y artefactos controlados.
- Aplicar filtro band‑pass 0.8–48 Hz y reconocer los ritmos δ, θ, α, β.
- Exportar los datos y generar un informe breve con hallazgos cuantitativos.

---

## 🛠️ 3. Materiales e Instrumentos
## 🧰 Descripción de materiales

| Ítem                                   | BITalino (r)evolution Board Kit BLE/BT | Laptop con Bluetooth 4.0+          | Software OpenSignals (r)evolution | Electrodos Ag/AgCl desechables (gel) | Ultracortex Mark IV (headset seco) |
|----------------------------------------|-----------------------------------------|------------------------------------|-----------------------------------|---------------------------------------|------------------------------------|
| **Función principal**                  | Módulo de adquisición de biosenales     | Procesamiento y visualización      | Registro y análisis de señales    | Registro de señal EEG                 | Registro con electrodos secos       |
| **Detalles técnicos**                  | Entradas: ECG, EMG, EEG, EDA            | Software *OpenSignals* + Python    | Compatible con BITalino           | Sensores de un solo uso               | Electrodos activos, portátil        |
| **Cantidad por grupo**                 | 1                                       | 1                                  | -                                 | 3                                     | Rotativo (demo)                     |

<p align="center">
  <img src="Multimedia/bitalino.png" alt="BITalino Board" width="400"/><br>
  <em>Figura 5. Setup para la adquisición de señales EEG.</em>
</p>
---

## 🔍 4. Metodología

### 4.1 Preparación del software
- Se instaló el programa **OpenSignals (r)evolution**, compatible con el sistema BITalino, en la laptop 
- Se emparejó el **BITalino (r)evolution Board Kit BLE/BT** mediante Bluetooth
- Se configuró el canal **A4 como EEG** y se definió una **frecuencia de muestreo de 1000 Hz**, lo que asegura cubrir la banda de interés (0.5–48 Hz).  
- Se verificó que el nivel de batería del dispositivo fuera superior al 30 % antes de iniciar la sesión.

### 4.2 Montaje de electrodos
- Se seleccionaron las posiciones **Fp1, Fp2 y mastoide derecha**, siguiendo el sistema internacional **10–20**.  
- Conexión realizada:  
  - **Canal EEG → Fp1**  
  - **GND → Fp2**  
  - **Referencia → mastoide derecha**  
- Previa colocación, se limpió la piel con una papel y alcohol para limpiarla.
- Se usaron audífonos para evitar interferencias con sonidos, se posicionó al voluntario mirando hacia dónde no recibiera luz directa, debido a el espacio del laboratorio el área más próxima fue cercana a la puerta.
- Cuando la tarea solicitaba tener los ojos cerrados, se le solicitó al voluntario que los cierre, debido a que no se contaba con ningún dispositivo adicional no se lo pudo tapar de mejor manera los ojos.

<p align="center">
  <img src="Multimedia/posicion%20de%20electrodos.png" alt="Posición de electrodos EEG" width="400"/><br>
  <em>Figura 6. Colocación de electrodos en posiciones Fp1, Fp2 y mastoide.</em>
</p>

### 4.3 Secuencia experimental
El registro de señales se llevó a cabo siguiendo diferentes condiciones, cada una con una duración aproximada de 1–2 minutos:

| Condición                | Descripción                                                                 | Video                                     |
|---------------------------|-----------------------------------------------------------------------------|-------------------------------------------|
| **Basal – ojos abiertos** | Participante fijó la vista en un punto frente a él, evitando movimientos bruscos. | *(No disponible)*                          |
| **Basal – ojos cerrados** | Participante mantuvo los ojos cerrados en reposo.                           | [🎥 Ver video](Multimedia/PRUEBA%202.mp4) |
| **Tarea cognitiva**       | Ejecución de restas sucesivas desde 100 en intervalos de 7 (100, 93, 86, …). | [🎥 Ver video](Multimedia/PRUEBA%203.mp4) |
| **Artefactos controlados**| Se realizaron parpadeos voluntarios cada ~2 segundos y luego masticando.    | [🎥 Ver video](Multimedia/PRUEBA%204.mp4) |
| **Condición libre**       | El participante escuchó música clásica, luego rock y por último ondas alfa. | [🎥 Ver video](Multimedia/PRUEBA%205.mp4) |


---

## 📊 5. Resultados

### 5.1 Repositorio de vídeos

| Condición                | Archivo de vídeo     | Enlace                                                  |
|---------------------------|----------------------|---------------------------------------------------------|
| **Basal – ojos abiertos** | *(No disponible)*    | -                                                       |
| **Basal – ojos cerrados** | PRUEBA 2.mp4         | [🎥 Ver video](Multimedia/PRUEBA%202.mp4)               |
| **Tarea cognitiva**       | PRUEBA 3.mp4         | [🎥 Ver video](Multimedia/PRUEBA%203.mp4)               |
| **Artefactos controlados**| PRUEBA 4.mp4         | [🎥 Ver video](Multimedia/PRUEBA%204.mp4)               |
| **Condición libre**       | PRUEBA 5.mp4         | [🎥 Ver video](Multimedia/PRUEBA%205.mp4)               |

### 5.2 Gráficas obtenidas

#### 5.2.1 Señales EEG crudas y filtradas durante reposo (ojos cerrados) y fijación visual (ojos abiertos)
*(Descripción + figuras)*

#### 5.2.2 Densidad espectral de potencia (PSD) de EEG
*(Descripción + figuras)*

#### 5.2.3 Potencia relativa (%) por banda
*(Descripción + gráficas comparativas)*

#### 5.2.4 Comparación de potencia α: ojos cerrados vs ojos abiertos
*(Descripción + gráficas)*

#### 5.2.5 Tarea cognitiva: Resta 100-7
*(Descripción + gráficas de la tarea)*

#### 5.2.6 Comparación de potencia β durante tarea cognitiva
*(Descripción + resultados estadísticos)*

#### 5.2.7 Detección de parpadeos
*(Conteo y gráficas de artefactos detectados)*

---

## 💭 6. Discusión e interpretación

### 6.1 Señales crudas vs. filtradas (0.8–48 Hz + notch)
*(Discusión breve)*

### 6.2 PSD por grabación
*(Discusión breve)*

### 6.3 Potencia relativa por banda (Δ, θ, α, β, γ)
*(Discusión breve)*

### 6.4 Comparación de α (8–13 Hz): Ojos cerrados (EC) vs. Ojos abiertos (EO)
*(Discusión breve)*

### 6.5 Tarea cognitiva (resta 100–7) y comparación en β (13–30 Hz)
*(Discusión breve)*

### 6.6 Detección de parpadeos (EOG) en frontal
*(Discusión breve)*

### 6.7 Actividad cognitiva libre: Escuchar música
*(Discusión breve)*

---

## 🚫⚠️ 7. Limitaciones y mejoras
*(Lista de limitaciones encontradas y propuestas de mejora.)*

---

## 📰 8. Conclusiones
*(Síntesis de logros y hallazgos principales.)*

---

## 9. Referencias

1. U. Salahuddin y P.-X. Gao, “Signal Generation, Acquisition, and Processing in Brain Machine Interfaces: A Unified Review,” *Frontiers in Neuroscience*, vol. 15, 2021. [En línea]. Disponible en: [https://www.frontiersin.org/articles/10.3389/fnins.2021.728178/full](https://www.frontiersin.org/articles/10.3389/fnins.2021.728178/full)  

2. O. M. Bazanova y D. Vernon, “Interpreting EEG alpha activity,” *Frontiers in Human Neuroscience*, vol. 14, p. 594, 2020. [En línea]. Disponible en: [https://www.frontiersin.org/articles/10.3389/fnhum.2020.594/full](https://www.frontiersin.org/articles/10.3389/fnhum.2020.594/full)  

3. A. Delorme *et al.*, “Enhanced ICA-based artifact removal for EEG,” *NeuroImage*, vol. 209, p. 116506, 2020. [En línea]. Disponible en: [https://www.sciencedirect.com/science/article/pii/S1053811920302418](https://www.sciencedirect.com/science/article/pii/S1053811920302418)  

4. Y. M. Chi *et al.*, “Dry EEG electrodes for mobile and wireless systems,” *IEEE Transactions on Biomedical Engineering*, vol. 67, no. 5, pp. 1398–1405, mayo 2020. [En línea]. Disponible en: [https://ieeexplore.ieee.org/document/8953212](https://ieeexplore.ieee.org/document/8953212)  

5. A. Mahajan *et al.*, “Flexible Dry Electrodes for Long-Term EEG Monitoring,” *Sensors*, vol. 21, no. 3, p. 987, 2021. [En línea]. Disponible en: [https://www.mdpi.com/1424-8220/21/3/987](https://www.mdpi.com/1424-8220/21/3/987)  

6. R. Jiang *et al.*, “A novel EEG artifact removal algorithm based on an advanced attention mechanism,” *Scientific Reports*, vol. 15, art. 19419, 2025. [En línea]. Disponible en: [https://www.nature.com/articles/s41598-025-98653-1](https://www.nature.com/articles/s41598-025-98653-1)  


