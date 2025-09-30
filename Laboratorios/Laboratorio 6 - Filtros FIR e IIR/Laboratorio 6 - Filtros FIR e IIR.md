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
Los filtros digitales son sistemas matemáticos que permiten modificar el espectro de una señal con el fin de eliminar o atenuar el ruido y resaltar las componentes de interés [1].

* Los **filtros FIR** tienen una respuesta al impulso de duración finita, siempre son estables y permiten fase lineal exacta, lo que los hace especialmente útiles en aplicaciones clínicas donde la forma de onda debe conservarse [4].
* Los **filtros IIR** emplean realimentación y alcanzan buenos resultados con órdenes menores, lo que los hace más eficientes en sistemas de tiempo real. Sin embargo, pueden introducir fase no lineal y requieren un diseño cuidadoso [6].

### 4.2 Transformada de Fourier
La **Transformada de Fourier**, calculada de forma rápida mediante la FFT, permite observar las señales en el dominio de la frecuencia. Con ella se pueden identificar picos de ruido (como los 50/60 Hz en ECG) o diferenciar ritmos cerebrales en EEG [1], [3], [8]. Este análisis es fundamental para diseñar filtros adecuados.

### 4.3 Relación Señal a Ruido (SNR)
La SNR expresa la proporción entre la energía de la señal útil y la del ruido. Un filtrado exitoso se traduce en un aumento de esta relación, siempre que no se eliminen componentes fisiológicos relevantes [5], [7].

### 4.4 Correlación cruzada
La correlación cruzada mide la similitud entre dos señales a lo largo del tiempo. Al aplicarse a una señal original y a su versión filtrada, permite comprobar si el filtrado ha preservado la forma de la señal o ha introducido distorsiones [4], [9], [11].

### 📊 Datos de señales  
- EMG  
- ECG  
- EEG  

---

## 4. 📚 Fundamentos Teóricos  
### 🔹 Filtros digitales (FIR e IIR)  
### 🔹 Transformada de Fourier y análisis en frecuencia  
### 🔹 Relación señal-ruido (SNR, Signal-to-Noise Ratio) ⭐ *(punto extra)*  
### 🔹 Correlación cruzada como método de similitud ⭐ *(punto extra)*  

---

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
 

---

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

---

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
