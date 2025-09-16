# Laboratorio N° 4 – Uso de BiTalino para ECG 🫀

## 🫀 Introducción  

El **electrocardiograma (ECG)** es una técnica diagnóstica no invasiva que registra la actividad eléctrica del corazón mediante electrodos colocados en la superficie de la piel. La señal está conformada por componentes como la onda P, el complejo QRS y la onda T, que reflejan la despolarización y repolarización de aurículas y ventrículos. Su interpretación es fundamental para la detección de arritmias, bloqueos, isquemias y otras alteraciones cardiovasculares [1]. Además, el ECG continúa siendo la herramienta de referencia en electrofisiología cardíaca, ya que proporciona una resolución temporal inigualable para estudiar los eventos eléctricos del corazón [2]. En el ámbito educativo, el análisis de esta señal permite a los estudiantes aplicar los principios de la bioinstrumentación y del procesamiento digital de señales biomédicas en escenarios prácticos.  

En este contexto, el dispositivo **BiTalino (r)evolution** se ha consolidado como una plataforma modular, de bajo costo y gran portabilidad, diseñada para la adquisición de biosenales como ECG, EMG o EDA en tiempo real. Diversos estudios han validado su desempeño en comparación con equipos de referencia, demostrando que BITalino puede registrar señales ECG con una precisión suficiente para entornos de docencia e investigación [3], [4]. Su arquitectura abierta, la comunicación inalámbrica vía Bluetooth y la compatibilidad con software como *OpenSignals* facilitan la adquisición y análisis de señales fisiológicas, ofreciendo a los estudiantes la posibilidad de trabajar desde la correcta colocación de electrodos hasta la aplicación de técnicas de filtrado, segmentación y análisis de variabilidad cardíaca, consolidando así su aprendizaje en instrumentación biomédica moderna [5].  

---
## 🎯 Objetivos  

- **Adquirir señales biomédicas de ECG**, comprendiendo el proceso de registro de la actividad eléctrica del corazón mediante el uso de electrodos y el dispositivo BiTalino.  
- **Configurar adecuadamente el sistema BiTalino**, asegurando la correcta conexión de sus componentes y la vinculación con el software *OpenSignals (r)evolution* para la captura de datos.  
- **Extraer y analizar la información de las señales ECG** registradas, empleando las herramientas del software para visualizar la señal y reconocer sus características principales.  

---

## 🛠️ Descripción de materiales  

| **Ítem** | BiTalino (r)evolution | Cable para 3 electrodos | Batería LiPo 3.7V 500mA | Electrodos de superficie | Laptop |
|:---------|:-------------------------|:---------------------------|:-----------------------------|:----------------------------|:---------|
| **Función principal** | Módulo de adquisición de biosenales | Conexión de electrodos al BiTalino | Alimentación del sistema | Registro de la señal ECG | Procesamiento y visualización |
| **Detalles técnicos** | Entradas: ECG, EMG, EEG, EDA | Tipo tripolar | Recargable, portátil | Sensores desechables | Software *OpenSignals* + Python |
| **Cantidad** | 1 | 1 | 1 | 3 | 1 |

<p align="center">
  <img src="Multimedia/Configuración%20Bitalino%20EMG.png" alt="Configuración del BiTalino para EMG" width="500"/>
</p>  

**Figura 1.** Configuración del BiTalino para el registro de EMG.  

---

## 📝 Metodología  

La práctica se desarrolló siguiendo una secuencia de pasos que garantizan la correcta adquisición de la señal ECG mediante el sistema **BiTalino (r)evolution** y el software *OpenSignals (r)evolution*. A continuación, se detallan las fases principales del procedimiento:  


### ⚡ Preparación del equipo  
1. Se verificó el estado físico del módulo BiTalino, cables y electrodos, asegurando la ausencia de daños visibles en conectores o recubrimientos.  
2. Se conectó la batería LiPo 3.7V–500mA al BiTalino y se activó la comunicación Bluetooth entre el dispositivo y la laptop, según las recomendaciones de la guía de laboratorio.  
3. En la computadora, se instaló y configuró el software *OpenSignals (r)evolution*, necesario para la visualización y almacenamiento de la señal adquirida.  



### 👤 Preparación del sujeto  
1. Se seleccionó un voluntario sano, sin antecedentes de patologías cardiovasculares.  
2. Antes de colocar los electrodos, se realizó la **limpieza de la piel** en los puntos de contacto, con el fin de reducir la impedancia cutánea y mejorar la calidad de la señal.  
3. Se dispusieron los electrodos de superficie siguiendo las derivaciones estándar de Einthoven, adaptadas al BiTalino.  



### 📌 Configuración de electrodos  
- Se emplearon **tres electrodos externos** (positivo, negativo y referencia) conectados al canal analógico **A2** del BiTalino.  
- El sistema requiere dos electrodos activos (IN+ e IN–) y un electrodo de referencia (REF) que estabiliza la señal.  
- La colocación se basó en las derivadas de Einthoven:  

  - **Derivación I (Lead I):**  
    - Electrodo negativo (IN–) → brazo derecho  
    - Electrodo positivo (IN+) → brazo izquierdo  
    - Electrodo de referencia (REF) → cresta ilíaca derecha  

  - **Derivación II (Lead II):**  
    - Electrodo negativo (IN–) → brazo derecho  
    - Electrodo positivo (IN+) → cresta ilíaca derecha  
    - Electrodo de referencia (REF) → brazo izquierdo  

