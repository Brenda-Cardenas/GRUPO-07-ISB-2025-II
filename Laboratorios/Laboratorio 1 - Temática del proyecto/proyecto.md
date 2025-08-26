<h1 align="center"> Laboratorio 1 - Temática del Proyecto </h1>

## Título tentativo del proyecto
**Extracción de características de señales EMG para la detección temprana de fatiga muscular en el ámbito ocupacional**

---

## Problemática
La fatiga muscular en trabajadores de sectores con alta exigencia física y movimientos repetitivos es una problemática crítica en Perú y Latinoamérica, afectando no solo el bienestar, sino la seguridad y productividad laboral. Actualmente, la detección se basa en evaluaciones subjetivas como el dolor o el cansancio, que son poco fiables y a menudo no reflejan el estado fisiológico real del músculo. Esto resulta en diagnósticos tardíos, aumento de lesiones musculoesqueléticas y pérdidas económicas para las empresas debido a ausentismo y menor rendimiento. 

---

## Justificación
La fatiga muscular y los trastornos musculoesqueléticos representan un problema creciente en distintos sectores laborales en el Perú. 
- En estudios en Lima, se ha reportado que el 10.4% de los agentes de seguridad presentaban fatiga laboral, de los cuales el 92.3% era de tipo moderada, además de que el 36.7% sufría lesiones musculoesqueléticas, principalmente lumbalgia [1].
- De manera similar, en el Callao, se identificó que el 79.89% de los trabajadores de la industria alimentaria presentaban trastornos musculoesqueléticos (TME), siendo las zonas más afectadas la espalda (27.03%) y la muñeca derecha (26.35%) [2].
- En el ámbito hospitalario, un estudio en el Hospital Rebagliati de Lima mostró que el 93.02% del personal de limpieza reportó dolor musculoesquelético, con un 65.12% localizado en la zona lumbar, lo que refleja la alta demanda física asociada a tareas de soporte clínico [3].

Estos datos reflejan que los métodos actuales de evaluación de la fatiga muscular en el entorno laboral son principalmente subjetivos, basados en autoinformes de dolor, cansancio o incomodidad. Esto limita la posibilidad de contar con herramientas objetivas que permitan una detección temprana y una intervención más efectiva para la prevención de lesiones.

---

## Objetivos

| **Objetivos** | **Descripción** |
|---------------|-----------------|
| **Objetivo General** | Desarrollar un modelo de clasificación capaz de identificar el estado de fatiga muscular en tareas de alta repetición utilizando señales electromiográficas (EMG) como fuente principal de datos, con el propósito de prevenir lesiones en trabajadores manuales. |
| **Objetivos Específicos** | 1. Recopilar y preprocesar datos de señales EMG de bases públicas, eliminando ruidos para obtener una señal limpia. <br> 2. Extraer características relevantes de las señales EMG que indiquen el inicio y evolución de la fatiga muscular. <br> 3. Entrenar y validar un modelo de clasificación que prediga el estado de fatiga con alta precisión. <br> 4. Evaluar el rendimiento del modelo comparándolo con resultados de otros estudios o métodos existentes, asegurando la efectividad de la propuesta. |

---

## Herramientas a utilizar
- **Hardware:** Un electromiógrafo con electrodos de superficie para captar la actividad eléctrica de los músculos de forma no invasiva.  
- **Software y Entorno de Desarrollo:** Se utilizará Python en el entorno de desarrollo *Visual Studio Code*. Pues, estas herramientas ofrecen un ecosistema robusto para la programación, el análisis de datos y el desarrollo de modelos de aprendizaje automático.  
- **Procesamiento de Señales:** Se aplicarán técnicas de filtrado digital. Esto es esencial para limpiar la señal de EMG y asegurar que los datos sean confiables para el análisis posterior.  
- **Librerías de Python:**  
  - NumPy: Para la manipulación y el procesamiento numérico de las señales.  
  - Scikit-learn: Para la implementación de modelos de clasificación.  
  - TensorFlow/Keras o PyTorch: También podríamos optar por desarrollar redes neuronales, lo cual nos permitiría explorar modelos más avanzados, como las Redes Neuronales Convolucionales (CNN).  
- **Bases de Datos:** Se emplearán bases de datos de EMG de acceso público, como las de *PhysioNet* o *The Ninapro Database*, para entrenar y validar el modelo de clasificación.  

