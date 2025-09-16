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


---

## 📝 Metodología  

La práctica se desarrolló siguiendo una secuencia de pasos que garantizan la correcta adquisición de la señal ECG mediante el sistema **BiTalino (r)evolution** y el software *OpenSignals (r)evolution*. A continuación, se detallan las fases principales del procedimiento:  

### ⚡ Preparación del equipo  
1. Se verificó el estado físico del módulo BiTalino, cables y electrodos, asegurando la ausencia de daños visibles en conectores o recubrimientos. 
2. Se conectó la batería LiPo 3.7V–500mA al BiTalino y se activó la comunicación Bluetooth entre el dispositivo y la laptop, según las recomendaciones de la guía de laboratorio, 
3. En la computadora, se instaló y configuró el software *OpenSignals (r)evolution*, necesario para la visualización y almacenamiento de la señal adquirida.  

### 👤 Preparación del sujeto  
1. Se seleccionó un voluntario sano, sin antecedentes de patologías cardiovasculares.  
2. Se procedió a limpiar la zona de la piel donde se colocarían los electrodos, con el fin de reducir el ruido por interferencias y garantizar un mejor contacto eléctrico.  
3. Se dispusieron los electrodos de superficie siguiendo la configuración estándar para ECG de derivación simple: un electrodo en cada muñeca (positivo y negativo) y uno en la región de la cresta ilíaca como referencia. 

### 📈 Registro de la señal ECG  

1. **Configuración inicial:**  
   - Se seleccionó el canal de ECG en el BiTalino y se verificó la correcta conexión Bluetooth con la laptop a través de *OpenSignals (r)evolution*.  
- Se trabajó con dos configuraciones de derivaciones:  

  - **Primera derivación:**  
    El electrodo positivo se colocó en la muñeca izquierda, el electrodo negativo en la muñeca derecha y el electrodo de referencia en la cresta ilíaca derecha. Esta configuración permite obtener una señal clara de la actividad eléctrica general del corazón en reposo.  

  - **Segunda derivación:**  
    El electrodo positivo se colocó en la pierna izquierda (región de la cresta ilíaca), el electrodo negativo en la muñeca derecha y el electrodo de referencia en la muñeca izquierda. Esta disposición facilita la observación de la onda P y del complejo QRS con mayor amplitud y estabilidad.  

2. **Condiciones de apnea y recuperación:**  
   - El sujeto realizó apnea voluntaria durante 30 segundos, seguida de 1 minuto de recuperación en reposo.  
   - Este procedimiento se repitió tres veces consecutivas para la primera derivación.  
   - Posteriormente, se cambió a la segunda derivación y se repitió el mismo proceso (tres repeticiones de apnea + recuperación).  

3. **Condición post-ejercicio:**  
   - El sujeto realizó la actividad aeróbica  de correr durante 15 minutos.  
   - Se registró la señal ECG en dos configuraciones:  
     - 1 minuto con la primera derivación.  
     - 1 minuto con la segunda derivación.  

4. **Documentación:**  
   - Cada adquisición se acompañó de la visualización en tiempo real de la señal en OpenSignals.  
   - Se grabaron fotografías y videos como respaldo de la práctica experimental.  


### 🔬 Procesamiento inicial  
1. Los archivos exportados en formato compatible fueron analizados con Python, aplicando filtrado digital básico (pasa-bajas y elimina-ruido).  
2. Se identificaron los componentes característicos de la señal (ondas P, complejo QRS, onda T), comparando sus morfologías en las distintas condiciones registradas.  

---

### 📚 Referencias 

[1] Mayo Clinic, “Electrocardiogram (ECG or EKG),” *Mayo Clinic*, 2023. [Online]. Available: https://www.mayoclinic.org/tests-procedures/ekg/about/pac-20384983  
[2] L. Sörnmo and P. Laguna, *Bioelectrical Signal Processing in Cardiac and Neurological Applications*, 2nd ed. Academic Press, 2020.  
[3] A. Guerreiro, A. Lourenço, F. Canento, R. P. P. Lopes, H. Silva, and A. Fred, “BITalino: A Multimodal Platform for Physiological Computing,” in *Proc. Int. Conf. Physiological Computing Systems (PhyCS)*, 2013, pp. 246–253.  
[4] S. Krachunov, J. Fafoutis, and R. Piechocki, “Benchmarking BITalino against a Reference System for Physiological Sensing,” *IEEE Sensors Journal*, vol. 19, no. 22, pp. 10620–10627, Nov. 2019. doi: 10.1109/JSEN.2019.2932777  
[5] C. Oliveira et al., “Validation of a Low-Cost Electrocardiography (ECG) Toolkit: BITalino vs BrainAmp ExG,” *Sensors*, vol. 21, no. 13, pp. 4485, Jul. 2021. doi: 10.3390/s21134485  

