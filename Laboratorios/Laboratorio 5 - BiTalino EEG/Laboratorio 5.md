# 🧠📉 LABORATORIO 4: Uso de BiTalino para adquisición de señales EEG

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

1.1 Generación de la señal EEG

La corteza cerebral es la capa más externa del encéfalo, formada por sustancia gris con un grosor de 2 a 4 mm. Está organizada en seis capas histológicas que contienen diferentes tipos de neuronas y conexiones, siendo que en las capas III y V dónde se encuentran las neuronas de interés para el EEG, que son las piramidales. 

<p align="center">
  <img src="Multimedia/Neuronas.png" alt="Neuronas" width="400"/><br>
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


1.2 Bandas y reactividad alfa (EO vs EC)

Las oscilaciones EEG se agrupan en bandas de frecuencia asociadas a estados mentales:

Delta (0.5–4 Hz): sueño profundo.

Theta (4–8 Hz): somnolencia y meditación.

Alfa (8–13 Hz): relajación y atención pasiva.

Beta (13–30 Hz): actividad cognitiva y alerta.

Gamma (>30 Hz): integración sensorial y procesos de conciencia.

La banda alfa muestra una marcada reactividad al estado ocular: aumenta con ojos cerrados (EC) y disminuye con ojos abiertos (EO), reflejando un bloqueo por procesamiento visual. Esta reactividad alfa se ha consolidado como un biomarcador de integridad funcional y de estados de relajación [2].

1.3 Sistema 10–20, Fp1/Fp2 y artefactos oculares

El sistema internacional 10–20 asegura estandarización en la colocación de electrodos, permitiendo comparabilidad entre estudios. Las posiciones Fp1 y Fp2, ubicadas en la región frontal, son sensibles a artefactos oculares, como parpadeos y movimientos sacádicos, que pueden superar en amplitud a la señal cerebral (hasta 200 µV). Para mitigar estos artefactos se aplican algoritmos de Independent Component Analysis (ICA) y, más recientemente, enfoques basados en atención profunda y redes neuronales que logran una supresión más efectiva conservando las señales neuronales [3], [4].

1.4 Electrodos: húmedos vs secos

Los electrodos húmedos de Ag/AgCl con gel conductor continúan siendo el estándar clínico por su baja impedancia y fidelidad en la captura de señales, aunque requieren preparación y mantenimiento, lo que limita su portabilidad [4]. En contraste, los electrodos secos han evolucionado en los últimos años con el uso de materiales conductores flexibles y estructuras multipin, alcanzando un desempeño comparable al de los húmedos en muchos escenarios. Estas innovaciones permiten aplicaciones portátiles y de larga duración en EEG móvil y monitoreo continuo [4], [5].

1.5 Muestreo, referencia y filtrado

La frecuencia de muestreo debe respetar el teorema de Nyquist, siendo habituales 256, 512 o 1024 Hz para capturar adecuadamente bandas de hasta 40–50 Hz [1]. La elección del electrodo de referencia (mastoidales, Cz o promedio común) condiciona la topografía y amplitud de las señales. El filtrado digital constituye un paso crítico en el preprocesamiento:

Pasabanda (0.5–45 Hz): elimina deriva y ruido de alta frecuencia.

Notch (50/60 Hz): suprime la interferencia eléctrica de la red.

Filtros adaptativos: corrigen artefactos dinámicos (p. ej., EOG o ECG).

Recientemente se han desarrollado métodos de aprendizaje profundo para la eliminación de artefactos que mejoran la relación señal/ruido frente a los filtros clásicos [6].

---

## 2. Objetivos

### 2.1 Objetivo general
*(Texto del objetivo general.)*

### 2.2 Objetivos específicos
*(Lista de objetivos específicos.)*

---

## 🛠️ 3. Materiales e Instrumentos
*(Tabla con ítems, descripción y cantidad.)*

---

## 🔍 4. Metodología

### 4.1 Preparación del software
*(Pasos de instalación y configuración.)*

### 4.2 Montaje de electrodos
*(Ubicación y conexiones según sistema 10–20.)*

### 4.3 Secuencia experimental
*(Tabla con condiciones y tiempos.)*

### 4.4 Ejercicios de análisis
*(Lista de análisis solicitados: PSD, comparación α/β, parpadeos, etc.)*

---

## 📊 5. Resultados

### 5.1 Repositorio de vídeos
*(Enlaces o referencias a videos del registro experimental.)*

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

## 👥 9. Aporte de los integrantes

| Integrante | Contribución (%) |
|------------|:----------------:|
| Nombre 1   | 33.3% |
| Nombre 2   | 33.3% |
| Nombre 3   | 33.3% |

