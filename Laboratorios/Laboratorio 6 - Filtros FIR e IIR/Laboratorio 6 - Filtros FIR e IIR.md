# Informe de Laboratorio 6: Filtros FIR e IIR
---

## 1. Introducción

Las bioseñales como la electromiografía (EMG), la electrocardiografía (ECG) y la electroencefalografía (EEG) son herramientas fundamentales para el estudio de la actividad muscular, cardíaca y cerebral. Estas señales suelen estar contaminadas por diversos tipos de ruido, como la interferencia de la red eléctrica, los artefactos de movimiento y la deriva de la línea base [1], [2]. Dichas alteraciones dificultan la interpretación y si no se observan de manera  addecuada puden afectar la precisión de un diagnóstico clínico. Para evitarlo, se emplea el **procesamiento digital de señales**, el cual ofrece ventajas frente al procesamiento analógico, ya que permite diseñar filtros precisos, estables y reproducibles [1], [3]. Entre las técnicas más empleadas se encuentran los filtros FIR (Finite Impulse Response) y los IIR (Infinite Impulse Response).

Los **filtros FIR** cuentan con estabilidad y la posibilidad de diseñarse con fase lineal, lo que permite preservar la forma original de la señal, aspecto especialmente relevante en ECG, donde la mínima distorsión puede afectar el análisis clínico [4], [5]. Sin embargo, para alcanzar resultados exigentes suelen requerir un mayor número de cálculos y coeficientes. En contraste, los **filtros IIR** son más eficientes, ya que logran buenos resultados con órdenes más bajos, lo que facilita su uso en sistemas portátiles y aplicaciones en tiempo real [6]. Sin embargo, pueden introducir fase no lineal y requieren un diseño cuidadoso para mantener la estabilidad [1], [3].

La importancia clínica de estos filtros se ha demostrado en múltiples investigaciones. En ECG, los filtros digitales han permitido eliminar de forma robusta la interferencia de red sin alterar la detección de arritmias [7]. En EMG, se han combinado con métodos de clasificación para mejorar el reconocimiento de gestos musculares y el desarrollo de interfaces hombre-máquina [8]. En EEG, los filtros FIR han resultado útiles en la eliminación de artefactos de parpadeo y movimiento, preservando ritmos cerebrales esenciales como alfa, beta o delta [9].

En este laboratorio se propone el diseño, implementación y comparación de filtros FIR e IIR aplicados a EMG, ECG y EEG. El análisis se realizará tanto de forma cualitativa, observando las señales, como de forma cuantitativa. De esta manera, se busca comprender las ventajas, limitaciones y aplicaciones de cada tipo de filtro en el procesamiento de bioseñales.

## 2. Objetivos
### Objetivo general
- Comprender el uso de la biblioteca PyFDA, los tipos de filtros que ofrece y desarrollar la capacidad de diseñarlos e implementarlos para el procesamiento de señales biomédicas.

### Objetivos específicos
- Analizar el desempeño de diferentes tipos de filtros diseñados en PyFDA, identificando sus ventajas y limitaciones en el tratamiento de señales biomédicas.
- Explorar las funcionalidades de la biblioteca PyFDA para el diseño de filtros, destacando su aplicación práctica en el procesamiento y mejora de señales biomédicas.

## 3. Materiales
| Ítem     | Descripción                                                                 | Cantidad |
|----------|-----------------------------------------------------------------------------|----------|
| Laptop   | Equipo con capacidad de ejecutar software de procesamiento de señales.      | 1        |
| Software | Python 3.x y **PyFDA**| - |
| Datos    | Registros de bioseñales con interferencia controlada de laboratorios pasados | - |



## 4. Fundamentos Teóricos
### 4.1 Filtros digitales: FIR e IIR  

Los filtros digitales procesan señales discretas eliminando o reduciciendo componentes no deseadas, como ruidos e interferencias, y resaltar las frecuencias que contienen la información de interés clínico [1].  

