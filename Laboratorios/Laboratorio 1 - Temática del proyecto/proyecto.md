# Proyecto – Temática

## Título tentativo del proyecto
**Extracción de características de señales EMG para la detección temprana de fatiga muscular en el ámbito ocupacional**

---

## Problemática a abordar
<p align="justify">
La fatiga muscular en trabajadores de sectores con alta exigencia física y movimientos repetitivos es una problemática crítica en Perú y Latinoamérica, afectando no solo el bienestar, sino la seguridad y productividad laboral. Actualmente, la detección se basa en evaluaciones subjetivas como el dolor o el cansancio, que son poco fiables y a menudo no reflejan el estado fisiológico real del músculo. Esto resulta en diagnósticos tardíos, aumento de lesiones musculoesqueléticas y pérdidas económicas para las empresas debido a ausentismo y menor rendimiento.  
Por ejemplo, en Lima, más del 10% de los agentes de seguridad han reportado fatiga moderada que se relaciona con lesiones, y en el sector salud de Puno, el 84% del personal reporta niveles medios de fatiga. Esta realidad resalta la necesidad de una solución objetiva, temprana y no invasiva que transforme la seguridad laboral de una respuesta a un problema a una estrategia de prevención activa.
</p>

---

## Objetivos a alcanzar

| **Objetivo General** | **Objetivos Específicos** |
|-----------------------|----------------------------|
| <p align="justify">Desarrollar un modelo de clasificación capaz de identificar el estado de fatiga muscular en tareas de alta repetición. Para ello, se usarán señales electromiográficas (EMG) como la principal fuente de datos, con el fin de prevenir lesiones en trabajadores manuales.</p> | <p align="justify">1. Recopilar y preprocesar datos de señales EMG de bases de datos públicas, eliminando ruidos para obtener una señal limpia.<br><br>2. Extraer características relevantes de las señales EMG que indiquen el inicio y el progreso de la fatiga muscular.<br><br>3. Entrenar y validar un modelo de clasificación para predecir el estado de fatiga con alta precisión.<br><br>4. Evaluar el rendimiento del modelo clasificador comparándolo con los resultados de otros estudios o métodos existentes para asegurar que nuestra solución sea efectiva.</p> |

---

## Herramientas a utilizar
- **Hardware:** Un electromiógrafo con electrodos de superficie para captar la actividad eléctrica de los músculos de forma no invasiva.  
- **Software y Entorno de Desarrollo:** Python en el entorno de desarrollo *Visual Studio Code*. Estas herramientas ofrecen un ecosistema robusto para la programación, el análisis de datos y el desarrollo de modelos de aprendizaje automático.  
- **Procesamiento de Señales:** Se aplicarán técnicas de filtrado digital para limpiar la señal EMG y asegurar datos confiables para el análisis posterior.  
- **Librerías de Python:**  
  - NumPy: Para la manipulación y procesamiento numérico de señales.  
  - Scikit-learn: Para la implementación de modelos de clasificación.  
  - TensorFlow/Keras o PyTorch: Para redes neuronales avanzadas, como CNN.  
- **Bases de Datos:** Se emplearán bases de datos de EMG de acceso público, como las de *PhysioNet* o *The Ninapro Database*, para entrenar y validar el modelo de clasificación.  

---

## Resumen del proyecto
<p align="justify">
La propuesta de nuestro proyecto se centra en la detección de la fatiga muscular, un fenómeno que no siempre es perceptible y que afecta a trabajadores expuestos a labores repetitivas o de esfuerzo físico en sectores laborales. A diferencia de las evaluaciones subjetivas actuales, que se basan en la percepción del cansancio u otros malestares, este proyecto plantea una solución objetiva y no invasiva.  
Al analizar las señales EMG, las cuales reflejan la actividad eléctrica del músculo, se podrán reconocer cambios distintivos a medida que la fatiga se desarrolla. Se realizará el procesamiento digital de señales para filtrar y limpiar los datos EMG. Posteriormente, un modelo de clasificación será entrenado utilizando bases de datos públicas para reconocer los patrones de la señal asociados a la fatiga. El objetivo final es que este modelo sea capaz de predecir el estado de fatiga de un músculo, sirviendo como una herramienta preventiva contra lesiones laborales.  
La relevancia de este proyecto radica en su impacto social y económico, ya que su aplicación en el contexto laboral permitiría mejorar la seguridad, reducir la cantidad de trabajadores que sufren lesiones y optimizar su rendimiento.
</p>

---

## Link del repositorio
[Enlace al repositorio en GitHub](https://github.com/usuario/GRUPO-XX-ISB-2025)  