---

## Resumen del proyecto
<p align="justify">
La propuesta inicial de nuestro proyecto se centra en la detección de la fatiga muscular, un fenómeno que no siempre es perceptible y que afecta a trabajadores expuestos a labores repetitivas o de esfuerzo físico en sectores laborales. A diferencia de las evaluaciones subjetivas actuales, que se basan en la percepción del cansancio u otros malestares, este proyecto plantea una solución objetiva y no invasiva.  
Al analizar las señales EMG, las cuales reflejan la actividad eléctrica del músculo, se podrá reconocer cambios distintivos a medida que la fatiga se desarrolla.  Se realizará el procesamiento digital de señales para filtrar y limpiar los datos EMG. Posteriormente, un modelo de clasificación será entrenado utilizando bases de datos públicas para reconocer los patrones de la señal asociados a la fatiga. El objetivo final es que este modelo sea capaz de predecir el estado de fatiga de un músculo, sirviendo como una herramienta preventiva contra lesiones laborales.  
La relevancia de este proyecto radica en su impacto social y económico, ya que su aplicación en el contexto laboral permitiría mejorar la seguridad, reducir la cantidad de trabajadores que sufren lesiones y optimizar su rendimiento.
</p>

---

## Artículos académicos
| Título | Contexto | Métodos Empleados | Resultados | Relevancia Ocupacional|
|----|----|----|----|----|
| Detecting Muscle Fatigue During Lower Limb Isometric Contractions: A Machine Learning Approach [4] | El propósito del estudio fue simular posturas estáticas comunes en entornos industriales y de rehabilitación. Diez participantes realizaron contracciones isométricas controladas de los músculos de las extremidades inferiores. | Las señales EMG fueron descompuestas usando ICEEMDAN. ICEEMDAN es una técnica avanzada de descomposición de señales no lineales y no estacionarias, que mejora la precisión en la detección temprana de fatiga muscular. Se extrajeron características de los dominios de tiempo, frecuencia, tiempo-frecuencia y no lineales. | Se logró una precisión de clasificación del 99.8%. Las características no lineales lograron detectar pequeños cambios en el cansancio del músculo. ICEEMDAN ayudó a limpiar la señal EMG, separando sus partes importantes para que se puedan analizar mejor. | Tiene aplicación para los sectores de minería, agricultura y manufactura, donde es común mantener posturas estáticas durante largos periodos. Brinda una base para identificar la fatiga de manera temprana en sistemas de monitoreo en tiempo real. |
| Detection of Muscles Fatigue Through Surface EMG Signals Utilizing Machine Learning Algorithm [5] | El objetivo del estudio fue detectar fatiga muscular utilizando señales de electromiografía de superficie (sEMG) durante actividades físicas. Se recopilaron datos de dos conjuntos experimentales que incluían ejercicios dinámicos. Se buscó mejorar el análisis automático de fatiga muscular en aplicaciones médicas y de rehabilitación, con potencial para ser adaptado a entornos laborales.| Se extrajeron 14 características (8 en el dominio del tiempo, 6 en el dominio de la frecuencia); se aplicó mRMR (Minimum Redundancy Maximum Relevance), el cual selecciona las mejores características de un conjunto de datos para que un modelo de machine learning pueda clasificar con precisión si hay fatiga muscular. Se usaron SVM, LDA y KNN para la clasificación. | KNN superó a los demás con un puntaje F1 del 95.12%. Las características principales fueron la media, la asimetría y el valor absoluto medio. El modelo demostró una buena capacidad para adaptarse y funcionar correctamente en diferentes personas. | Se podría aplicar para trabajos que necesitan un control constante de la fatiga muscular, como tareas repetitivas, transporte, manufactura o construcción. Además, el uso de características simples del dominio del tiempo podría permitir que se use en wearables. |
| Assessment of Muscles Fatigue Based on Surface EMG Signals Using Machine Learning and Statistical Approaches: A Review [6]| Revisa diferentes métodos para detectar fatiga muscular usando señales EMG de superficie. Se analizan enfoques en los dominios temporal, frecuencial y tiempo-frecuencia. | Describe el flujo de procesamiento de señales (filtrado, rectificación, suavizado) y el uso de métricas como RMS, MAV, MDF, MNF, Wavelets y STFT. Se revisan modelos como SVM, redes neuronales, regresiones y árboles de decisión. | La fatiga se refleja en un aumento de la amplitud (RMS) y una disminución en la frecuencia (MDF/MNF). La combinación de características de distintos dominios mejora la precisión y la resistencia al ruido. | Permite proponer un enfoque no invasivo y de bajo costo, útil en salud ocupacional para prevenir lesiones y desarrollar wearables que detecten fatiga en tareas repetitivas o posturas prolongadas. |