- Los **filtros FIR (Finite Impulse Response)** se caracterizan por tener una respuesta impulsional de duración finita, lo que garantiza su estabilidad en cualquier condición. Una de sus principales ventajas es la posibilidad de diseñarlos con fase lineal exacta, lo que asegura que la forma original de la señal no se deforme, aspecto crucial en bioseñales como el ECG, donde pequeñas variaciones en la morfología pueden alterar el diagnóstico [4]. Además, su diseño permite controlar con precisión la banda de paso y la atenuación de la banda de rechazo, aunque esto suele requerir órdenes más altos y, por lo tanto, un mayor costo computacional.  

- Los **filtros IIR (Infinite Impulse Response)** utilizan realimentación en su estructura, lo que les permite obtener una respuesta de impulso infinita. Su principal ventaja es que logran un desempeño similar al de los FIR, pero con un número mucho menor de coeficientes, lo que los hace más eficientes para aplicaciones en tiempo real, como dispositivos biomédicos portátiles y sistemas de monitoreo continuo [6]. No obstante, presentan dos limitaciones: pueden generar una fase no lineal, lo que altera la forma de la señal, y requieren un diseño más cuidadoso para evitar problemas de inestabilidad numérica.  

En el ámbito biomédico, la elección entre FIR e IIR depende de las necesidades del análisis: los filtros FIR son preferidos cuando es indispensable preservar la morfología de la señal (ECG o EEG), mientras que los IIR resultan más útiles en situaciones donde la eficiencia computacional es prioritaria, como en la adquisición de EMG en tiempo real.  

### 4.2 Transformada de Fourier  

La **Transformada de Fourier** permite descomponer una señal en sus componentes de frecuencia. Su implementación eficiente mediante la **Transformada Rápida de Fourier (FFT)** facilita el análisis espectral de bioseñales en contextos clínicos y experimentales [1], [3].  

En ECG, la transformada permite identificar picos específicos en 50/60 Hz, asociados a la interferencia de la red eléctrica, y guiar el diseño de filtros notch para su eliminación. En EEG, posibilita la detección y separación de ritmos cerebrales (delta, theta, alfa, beta y gamma), permitiendo diferenciar entre actividad fisiológica normal y artefactos externos como el parpadeo o el movimiento [8]. En EMG, el análisis espectral ayuda a estudiar el rango de frecuencia de la señal muscular, que suele encontrarse entre 20 y 500 Hz, y a distinguirlo de interferencias ajenas a la contracción muscular.  

El análisis en frecuencia no solo permite detectar ruidos, sino también evaluar la efectividad del filtrado aplicado, ya que la reducción de picos indeseados en el espectro refleja la eficiencia del filtro.  

### 4.3 Relación Señal a Ruido (SNR)  

La **Relación Señal a Ruido (SNR)** es una métrica que compara la potencia de la señal útil frente a la del ruido presente en un registro. Se expresa generalmente en decibelios (dB) y constituye un indicador fundamental de la calidad de una señal biomédica [5].  

Un filtrado digital exitoso se refleja en un aumento de la SNR, lo que significa que se ha eliminado parte del ruido sin afectar de manera significativa la información fisiológica. En ECG, por ejemplo, un incremento en la SNR permite que las ondas P-QRS-T se distingan con mayor claridad, mejorando la detección de arritmias [7]. En EEG, una SNR más alta facilita el análisis de ritmos neuronales y su relación con procesos cognitivos o patológicos. En EMG, se traduce en la posibilidad de estudiar con mayor precisión los patrones de activación muscular sin la interferencia de artefactos eléctricos.  

La SNR también se utiliza como parámetro comparativo entre filtros: un diseño que logre incrementar la relación señal-ruido de manera significativa, preservando la forma de onda, se considera más eficiente y clínicamente útil.  

## 5. Metodología  

