# Laboratorio N° 4 – Uso de BiTalino para ECG 🫀
---
# Índice  

1. [Introducción](#-introducción)  
2. [Objetivos](#-objetivos)  
3. [Descripción de materiales](#-descripción-de-materiales)  
4. [Metodología](#-metodología)  
   - [Preparación del equipo](#-preparación-del-equipo)  
   - [Preparación del sujeto](#-preparación-del-sujeto)  
   - [Configuración de electrodos](#-configuración-de-electrodos)  
   - [Registro de la señal ECG](#-registro-de-la-señal-ecg)  
   - [Procesamiento inicial](#-procesamiento-inicial)  
5. [Resultados](#-resultados)  
   - [Videos](#videos)  
   - [Señal ECG no filtrada](#señal-ecg-no-filtrada)  
   - [Señal ECG derivada 1](#señal-ecg-derivada-1)  
   - [Señal ECG derivada 2](#señal-ecg-derivada-2)  
   - [Señal ECG posterior a ejercicio](#señal-ecg-posterior-a-ejercicio)  
   - [Códigos](#-códigos)  
6. [Discusión de resultados](#-discusión-de-resultados)  
   - [Señal ECG en estado de reposo: derivadas 1 y 2](#señal-ecg-en-estado-de-reposo-derivadas-1-y-2)  
   - [Señal ECG en estado de apnea: derivadas 1 y 2](#señal-ecg-en-estado-de-apnea-derivadas-1-y-2)  
   - [Señal ECG posterior a ejercicio: derivadas 1 y 2](#señal-ecg-posterior-a-ejercicio-derivadas-1-y-2)  
7. [Referencias](#-referencias)  

## Introducción  

El electrocardiograma (ECG) es una técnica diagnóstica no invasiva que registra la actividad eléctrica del corazón mediante electrodos colocados en la superficie de la piel. La señal está conformada por componentes como la onda P, el complejo QRS y la onda T, que reflejan la despolarización y repolarización de aurículas y ventrículos. Su interpretación es fundamental para la detección de arritmias, bloqueos, isquemias y otras alteraciones cardiovasculares [1]. Además, el ECG continúa siendo la herramienta de referencia en electrofisiología cardíaca, ya que proporciona una resolución temporal inigualable para estudiar los eventos eléctricos del corazón [2]. En el ámbito educativo, el análisis de esta señal permite a los estudiantes aplicar los principios de la bioinstrumentación y del procesamiento digital de señales biomédicas en escenarios prácticos.  

En este contexto, el dispositivo BiTalino (r)evolution se ha consolidado como una plataforma modular, de bajo costo y gran portabilidad, diseñada para la adquisición de biosenales como ECG, EMG o EDA en tiempo real. Diversos estudios han validado su desempeño en comparación con equipos de referencia, demostrando que BITalino puede registrar señales ECG con una precisión suficiente para entornos de docencia e investigación [3], [4]. Su arquitectura abierta, la comunicación inalámbrica vía Bluetooth y la compatibilidad con software como *OpenSignals* facilitan la adquisición y análisis de señales fisiológicas, ofreciendo a los estudiantes la posibilidad de trabajar desde la correcta colocación de electrodos hasta la aplicación de técnicas de filtrado, segmentación y análisis de variabilidad cardíaca, consolidando así su aprendizaje en instrumentación biomédica moderna [5].  

---
## Objetivos  

- **Adquirir señales biomédicas de ECG**, comprendiendo el proceso de registro de la actividad eléctrica del corazón mediante el uso de electrodos y el dispositivo BiTalino.  
- **Configurar adecuadamente el sistema BiTalino**, asegurando la correcta conexión de sus componentes y la vinculación con el software *OpenSignals (r)evolution* para la captura de datos.  
- **Extraer y analizar la información de las señales ECG** registradas, empleando las herramientas del software para visualizar la señal y reconocer sus características principales.  

---

## Descripción de materiales  

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

## Metodología  

La práctica se desarrolló siguiendo una secuencia de pasos que garantizan la correcta adquisición de la señal ECG mediante el sistema BiTalino (r)evolution y el software OpenSignals (r)evolution. A continuación, se detallan las fases principales del procedimiento:  


### Preparación del equipo  
1. Se verificó el estado físico del módulo BiTalino, cables y electrodos, asegurando la ausencia de daños visibles en conectores o recubrimientos.  
2. Se conectó la batería LiPo 3.7V–500mA al BiTalino y se activó la comunicación Bluetooth entre el dispositivo y la laptop, según las recomendaciones de la guía de laboratorio.  
3. En la computadora, se instaló y configuró el software OpenSignals (r)evolution, necesario para la visualización y almacenamiento de la señal adquirida.  



### Preparación del sujeto  
1. Se seleccionó un voluntario sano, sin antecedentes de patologías cardiovasculares.  
2. Antes de colocar los electrodos, se realizó la limpieza de la piel en los puntos de contacto, con el fin de reducir la impedancia cutánea y mejorar la calidad de la señal.  
3. Se dispusieron los electrodos de superficie siguiendo las derivaciones estándar de Einthoven, adaptadas al BiTalino.  



### Configuración de electrodos  
- Se emplearon tres electrodos externos (positivo, negativo y referencia) conectados al canal analógico A2 del BiTalino.  
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


### Registro de la señal ECG  

1. **Condiciones de reposo y apnea:**  
   - El sujeto permaneció en reposo durante 30 s de registro.  
   - Posteriormente realizó apnea voluntaria de 30 s, seguida de 1 minuto de recuperación.  
   - Este procedimiento se repitió tres veces consecutivas para la primera derivación y luego nuevamente con la segunda derivación.  

2. **Condición post-ejercicio:**  
   - El voluntario realizó actividad aeróbica (correr) durante 15 minutos.  
   - Se registró la señal ECG en dos configuraciones:  
     - 1 minuto con la primera derivación.  
     - 1 minuto con la segunda derivación.  

3. **Documentación:**  
   - Cada adquisición se acompañó de la visualización en tiempo real de la señal en OpenSignals.  
   - Se grabaron fotografías y videos como respaldo de la práctica experimental.  

### Procesamiento inicial  

1. Los datos fueron exportados desde OpenSignals (r)evolution en dos formatos:  
   - **.h5 (HDF5):** compatible con Python y librerías como `h5py` o `pandas`.  
   - **.txt:** archivo delimitado en texto plano, útil para carga rápida y visualización simple.  

2. En los archivos, la señal de ECG se encuentra en el canal A2, mientras que las demás columnas incluyen:  
   - `nSeq` → número de secuencia (contador interno).  
   - `I1`, `I2` → entradas digitales.  
   - `O1`, `O2` → salidas digitales.  
   - `A2` → canal analógico de ECG.  

3. Se cargaron los datos en Python utilizando `h5py`, `numpy` y `pandas`.  

4. Se realizó la conversión de los valores del ADC a voltios, aplicando la fórmula:  

   `V = (ADC / (2^n - 1)) * Vref`  

   Donde:  
   - `n = 10 bits` (resolución del ADC del BiTalino).  
   - `Vref = 3.3 V` (voltaje de referencia).  

   Resultando:  

   `V = (ADC / 1023) * 3.3`  

5. Se consideró el offset ≈ 512, correspondiente a ~1.65 V (la mitad de 3.3 V). Este valor centra la señal en el rango del ADC, permitiendo representar tanto potenciales positivos como negativos. Para el análisis, se restó este offset, lo que permitió visualizar la señal ECG alrededor de 0 V.  

6. La señal fue procesada con un filtro pasa-banda Butterworth (0.5–40 Hz) para eliminar ruido de baja frecuencia y artefactos de alta frecuencia.  

7. Se implementó la detección de picos R usando la función `find_peaks` de `scipy.signal`, con:  
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

## Resultados  

### Videos  
En esta sección se presentan los registros audiovisuales obtenidos durante la práctica experimental:  

- [▶️ Prueba 1 – Apnea (30 s + recuperación)](Multimedia/Prueba%201%20apnea%20video.mp4)  
- [▶️ Prueba 2 – Ejercicio (post-actividad aeróbica)](Multimedia/Prueba%201%20video.mp4)  


### Señal ECG no filtrada

<p align="center">
  <img src="Multimedia/Se%C3%B1al%20ECG%20sin%20filtrar%20en%20reposo%20y%20Apnea%20respiratoria.png" alt="Señal ECG sin filtrar" width="3000"/>
</p>  
Figura 3. Señal ECG sin filtrar en reposo y apnea respiratoria.  

### Señal ECG derivada 1

<p align="center">
  <img src="Multimedia/Se%C3%B1al%20ECG%20en%20Reposo%20y%20en%20Apnea%20respiratoria_%20Derivada%201.png" alt="Señal ECG en reposo y apnea - derivada I" width="3000"/>
</p>  
Figura 4. Señal ECG en reposo y durante apnea respiratoria en derivada I.  

### Señal ECG derivada 2

<p align="center">
  <img src="Multimedia/Se%C3%B1al%20ECG%20en%20Reposo%20y%20en%20Apnea%20respiratoria_%20Derivada%202.png" alt="Señal ECG en reposo y apnea - derivada II" width="3000"/>
</p>  
Figura 5. Señal ECG en reposo y durante apnea respiratoria en derivada II.  

### Datos obtenidos de las mediciones
<p align="center">
  <img src="Multimedia/datos%20adicionales.png" alt="Señal ECG post ejercicio" width="1000"/>
</p>  
Figura 6. Datos para analisis luego de apneas

### Señal ECG posterior a ejercicio
<p align="center">
  <img src="Multimedia/Se%C3%B1al%20ECG%20Post%20ejercicio.png" alt="Señal ECG post ejercicio" width="1000"/>
</p>  
Figura 7. Señal ECG post-ejercicio aeróbico.  


### 📂 Códigos

El desarrollo completo del procesamiento y análisis de señales se encuentra documentado en:  
- [📓 Laboratorio_4_Codes.ipynb](Laboratorio_4_Codes.ipynb)


---

## Discusión de resultados

En esta sección se analizan e interpretan las señales ECG obtenidas en diferentes condiciones fisiológicas (reposo, apnea y post-ejercicio), registradas con el sistema BiTalino en derivaciones I y II. El objetivo es comparar amplitudes, frecuencias y morfología de las ondas para comprender los efectos de cada situación sobre la actividad eléctrica del corazón.

### Señal ECG en estado de reposo: derivadas 1 y 2
Podemos ver que la amplitud de la señal en general es mayor en la derivación II que en la I.  
Como el eje eléctrico del corazón se alinea bastante bien con el eje de la derivación II, los potenciales se proyectan más intensamente en II que en I, dando mayores picos R (mayor amplitud de QRS) en derivación II [6].  

En la derivada II se aprecia mejor los intervalos QRS y parcialmente el T. En la derivada I, la señal no se pudo captar correctamente por un problema con electrodos. A pesar de eso, se aprecia el segmento R.  

### Señal ECG en estado de Apnea: derivadas 1 y 2
En la derivación I, durante el periodo de apnea (contención voluntaria de la respiración) registrado en la derivación I del ECG, se observa una disminución general en la amplitud de las ondas R junto con una ligera irregularidad en el intervalo entre complejos, lo que puede indicar una modulación autonómica sobre la actividad cardíaca. La apnea genera un aumento progresivo de la presión intratorácica negativa y de la actividad parasimpática, lo que tiende a reducir la frecuencia cardíaca (bradicardia refleja) y puede alterar la morfología del ECG, en especial disminuyendo la amplitud de las ondas por cambios en el retorno venoso y el volumen sistólico. Estos efectos han sido documentados en estudios que muestran una reducción de la amplitud del QRS y de la frecuencia cardíaca durante apnea voluntaria, especialmente en registros de derivaciones de miembros como la I.  

El registro del ECG en derivación II se muestra un ritmo sinusal regular con ondas R bien definidas, complejos QRS estrechos y sin evidencia de arritmias o alteraciones en la repolarización, lo que corresponde al patrón esperado en un corazón sano en reposo. Estos hallazgos son coherentes con la definición de ritmo sinusal normal, caracterizado por intervalos regulares y complejos QRS bien delimitados [7]. Además, estudios recientes han documentado que durante apneas prolongadas pueden aparecer bradicardia marcada y arritmias, mientras que en fases iniciales o en apneas cortas, la actividad eléctrica se mantiene estable [8], [9]. De igual forma, investigaciones han mostrado que la repolarización ventricular puede alterarse con la apnea sostenida, aunque en condiciones basales permanece sin cambios significativos [10]. En conjunto, estos reportes respaldan que el trazado presentado refleja un estado normal previo a los efectos fisiológicos de la apnea.  

Ya para ambas derivaciones, las últimas señales en el tiempo se aprecian parecidas a las de estado de reposo pues ya se pasó por la etapa de apnea y se está recuperando el estado basal.  

### Señal ECG posterior a ejercicio: derivadas 1 y 2
El análisis de los registros post-ejercicio en derivaciones I y II muestra un incremento evidente en la frecuencia cardíaca respecto al estado basal, reflejado en la mayor densidad de complejos QRS por unidad de tiempo y en la reducción de los intervalos RR. Esta respuesta corresponde a la adaptación fisiológica normal del sistema cardiovascular frente al ejercicio aeróbico, donde el aumento de la demanda metabólica se acompaña de un incremento del gasto cardíaco y de la actividad simpática [11]. A su vez, los complejos QRS mantienen una morfología estable, con ondas R bien definidas y sin evidencia de arritmias, lo que es congruente con la adaptación de un corazón sano a la actividad física [12].

Por otro lado, la señal muestra mayor variabilidad en la línea de base, en especial en la derivación I, fenómeno que puede atribuirse tanto al aumento del tono simpático como a artefactos de movimiento y respiración posteriores al esfuerzo [13].

---
### Referencias 
[1] Mayo Clinic, “Electrocardiogram (ECG or EKG),” *Mayo Clinic*, 2023. [En línea]. Disponible en: https://www.mayoclinic.org/tests-procedures/ekg/about/pac-20384983  
[2] L. Sörnmo y P. Laguna, *Bioelectrical Signal Processing in Cardiac and Neurological Applications*, 2.ª ed. Academic Press, 2020.  
[3] A. Guerreiro, A. Lourenço, F. Canento, R. P. P. Lopes, H. Silva y A. Fred, “BITalino: A Multimodal Platform for Physiological Computing,” en *Proc. Int. Conf. Physiological Computing Systems (PhyCS)*, 2013, pp. 246–253.  
[4] S. Krachunov, J. Fafoutis y R. Piechocki, “Benchmarking BITalino against a Reference System for Physiological Sensing,” *IEEE Sensors Journal*, vol. 19, no. 22, pp. 10620–10627, nov. 2019. doi: 10.1109/JSEN.2019.2932777  
[5] C. Oliveira et al., “Validation of a Low-Cost Electrocardiography (ECG) Toolkit: BITalino vs BrainAmp ExG,” *Sensors*, vol. 21, no. 13, p. 4485, jul. 2021. doi: 10.3390/s21134485  
[6] J. E. Hall y A. C. Guyton, *Tratado de fisiología médica*, 14.ª ed. Barcelona, España: Elsevier, 2021, cap. 11.  
[7] LITFL, “Normal Sinus Rhythm • ECG Library Basics,” 2023. [En línea]. Disponible en: https://litfl.com/normal-sinus-rhythm-ecg-library/  
[8] K. Kjeld et al., “Extreme Hypoxia Causing Brady-Arrythmias During Apnea in Elite Breath-Hold Divers,” *Front. Physiol.*, vol. 12, 2021. [En línea]. Disponible en: https://www.frontiersin.org/articles/10.3389/fphys.2021.712573/full  
[9] C. Bouten et al., “Heart Rate and Muscle Oxygenation Kinetics During Short Dynamic Apnea and Face Immersed Apnea,” *Front. Physiol.*, vol. 12, 2021. [En línea]. Disponible en: https://pmc.ncbi.nlm.nih.gov/articles/PMC8339880/  
[10] A. N. Research Group, “Cardiovascular Response to Breath-Holding Explained by Changes of the Indices and their Dynamic Interactions,” *Int. J. Cardiovasc. Res.*, 2020. [En línea]. Disponible en: https://www.iomcworld.com/open-access/cardiovascular-response-to-breathholding-explained-by-changes-of-the-indices-and-their-dynamic-interactions-13437.html  
[11] L. Brockmann, H. Wang y K. J. Hunt, “Heart rate variability changes with respect to time and exercise intensity during heart-rate-controlled steady-state treadmill running,” *Sci. Rep.*, vol. 13, no. 8515, 2023. [En línea]. Disponible en: https://www.nature.com/articles/s41598-023-35717-0  
[12] L. Kocsis, A. Kocsis y M. Tóth, “Exercise-Induced Electrocardiographic Changes in Healthy Young Adults: Effects During Peak Exercise and Recovery,” *Diagnostics*, vol. 14, no. 4, p. 377, 2024. [En línea]. Disponible en: https://pmc.ncbi.nlm.nih.gov/articles/PMC11119175/  
[13] A. Y. K. Wong et al., “Exercise-induced changes in heart rate variability and cardiac autonomic regulation: A systematic review,” *Front. Physiol.*, vol. 14, 2023. [En línea]. Disponible en: https://www.frontiersin.org/articles/10.3389/fphys.2023.1166684/full  