---
## Productos comerciales

| **Dispositivo** | **Resumen técnico** | **Aplicación en salud ocupacional** | **Características clave** |
|-----------------|---------------------|-------------------------------------|----------------------------|
| **FreeEMG — BTS Bioengineering [7]** | Sistema inalámbrico de sEMG, compacto; permite registrar actividad en múltiples músculos de forma simultánea. | Monitoreo en campo, análisis de movimientos repetitivos y evaluación de carga muscular en tareas físicas. | Inalámbrico y portátil;<br>Alta resolución de señal;<br>Compatible con software de análisis biomecánico. |
| **EMG One — Waves Tech / Ideal Biomechanics [8]** | Dispositivo portátil y asequible para registrar actividad muscular y función neuromuscular; incluye app de biofeedback tipo videojuego. | Clínicas, consultorios y entornos laborales para seguimiento de fatiga, fuerza y coordinación muscular. | Amplificación 1000×;<br>Filtros 10–450 Hz;<br>App interactiva para entrenamiento;<br>Batería recargable. |  
| **K-Myo — Kinvent [9]** | Sensor EMG no invasivo con Bluetooth; análisis en tiempo real de activación muscular, desequilibrios y evolución del usuario. | Fisioterapia laboral, rehabilitación postural y prevención de lesiones en tareas repetitivas. | Frecuencia de adquisición 1000–2000 Hz;<br>Precisión ±0.1%;<br>Alcance inalámbrico 50 m;<br>Compatible con Android/iOS. | 

---
## Patentes

| Título | Contexto | Métodos Empleados | Resultados | Relevancia Ocupacional |
|----|----|----|----|----|
| **KR102485242B1 - Dispositivo y método para predecir lesiones musculares durante la actividad laboral repetitiva del trabajador [10]** | Aborda la falta de manejo de datos en PYMES y cómo los movimientos repetitivos generan fatiga muscular y enfermedades musculoesqueléticas. | Un sensor EMG recolecta datos musculares; la señal se filtra y se ingresa a un modelo de *machine learning* que evalúa variabilidad y fuerza para determinar riesgo de lesión. | Predice lesiones de forma temprana y brinda un plan preventivo con alertas y ejercicios de rehabilitación, reduciendo riesgos y pérdidas económicas. | Altamente relevante: se ajusta al contexto laboral de manufactura y tareas repetitivas. |
| **KR101938241B1 - Aparato y método para generar un modelo de prevención de lesiones basado en aprendizaje automático [11]** | Se centra en lesiones de atletas por entrenamientos intensos y la dificultad de predecirlas, ya que el dolor reportado no siempre coincide con la lesión real. | Un modelo de *machine learning* analiza condición física antes y después del entrenamiento, considerando intensidad, área de dolor y características individuales. | Permite predecir lesiones de manera objetiva relacionando estado físico y riesgo de lesión, con base en datos recolectados. | Aunque está enfocado en atletas, puede aplicarse en trabajadores manuales con alta exigencia física. |
| **US20200015700A1 - Dispositivo sensor de electromiografía biométrica para monitorización de la fatiga y prevención de lesiones [12]** | Propone un dispositivo vestible con EMG y acelerómetro para monitorear fatiga y prevenir lesiones por sobreuso en atletas y usuarios comunes. | El EMG detecta contracciones y el acelerómetro elimina artefactos de movimiento. Los datos se envían a una app que usa un algoritmo de *machine learning* para medir fatiga. | Determina niveles de fatiga a partir de parámetros como frecuencia media y potencia de salida, ofreciendo retroalimentación útil al usuario. | Directamente aplicable en entornos laborales con movimientos repetitivos o esfuerzo constante. |


---
## 📚 Referencias