1. **Selección de señales**  
   Se emplearon señales de ECG, EMG y EEG adquiridas por el propio grupo en laboratorios anteriores. Estas señales fueron elegidas porque contenían diferentes tipos de interferencias (ruido de red, artefactos de movimiento y variaciones de base), lo cual permitió aplicar y validar los filtros digitales diseñados.  

2. **Instalación y configuración del entorno**  
   Se instaló el programa **PyFDA** en el entorno virtual de **Anaconda**, asegurando su correcto funcionamiento para el diseño de filtros digitales.  

3. **Diseño de filtros en PyFDA**  
   Para cada señal biomédica se diseñaron cuatro filtros diferentes, incluyendo opciones de tipo FIR e IIR.  
   - En ECG, se configuraron filtros con el fin de eliminar la interferencia de la red eléctrica y la deriva de línea base.  
   - En EMG, se diseñaron filtros para atenuar el ruido de alta frecuencia y los artefactos de movimiento.  
   - En EEG, se aplicaron configuraciones que permitieran resaltar bandas de interés y reducir interferencias.  

4. **Exportación de filtros**  
   Los filtros diseñados en PyFDA fueron exportados en formato **.csv**, conteniendo los coeficientes necesarios para su posterior aplicación en Python.  

5. **Implementación en Python**  
   Los coeficientes de los filtros exportados fueron integrados en scripts de **Python**, creando sistemas de una entrada y una salida. De este modo, se aplicaron los filtros directamente a las señales seleccionadas en el paso inicial.  

6. **Visualización de resultados**  
   Se graficaron las señales antes y después de la aplicación de cada filtro, lo que permitió observar los cambios logrados en el dominio temporal.  

7. **Análisis de parámetros**  
   Para cuantificar los resultados obtenidos se realizaron mediciones de la **relación señal-ruido (SNR)** y se aplicó la **correlación cruzada** entre las señales originales y filtradas. Estos análisis facilitaron la comparación objetiva entre los filtros FIR e IIR diseñados.
   
## 6. Resultados  
### Resultados de filtrado de EMG
#### Respuesta en frecuencia
![EMG Magnitud](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/EMG%20MAGNITUD.png)

#### Tabla
| Condición          | Señal Cruda                                                                 | Filtro Butterworth                                                          | Filtro FIR Lineal                                                           | Filtro FIR Bessel                                                           | Filtro Notch Butter                                                         |
|--------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Reposo**         | ![1](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/1.png) | ![2](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/2.png) | ![3](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/3.png) | ![4](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/4.png) | ![5](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/5.png) |
| **Movimiento lento** | ![6](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/6.png) | ![7](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/7.png) | ![8](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/8.png) | ![9](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/9.png) | ![10](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/10.png) |
| **Contracción**    | ![11](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/11.png) | ![12](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/12.png) | ![13](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/13.png) | ![14](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/14.png) | ![15](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/15.png) |

#### Respuesta obtenida en PyFDA
![PyFDA1](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/pyfda1.png)

### Resultados de filtrado de ECG
#### Respuesta en frecuencia
![ECG Magnitud](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/ECG%20MAGNITUD.png)

#### Tabla

| Condición          | Señal Cruda                                                                 | FIR (0.5–40 Hz)                                                             | Butterworth (0.5–40 Hz)                                                     | Chebyshev II (0.5–40 Hz)                                                   | Notch 50 Hz + Butterworth                                                   |
|--------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Reposo**         | ![16](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/16.png) | ![17](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/17.png) | ![18](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/18.png) | ![19](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/19.png) | ![20](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/20.png) |
| **Apnea**          | ![21](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/21.png) | ![22](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/22.png) | ![23](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/23.png) | ![24](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/24.png) | ![25](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/25.png) |
| **Post ejercicio** | ![26](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/26.png) | ![27](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/27.png) | ![28](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/28.png) | ![29](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/29.png) | ![30](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/30.png) |

