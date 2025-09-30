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
### 💪 EMG  
- Reposo  
- Contracción leve  
- Contracción fuerte  

### ❤️ ECG  
- Estado basal  
- Respiración controlada  
- Post ejercicio  
- Respiración prolongada  

### 🧠 EEG  
- Basal  
- Ojos abiertos/cerrados  
- Ejercicios mentales simples y complejos  

## 7. Discusión de resultados  
### Comparación entre FIR e IIR  
### Impacto en la limpieza de la señal  
### Evaluación de SNR ⭐  
### Utilidad de la correlación cruzada ⭐  



## 8. Conclusiones  


## 9. Referencias  
[1] A. V. Oppenheim and R. W. Schafer, *Discrete-Time Signal Processing*, 3rd ed. Pearson, 2010.
[2] R. M. Rangayyan, *Biomedical Signal Analysis*, 2nd ed. Wiley–IEEE Press, 2015.
[3] S. Sörnmo and L. Laguna, *Bioelectrical Signal Processing in Cardiac and Neurological Applications*. Elsevier, 2005.
[4] S. Mitra, *Digital Signal Processing: A Computer-Based Approach*, 4th ed. McGraw-Hill, 2011.
[5] A. Phinyomark, P. Phukpattaranont, and C. Limsakul, “Feature reduction and selection for EMG signal classification,” *Expert Systems with Applications*, vol. 39, no. 8, pp. 7420–7431, 2012.
[6] S. K. Mitra and J. Kaiser, “Handbook for Digital Signal Processing,” Wiley-IEEE Press, 2013.
[7] S. Sörnmo, “Time-varying digital filtering of ECG signals,” *IEEE Trans. Biomed. Eng.*, vol. 39, no. 7, pp. 700–707, 1992.
[8] S. De Luca, L. Gil-Cayuela, and R. Bragós, “Reducing noise, artifacts and interference in single-channel EMG signals,” *Sensors*, vol. 23, no. 7, p. 3725, 2023.
[9] A. Pant, S. Banerjee, and R. Indu, “Comparative exploration on EEG signal filtering using windowing methods,” *Array*, vol. 23, 2024.
[10] M. D. Addison, *Illustrated Wavelet Transform Handbook*. Taylor & Francis, 2002.
[11] T. A. L. Wren et al., “Cross-correlation as a method for comparing dynamic electromyography signals during gait,” *J. Biomechanics*, vol. 39, no. 14, pp. 2714–2718, 2006.