[1] F. J. Sánchez Fu, *Fatiga laboral y lesiones músculo esqueléticas en trabajadores de una empresa de seguridad y vigilancia Lima – Perú 2018*,  
Universidad Peruana Cayetano Heredia, Maestría en Medicina Ocupacional y del Medio Ambiente, Lima, Perú, 2020.  
[En línea]. Disponible en: [Handle](https://hdl.handle.net/20.500.12866/10094)  

[2] S. Torres-Ruiz, “Riesgo ergonómico y trastornos musculoesqueléticos en trabajadores de industria alimentaria en el Callao en el 2021,”  
*Horizonte Médico*, vol. 23, no. 3, e2207, Lima, Perú, 2023.  
[En línea]. Disponible en: [Scielo](http://www.scielo.org.pe/scielo.php?script=sci_abstract&pid=S1727-558X2023000300005)  

[3] S. C. Zamora-Chávez, R. Vásquez-Alva, C. Luna-Muñoz y L. L. Carvajal-Villamizar,  
“Factores asociados a trastornos musculoesqueléticos en trabajadores de limpieza del servicio de emergencia de un hospital terciario,”  
*Revista de la Facultad de Medicina Humana*, vol. 20, no. 3, pp. 388–396, Lima, Perú, 2020.  
[En línea]. Disponible en: [Scielo](http://www.scielo.org.pe/pdf/rfmh/v20n3/2308-0531-rfmh-20-03-388.pdf)  

[4] H. A. Yousif, M. A. Mohammed, M. A. Mostafa y M. S. Alsharif,  
“Evaluación de la fatiga muscular basada en señales EMG de superficie utilizando enfoques estadísticos y de aprendizaje automático: una revisión,” 
*IOP Conference Series: Materials Science and Engineering*, vol. 705, pp. 012036, nov. 2019.  
[En línea]. Disponible en: [ResearchGate](https://www.researchgate.net/publication/337689967_Assessment_of_Muscles_Fatigue_Based_on_Surface_EMG_Signals_Using_Machine_Learning_and_Statistical_Approaches_A_Review/fulltext/5de5bea2299bf10bc33a70b8)  

[5] N. T. Huu, G. T. Luu, P. Ravier y O. Buttelli,  
“Detección de fatiga muscular mediante señales EMG de superficie utilizando algoritmos de aprendizaje automático,”  
en *IFMBE Proceedings*, vol. 96, Springer, 2025, pp. 445–452.  
[En línea]. Disponible en: [Springer](https://link.springer.com/chapter/10.1007/978-3-031-90197-3_65)  

[6] M. A. Rodríguez, J. C. Morales y L. F. Salazar,  
“Detección de fatiga muscular durante contracciones isométricas de miembros inferiores: un enfoque de aprendizaje automático,”  
*Frontiers in Physiology*, vol. 16, art. 1547257, 2025.  
[En línea]. Disponible en: [Frontiers](https://www.frontiersin.org/journals/physiology/articles/10.3389/fphys.2025.1547257/full)  

[7] BTS Bioengineering, “FreeEMG: sistema inalámbrico de electromiografía de superficie,” BTS Bioengineering. [En línea]. Disponible en: https://www.btsbioengineering.com/products/freeemg/. [Accedido: 25-ago-2025].

[8] Ideal Biomechanics, “EMG One: sensor portátil de electromiografía,” Ideal Biomechanics. [En línea]. Disponible en: https://www.idealbiomechanics.com/product-page/emg-one. [Accedido: 25-ago-2025].

[9] Rocfit, “K-Myo: sensor de electromiografía portátil,” Rocfit. [En línea]. Disponible en: https://www.rocfit.com/profesionales/tecnologia/kmyo-sensor-de-electromiografia-portatil. [Accedido: 25-ago-2025].

[10] KR 102485242 B1 – Device and method to predict muscle injury during repetitive work activities of a worker. Google Patents. 
Google Patents

[11] KR 101938241 B1 – Apparatus and method for generating injury prevention model based on machine learning. Google Patents. 
Google Patents

[12] US 2020/0015700 A1 – Biometric electromyography sensor device for fatigue monitoring and injury prevention and methods for using same. Google Patents.

---
## Aporte de los Integrantes

| Integrante | Aporte |
|------------|--------|
| NAVARRO LUYO, Katherine Rossana  | 33.33% |
| CÁRDENAS INFANTES, Brenda Adriana  | 33.33% |
| CARRASCAL CASTILLO, Diego Aaron | 33.33% |