#### Respuesta obtenida en PyFDA
![PyFDA2](https://github.com/Brenda-Cardenas/GRUPO-07-ISB-2025-II/blob/main/Laboratorios/Laboratorio%206%20-%20Filtros%20FIR%20e%20IIR/Im%C3%A1genes/pyfda2.png)

## 7. Discusión de resultados  
### Comparación entre FIR e IIR 
### Analisis EMG
El filtro FIR aplicado a la señal EMG evidencia una reducción progresiva del ruido de baja y alta frecuencia, preservando la morfología de los transitorios musculares gracias a su fase lineal. En la señal filtrada se aprecia que los picos de activación mantienen su posición temporal y simetría, lo cual es esencial para análisis de latencias y detección de potenciales de acción. Sin embargo, la necesidad de un mayor orden para lograr transiciones estrechas implica mayor costo computacional, lo que puede limitar su uso en tiempo real [12].
El filtro Chebyshev, por su parte, ofrece una atenuación más pronunciada en las bandas de parada con un orden relativamente bajo, lo que se observa en la señal como una mayor supresión del ruido residual respecto a otros filtros IIR. No obstante, el ripple en la banda de paso puede introducir pequeñas ondulaciones en la envolvente de la EMG y, debido a su fase no lineal, puede producir ligeras distorsiones en los picos si no se aplica en modo de fase cero. Esto compromete en cierta medida la fidelidad temporal de la señal [13].
En el caso del filtro Butterworth, la señal filtrada muestra una transición más suave y sin ondulaciones artificiales, dado que este diseño no presenta ripple en la banda de paso. La EMG resultante conserva la envolvente muscular de forma más estable que en el Chebyshev, aunque, al igual que otros IIR, presenta fase no lineal. Para análisis donde se prioriza la preservación de la morfología, suele aplicarse en forma de filtrado bidireccional (filtfilt), evitando desfase [14].
El filtro Notch, finalmente, se muestra altamente eficaz para remover la interferencia de 50/60 Hz, evidenciándose en las imágenes una supresión clara de la componente periódica de red sin una alteración significativa del resto de la banda útil de la EMG. Sin embargo, al ser un filtro muy específico, no elimina otros tipos de ruido de banda ancha, por lo que generalmente se emplea en combinación con un FIR o un Butterworth para obtener una señal con mejor relación señal-ruido [15].
En conjunto, si el objetivo es la preservación temporal de la señal EMG y se trabaja en entornos de análisis offline, el FIR representa la mejor opción. En aplicaciones en tiempo real, el Butterworth ofrece un equilibrio adecuado entre simplicidad y rendimiento. El Chebyshev es recomendable en escenarios donde se requiera mayor atenuación selectiva con bajo costo computacional, aunque a costa de pequeñas distorsiones. Finalmente, el Notch es imprescindible como complemento cuando existe contaminación de red, pero debe usarse junto a otro filtro más general para lograr una limpieza efectiva de la señal.

### Analisis ECG
El filtro FIR aplicado a la señal ECG evidencia una mejora clara en la supresión del ruido de alta frecuencia, preservando de forma adecuada la morfología de los complejos QRS y las ondas P y T. Esto se debe a su propiedad de fase lineal, que garantiza que no haya distorsión temporal de los eventos eléctricos. En la señal filtrada se observa un trazado limpio y sin desplazamientos en el tiempo, aunque con un leve suavizado de los contornos debido a la necesidad de mayor número de coeficientes para lograr pendientes de corte pronunciadas. Su uso resulta especialmente útil en análisis offline y en estudios donde se prioriza la precisión temporal [16].
El filtro Chebyshev presenta en la señal ECG una atenuación más agresiva de los ruidos fuera de la banda de interés, lo que se traduce en un fondo más silencioso respecto al FIR. Sin embargo, las ondulaciones de ripple en la banda de paso generan ligeras variaciones en la amplitud de las ondas, lo que puede alterar la evaluación de la morfología en estudios clínicos. Además, su fase no lineal puede desplazar los complejos QRS si no se aplica en modo de fase cero. Este comportamiento lo convierte en una herramienta potente para eliminar ruido, pero con limitaciones para análisis morfológicos finos [17].
En el caso del Butterworth, la señal resultante muestra una reducción estable del ruido sin ripple en la banda de paso, conservando la morfología principal de los complejos QRS con mayor fidelidad que el Chebyshev. La respuesta es suave y natural, sin introducir ondulaciones artificiales en la envolvente de la señal. Al ser un filtro IIR, también presenta fase no lineal, pero su aplicación en forma bidireccional (filtfilt) elimina este inconveniente, resultando en un balance adecuado entre simplicidad computacional y preservación de la forma de onda [18].
El filtro Notch se aprecia particularmente eficaz para la eliminación de la interferencia de la red eléctrica de 50/60 Hz, visible en el ECG como ruido sinusoidal superpuesto. En la señal filtrada, esta componente es suprimida de manera notable, permitiendo un registro más claro de la actividad eléctrica. Sin embargo, por su naturaleza selectiva, el notch no atenúa otros ruidos de banda ancha, por lo que su uso aislado es insuficiente en condiciones de ruido complejo. En la práctica, se emplea en conjunto con otros filtros paso banda o paso bajo para obtener una señal limpia [19].
En síntesis, para el procesamiento de ECG, el FIR es el más recomendable cuando se requiere máxima preservación temporal y morfológica, aunque a mayor coste computacional. El Butterworth constituye la mejor alternativa en tiempo real al ofrecer un compromiso adecuado entre estabilidad, fidelidad y eficiencia. El Chebyshev puede ser útil cuando se busca una fuerte atenuación en escenarios ruidosos, pero con precaución ante la distorsión de amplitud. Finalmente, el Notch resulta indispensable como filtro complementario para eliminar la interferencia de la red, pero no sustituye al diseño de un filtro principal.

### Analisis EEG
El filtro FIR aplicado a la señal EEG permite una supresión eficaz de componentes de alta frecuencia, preservando con alta fidelidad la fase de las oscilaciones cerebrales relevantes como alfa, beta y theta. Su respuesta de fase lineal asegura que los ritmos neuronales no sufran desplazamientos temporales, lo que resulta esencial en estudios de conectividad y sincronización neuronal. No obstante, requiere mayor número de coeficientes, aumentando la carga computacional, lo cual puede ser una limitación en aplicaciones en tiempo real [20].
El filtro Chebyshev aplicado a la señal EEG evidencia una atenuación más pronunciada de las interferencias, lo que se traduce en registros con menor nivel de ruido. Sin embargo, el ripple en la banda de paso puede introducir distorsiones en la amplitud de los ritmos cerebrales, afectando la interpretación cuantitativa en análisis de potencia espectral. Este tipo de filtro es útil en ambientes muy ruidosos, pero no siempre adecuado para estudios donde la precisión de amplitud es crítica [21].
El filtro Butterworth muestra un desempeño estable y suave, eliminando ruido sin ripple en la banda de paso y manteniendo una representación clara de las oscilaciones alfa y beta. Aunque su fase no es lineal, al aplicarse de manera bidireccional se corrige esta distorsión, ofreciendo una alternativa eficiente y confiable para el procesamiento en tiempo real de EEG. Su balance entre simplicidad y fidelidad lo hace especialmente atractivo para aplicaciones clínicas y dispositivos portátiles [22].
Por último, el filtro Notch es altamente eficaz en la eliminación de la interferencia de red eléctrica (50/60 Hz), un problema común en la adquisición de EEG. Al aplicar este filtro, el artefacto sinusoidal se reduce significativamente, mejorando la visibilidad de las oscilaciones cerebrales. No obstante, debido a su carácter selectivo, no elimina otros tipos de ruido como artefactos musculares o de movimiento, por lo que suele usarse como complemento y no como filtro principal [23].
En conclusión, el FIR es ideal para estudios que requieran máxima fidelidad temporal y preservación de fase, mientras que el Butterworth se presenta como la mejor opción práctica en entornos clínicos y aplicaciones en tiempo real. El Chebyshev resulta adecuado en escenarios de alto ruido pero puede alterar amplitudes, y el Notch es indispensable para suprimir la interferencia de la red. En conjunto, una combinación de Butterworth y Notch representa la solución más equilibrada para el procesamiento de EEG.
### Impacto en la limpieza de la señal  
### Evaluación de SNR ⭐  
### Utilidad de la correlación cruzada ⭐  



## 8. Conclusiones  


## 9. Referencias  

[1] A. V. Oppenheim and R. W. Schafer, *Discrete-Time Signal Processing*, 3rd ed. Upper Saddle River, NJ, USA: Pearson, 2010. [En línea]. Disponible en: https://books.google.com/books?id=1aAoAQAAMAAJ  

[2] R. M. Rangayyan, *Biomedical Signal Analysis*, 2nd ed. Hoboken, NJ, USA: Wiley–IEEE Press, 2015. [En línea]. Disponible en: https://ieeexplore.ieee.org/book/5264705  

[3] S. Sörnmo and L. Laguna, *Bioelectrical Signal Processing in Cardiac and Neurological Applications*. Amsterdam, Netherlands: Elsevier, 2005. [En línea]. Disponible en: https://www.sciencedirect.com/book/9780124375529  

[4] S. K. Mitra, *Digital Signal Processing: A Computer-Based Approach*, 4th ed. New York, NY, USA: McGraw-Hill, 2011. [En línea]. Disponible en: https://books.google.com/books?id=1YV8QgAACAAJ  

[5] A. Phinyomark, P. Phukpattaranont, and C. Limsakul, “Feature reduction and selection for EMG signal classification,” *Expert Syst. Appl.*, vol. 39, no. 8, pp. 7420–7431, 2012. [En línea]. Disponible en: https://www.sciencedirect.com/science/article/pii/S0957417412001023  

[6] S. K. Mitra and J. F. Kaiser, *Handbook for Digital Signal Processing*. Hoboken, NJ, USA: Wiley–IEEE Press, 2013. [En línea]. Disponible en: https://ieeexplore.ieee.org/book/5264706  

[7] S. Sörnmo, “Time-varying digital filtering of ECG signals,” *IEEE Trans. Biomed. Eng.*, vol. 39, no. 7, pp. 700–707, Jul. 1992. [En línea]. Disponible en: https://ieeexplore.ieee.org/document/151195  

[8] S. De Luca, L. Gil-Cayuela, and R. Bragós, “Reducing noise, artifacts and interference in single-channel EMG signals,” *Sensors*, vol. 23, no. 7, p. 3725, 2023. [En línea]. Disponible en: https://www.mdpi.com/1424-8220/23/7/3725  

[9] A. Pant, S. Banerjee, and R. Indu, “Comparative exploration on EEG signal filtering using windowing methods,” *Array*, vol. 23, 2024. [En línea]. Disponible en: https://www.sciencedirect.com/science/article/pii/S2590005624000106  

[10] M. D. Addison, *Illustrated Wavelet Transform Handbook*. Boca Raton, FL, USA: Taylor & Francis, 2002. [En línea]. Disponible en: https://www.routledge.com/Illustrated-Wavelet-Transform-Handbook/Addison/p/book/9780367398196  

[11] T. A. L. Wren, J. R. Do, J. R. Hara, and M. R. Rethlefsen, “Cross-correlation as a method for comparing dynamic electromyography signals during gait,” *J. Biomech.*, vol. 39, no. 14, pp. 2714–2718, 2006. [En línea]. Disponible en: https://doi.org/10.1016/j.jbiomech.2005.08.009  