<p align="center">
  <img src="Multimedia/Configuracion%20ECG.png" alt="Configuración de derivaciones ECG" width="500"/>
</p>  

**Figura 2.** Configuración de electrodos en la primera (a) y segunda (b) derivación para la adquisición de señal ECG.  


### 📈 Registro de la señal ECG  

1. **Condiciones de reposo y apnea:**  
   - El sujeto permaneció en reposo durante 30 s de registro.  
   - Posteriormente realizó **apnea voluntaria de 30 s**, seguida de **1 minuto de recuperación**.  
   - Este procedimiento se repitió **tres veces consecutivas** para la primera derivación y luego nuevamente con la segunda derivación.  

2. **Condición post-ejercicio:**  
   - El voluntario realizó **actividad aeróbica (correr) durante 15 minutos**.  
   - Se registró la señal ECG en dos configuraciones:  
     - 1 minuto con la primera derivación.  
     - 1 minuto con la segunda derivación.  

3. **Documentación:**  
   - Cada adquisición se acompañó de la visualización en tiempo real de la señal en *OpenSignals*.  
   - Se grabaron fotografías y videos como respaldo de la práctica experimental.  

### 🔬 Procesamiento inicial  

1. Los datos fueron exportados desde *OpenSignals (r)evolution* en dos formatos:  
   - **.h5 (HDF5):** compatible con Python y librerías como `h5py` o `pandas`.  
   - **.txt:** archivo delimitado en texto plano, útil para carga rápida y visualización simple.  

2. En los archivos, la señal de ECG se encuentra en el canal **A2**, mientras que las demás columnas incluyen:  
   - `nSeq` → número de secuencia (contador interno).  
   - `I1`, `I2` → entradas digitales.  
   - `O1`, `O2` → salidas digitales.  
   - `A2` → canal analógico de ECG.  

3. Se cargaron los datos en **Python** utilizando `h5py`, `numpy` y `pandas`.  

4. Se realizó la **conversión de los valores del ADC a voltios**, aplicando la fórmula:  

   `V = (ADC / (2^n - 1)) * Vref`  

   Donde:  
   - `n = 10 bits` (resolución del ADC del BiTalino).  
   - `Vref = 3.3 V` (voltaje de referencia).  

   Resultando:  

   `V = (ADC / 1023) * 3.3`  

5. Se consideró el **offset ≈ 512**, correspondiente a ~1.65 V (la mitad de 3.3 V). Este valor centra la señal en el rango del ADC, permitiendo representar tanto potenciales positivos como negativos. Para el análisis, se restó este offset, lo que permitió visualizar la señal ECG alrededor de 0 V.  

6. La señal fue procesada con un **filtro pasa-banda Butterworth (0.5–40 Hz)** para eliminar ruido de baja frecuencia y artefactos de alta frecuencia.  

7. Se implementó la **detección de picos R** usando la función `find_peaks` de `scipy.signal`, con:  
   - Un **umbral dinámico** adaptado a la amplitud de la señal.  
   - Una **distancia mínima entre picos** que evita falsos positivos.  

8. A partir de los picos R se calcularon parámetros cuantitativos:  
   - **Intervalos RR**  
   - **Frecuencia cardíaca (HR)**  
   - **Variabilidad cardíaca**: SDNN y RMSSD  
   - **Amplitud media de los complejos R**  
   - **Número total de latidos detectados**  

9. Las señales se segmentaron según las condiciones fisiológicas del protocolo experimental:  
   - **Reposo**  
   - **Apnea voluntaria (30 s + 1 min de recuperación)**  
   - **Post-ejercicio (15 min de actividad aeróbica ligera)**  

10. Para cada condición, se analizó la **morfología de las ondas P, QRS y T**, así como las variaciones en amplitud y frecuencia cardíaca.  

---

## 📊 Resultados  
### Videos
En la siguiente sección se incluyen los registros audiovisuales obtenidos durante la práctica:  

- [▶️ Prueba 1 – Apnea (30 s + recuperación)](Multimedia/Prueba%201%20apnea%20video.mp4)  
- [▶️ Prueba 1 – Ejercicio (post-actividad aeróbica)](Multimedia/Prueba%201%20video.mp4)  

---
### 📚 Referencias 

[1] Mayo Clinic, “Electrocardiogram (ECG or EKG),” *Mayo Clinic*, 2023. [Online]. Available: https://www.mayoclinic.org/tests-procedures/ekg/about/pac-20384983  
[2] L. Sörnmo and P. Laguna, *Bioelectrical Signal Processing in Cardiac and Neurological Applications*, 2nd ed. Academic Press, 2020.  
[3] A. Guerreiro, A. Lourenço, F. Canento, R. P. P. Lopes, H. Silva, and A. Fred, “BITalino: A Multimodal Platform for Physiological Computing,” in *Proc. Int. Conf. Physiological Computing Systems (PhyCS)*, 2013, pp. 246–253.  
[4] S. Krachunov, J. Fafoutis, and R. Piechocki, “Benchmarking BITalino against a Reference System for Physiological Sensing,” *IEEE Sensors Journal*, vol. 19, no. 22, pp. 10620–10627, Nov. 2019. doi: 10.1109/JSEN.2019.2932777  
[5] C. Oliveira et al., “Validation of a Low-Cost Electrocardiography (ECG) Toolkit: BITalino vs BrainAmp ExG,” *Sensors*, vol. 21, no. 13, pp. 4485, Jul. 2021. doi: 10.3390/s21134485  

