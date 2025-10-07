# **Laboratorio 7: Transformada Wavelet**
## Introducción
El análisis de señales cuyas características varían en el tiempo es un desafío para el procesamiento digital. Para dichas señales, la transformada de Fourier se ve limitada debido a que esta se usa con señales estacionarias, lo que limita su capacidad para detectar eventos rápidos o transitorios [1]. Es por ello que la transformada wavelet resulta eficaz para analizar este tipo de señales porque permite analizar el tiempo y frecuencia de manera conjunta. 

La transformada wavelet descomponer una señal en versiones escaladas y desplazadas de una función base llamada mother wavelet. A diferencia de la transformada de Fourier, las wavelets se adaptan en escala y posición, lo que facilita analizar simultáneamente las partes lentas y los cambios rápidos de la señal. Esta descomposición se organiza en distintos niveles: los coeficientes de aproximación muestran las tendencias generales, mientras que los coeficientes de detalle resaltan variaciones transitorias [2]. 

Existen diversas familias de wavelets con propiedades particulares: las Daubechies, compactas y útiles en señales con bordes definidos; las Symlets, simétricas y adecuadas para reconstrucciones precisas; las Coiflets, con regularidad matemática para aplicaciones en señales biomédicas; y las biortogonales, que permiten una reconstrucción exacta gracias al uso de pares de funciones de análisis y síntesis [3]. La selección de la familia wavelet depende del tipo de señal a estudiar, del objetivo del análisis y de los requisitos de reconstrucción.

Debido a esto se puede emplear en múltiples áreas: en biomedicina, para el análisis de señales cardíacas y cerebrales; en la industria mecánica, para la detección temprana de fallas en equipos complejos como cajas de engranajes; y en la ingeniería ambiental, para el monitoreo de variables dinámicas como la calidad del aire [4], [5]. 

## Objetivos específicos
1. Aplicar la transformada wavelet para analizar señales EEG, EMG y EEG.
2. Comprender la utilidad de la transformada wavelet en el filtrado digital.
3. Diseñar un filtro digital basado en una familia de la transformada wavelet y justificar su configuración con respaldo en literatura científica reciente.

## Diseño del filtro
1. Elegir la familia de wavelet y justificar su elección.
2. Definir los parámetros del filtro.
3. Respaldar la elección con un artículo o referencia técnica.

## Metodología y diseño de filtro  

### Pasos generales  
1. Seleccionar la **familia wavelet** adecuada para cada tipo de señal biomédica.  
2. Definir el **nivel de descomposición** según la frecuencia de muestreo y el rango de interés.  
3. Elegir la **regla de umbralización** (soft o hard) más apropiada.  
4. Aplicar la **transformada discreta de wavelet (DWT)** y su **reconstrucción inversa (IDWT)**.  
5. Evaluar la calidad de la señal filtrada en términos de SNR, RMSE y conservación de la morfología.  

### Filtro para EMG  
| Nombre | Nivel | Umbral | Frecuencia |
|:--:|:--:|:--:|:--:|
| **Daubechies 4 (db4) / Symlets 5 (sym5)** | 5–7 | Universal Hard | 1000 Hz |

Las señales EMG presentan una alta concentración de componentes de frecuencia debido a los potenciales de acción generados por las fibras musculares. Para su procesamiento se seleccionaron las familias Daubechies 4 y Symlet 5, ya que tienen una resolución temporal y frecuencial, lo que facilita la detección de transitorios rápidos y la reducción del ruido sin afectar la forma de los picos de contracción. Estas familias han sido empleadas de forma consistente en estudios sobre transformadas wavelet en aplicaciones biomédicas, destacando su equilibrio entre estabilidad y capacidad de localización [6][7][8][12]. 

### 4.3 Filtro para ECG  
| Nombre | Nivel | Umbral | Frecuencia |
|:--:|:--:|:--:|:--:|
| **Daubechies 6 (db6) / Symlets 4 (sym4)** | 4–6 | Heursure Soft | 1000 Hz |

La señal ECG tiene una forma repetitiva y esta compuesta por las ondas P, QRS y T. Para su procesamiento se usaron las wavelets Daubechies 6 y Symlet 4 con niveles de descomposición entre 4 y 6, lo que permitió representar mejor los ciclos del corazón sin perder detalles importantes. Estas wavelets se utilizan con frecuencia en el análisis de señales fisiológicas por su capacidad para reducir el ruido sin alterar la forma original [6][7][8][12]. Se ha comprobado que un mayor número de momentos de anulación, como en la db6, ayuda a captar mejor las variaciones suaves del ECG y mejora su definición [9]. 

### Filtro para EEG  
| Nombre | Nivel | Umbral | Frecuencia |
|:--:|:--:|:--:|:--:|
| **Daubechies 4 (db4) / Symlets 4 (sym4)** | 6–8 | Universal Soft | 1000 Hz |

Las señales EEG tienen amplitudes bajas y se componen de distintas bandas de frecuencia entre 0.5 y 40 Hz. Para su análisis se usaron las wavelets Daubechies 4 y Symlet 4, ya que permiten estudiar variaciones lentas con buena precisión en el tiempo. Además, se utilizó la wavelet Morlet como base en la transformada continua para abarcar las escalas asociadas a las bandas cerebrales delta, theta, alpha, beta y gamma. Estas wavelets son adecuadas para separar frecuencias específicas sin alterar la forma general de la señal y resultan especialmente útiles en registros cerebrales, que son de naturaleza no estacionaria [8][9][12]. 

## Resultados
### Señales EMG
#### Comparación general de señales EMG — Bíceps Braquial
| Condición | Señal Cruda | Señal Filtrada (Wavelet Daubechies 4) |
|:--:|:--:|:--:|
| **Reposo** | <img src="./Multimedia/000_Bíceps-Braquial---Reposo.png" width="400"/> | <img src="./Multimedia/021_EMG-Filtrada-con-Wavelet-Daubechies-4-Umbral-por-Banda.png" width="400"/> |
| **Contracción isométrica máxima** | <img src="./Multimedia/011_Bíceps-Braquial---Contracción-isométrica-máxima.png" width="400"/> | <img src="./Multimedia/010_Señal-EMG-Original.png" width="400"/> |

#### Comparación general de señales EMG — Flexor
| Condición | Señal Cruda | Señal Filtrada (Wavelet Daubechies 4) |
|:--:|:--:|:--:|
| **Reposo** | <img src="./Multimedia/022_Flexor---Reposo.png" width="400"/> | <img src="./Multimedia/032_EMG-Filtrada-con-Wavelet-Daubechies-4-Umbral-por-Banda.png" width="400"/> |
| **Contracción isométrica máxima** | <img src="./Multimedia/033_Flexor---Contracción-isométrica-máxima.png" width="400"/> | <img src="./Multimedia/043_EMG-Filtrada-con-Wavelet-Daubechies-4-Umbral-por-Banda.png" width="400"/> |

#### Transformada y descomposición Wavelet
| Análisis | Imagen |
|:--:|:--:|
| Transformada de Wavelet Continua (Bíceps) | <img src="./Multimedia/003_Transformada-de-Wavelet-Continua.png" width="500"/> |
| Transformada de Wavelet Continua (Flexor) | <img src="./Multimedia/025_Transformada-de-Wavelet-Continua.png" width="500"/> |
| Scalograma de potencia (Bíceps) | <img src="./Multimedia/004_Scalograma-potencia-pcolormesh.png" width="500"/> |
| Scalograma de potencia (Flexor) | <img src="./Multimedia/026_Scalograma-potencia-pcolormesh.png" width="500"/> |
| Detalle Nivel 1 (Bíceps) | <img src="./Multimedia/006_Detalle-Nivel-i-bandasi-101f-bandasi-111f-Hz.png" width="500"/> |
| Detalle Nivel 1 (Flexor) | <img src="./Multimedia/028_Detalle-Nivel-i-bandasi-101f-bandasi-111f-Hz.png" width="500"/> |
| Aproximación muy baja frecuencia (Bíceps) | <img src="./Multimedia/018_Aproximación-muy-baja-frecuencia.png" width="500"/> |
| Aproximación muy baja frecuencia (Flexor) | <img src="./Multimedia/029_Aproximación-muy-baja-frecuencia.png" width="500"/> |
| Energía por banda (Bíceps) | <img src="./Multimedia/005_Señal-Original.png" width="500"/> |
| Energía por banda (Flexor) | <img src="./Multimedia/030_Energía-contenida-en-cada-banda-de-frecuencia.png" width="500"/> |

#### Análisis en frecuencia
| Representación | Imagen |
|:--:|:--:|
| Espectro de frecuencias (Bíceps) | <img src="./Multimedia/001_Espectro-de-frecuencias.png" width="500"/> |
| STFT de la señal (Bíceps) | <img src="./Multimedia/002_STFT-de-la-señal.png" width="500"/> |
| Espectro de frecuencias (Flexor) | <img src="./Multimedia/023_Espectro-de-frecuencias.png" width="500"/> |
| STFT de la señal (Flexor) | <img src="./Multimedia/024_STFT-de-la-señal.png" width="500"/> |

### Análisis de Señales ECG
#### Comparación general (señal temporal)
| Registro | Señal ECG Cruda | Señal ECG Filtrada (Wavelet Daubechies 4) |
|:--:|:--:|:--:|
| **A** | <img src="./Multimedia/022_ECG-Original.png" width="400"/> | <img src="./Multimedia/023_ECG-Filtrado-con-Wavelet-Daubechies-4-Umbral-por-Banda.png" width="400"/> |
| **B** | <img src="./Multimedia/033_ECG-Original.png" width="400"/> | <img src="./Multimedia/034_ECG-Filtrado-con-Wavelet-Daubechies-4-Umbral-por-Banda.png" width="400"/> |
| **C** | <img src="./Multimedia/007_ECG-Original.png" width="400"/> | — |

#### Transformada y descomposición Wavelet
| Análisis | Gráfico |
|:--:|:--:|
| Transformada Wavelet Continua | <img src="./Multimedia/016_Transformada-de-Wavelet-Continua.png" width="500"/> |
| Scalograma de Potencia | <img src="./Multimedia/017_Scalograma-potencia-pcolormesh.png" width="500"/> |
| Detalle Nivel 1 (≈10–11 Hz) | <img src="./Multimedia/019_Detalle-Nivel-i-bandasi-101f-bandasi-111f-Hz.png" width="500"/> |
| Aproximación (muy baja frecuencia) | <img src="./Multimedia/020_Aproximación-muy-baja-frecuencia.png" width="500"/> |
| Energía por banda | <img src="./Multimedia/021_Energía-contenida-en-cada-banda-de-frecuencia.png" width="500"/> |

#### Análisis en frecuencia (FFT / STFT)
| Representación | Gráfico |
|:--:|:--:|
| Espectro de frecuencias (FFT) | <img src="./Multimedia/014_Espectro-de-frecuencias.png" width="500"/> |
| STFT / Espectrograma | <img src="./Multimedia/015_STFT-de-la-señal.png" width="500"/> |

#### Ensayos fisiológicos (Derivada II)
| Condición | Gráfico |
|:--:|:--:|
| Reposo (Derivada II) | <img src="./Multimedia/000_Reposo---derivada-2.png" width="500"/> |
| Apnea respiratoria (Derivada II) | <img src="./Multimedia/013_Apnea-respiratoria---derivada-2.png" width="500"/> |
| Post-ejercicio (Derivada II) | <img src="./Multimedia/024_Post-ejercicio---derivada-2.png" width="500"/> |

### Análisis de señales EEG

#### Comparación general (Cruda vs Filtrada)
| Condición | Señal EEG Cruda | Señal EEG Filtrada (Wavelet Daubechies 4 – Umbral por banda) | Comentarios |
|:--|:--:|:--:|:--:|
| **Ensayo 1** | <img src="./Multimedia/031_EEG-Original.png" width="420"/> | <img src="./Multimedia/032_EEG-Filtrada-con-Wavelet-Daubechies-4-Umbrales-por-banda.png" width="420"/> | Reducción de ruido de alta frecuencia con preservación morfológica. |
| **Ensayo 2** | <img src="./Multimedia/020_EEG-Original.png" width="420"/> | <img src="./Multimedia/021_EEG-Filtrada-con-Wavelet-Daubechies-4-Umbrales-por-banda.png" width="420"/> | Eliminación de artefactos musculares manteniendo componentes alfa. |

#### Análisis en frecuencia (PSD / FFT)
| Análisis | Imagen |
|:--|:--:|
| Espectro de frecuencias (Ensayo 1) | <img src="./Multimedia/001_Espectro-de-frecuencias.png" width="520"/> |
| Espectro de frecuencias (Ensayo 2) | <img src="./Multimedia/012_Espectro-de-frecuencias.png" width="520"/> |
| Espectro de frecuencias (Ensayo 3) | <img src="./Multimedia/023_Espectro-de-frecuencias.png" width="520"/> |

#### ETFT / Espectrogramas
| Análisis | Imagen |
|:--|:--:|
| STFT de la señal (Ensayo 1) | <img src="./Multimedia/002_STFT-de-la-senal.png" width="520"/> |
| STFT de la señal (Ensayo 2) | <img src="./Multimedia/013_STFT-de-la-senal.png" width="520"/> |
| STFT de la señal (Ensayo 3) | <img src="./Multimedia/024_STFT-de-la-senal.png" width="520"/> |

#### Transformada Wavelet y Scalograma
| Tipo de análisis | Imagen |
|:--|:--:|
| Transformada de Wavelet Continua (Ensayo 1) | <img src="./Multimedia/003_Transformada-de-Wavelet-Continua.png" width="520"/> |
| Transformada de Wavelet Continua (Ensayo 2) | <img src="./Multimedia/014_Transformada-de-Wavelet-Continua.png" width="520"/> |
| Transformada de Wavelet Continua (Ensayo 3) | <img src="./Multimedia/025_Transformada-de-Wavelet-Continua.png" width="520"/> |
| Scalograma de potencia (Ensayo 1) | <img src="./Multimedia/004_Scalograma-potencia-pcolormesh.png" width="520"/> |
| Scalograma de potencia (Ensayo 2) | <img src="./Multimedia/015_Scalograma-potencia-pcolormesh.png" width="520"/> |
| Scalograma de potencia (Ensayo 3) | <img src="./Multimedia/026_Scalograma-potencia-pcolormesh.png" width="520"/> |

#### Descomposición y energía por bandas
| Nivel / Análisis | Imagen |
|:--|:--:|
| Detalle Nivel 1 (Ensayo 1) | <img src="./Multimedia/006_Detalle-Nivel-i-bandasi-101f-bandasi-111f-Hz.png" width="500"/> |
| Detalle Nivel 1 (Ensayo 2) | <img src="./Multimedia/017_Detalle-Nivel-i-bandasi-101f-bandasi-111f-Hz.png" width="500"/> |
| Detalle Nivel 1 (Ensayo 3) | <img src="./Multimedia/028_Detalle-Nivel-i-bandasi-101f-bandasi-111f-Hz.png" width="500"/> |
| Aproximación (baja frecuencia) | <img src="./Multimedia/018_Aproximacion-muy-baja-frecuencia.png" width="500"/> |
| Aproximación (Ensayo 3) | <img src="./Multimedia/029_Aproximacion-muy-baja-frecuencia.png" width="500"/> |
| Energía contenida por banda (Ensayo 1) | <img src="./Multimedia/019_Energia-contenida-en-cada-banda-de-frecuencia.png" width="500"/> |
| Energía contenida por banda (Ensayo 2) | <img src="./Multimedia/030_Energia-contenida-en-cada-banda-de-frecuencia.png" width="500"/> |

#### Señales originales y específicas
| Tipo / Ensayo | Imagen |
|:--|:--:|
| Señal EEG original (Ensayo 1) | <img src="./Multimedia/005_Senal-Original.png" width="520"/> |
| Señal EEG original (Ensayo 2) | <img src="./Multimedia/016_Senal-Original.png" width="520"/> |
| Señal EEG original (Ensayo 3) | <img src="./Multimedia/027_Senal-Original.png" width="520"/> |
| Señal EEG original (canal adicional) | <img src="./Multimedia/008_Senal-EEG-Original.png" width="520"/> |
| Señal EEG adicional | <img src="./Multimedia/010_Senal-EEG-Original.png" width="520"/> |
| EEG — Ojos cerrados | <img src="./Multimedia/011_Ojos-cerrados.png" width="520"/> |
| EEG — Tarea cognitiva | <img src="./Multimedia/022_Tarea-cognitiva.png" width="520"/> |
| EEG — Figura inicial | <img src="./Multimedia/000_EEG-Figura-1.png" width="520"/> |
| EEG — Original adicional | <img src="./Multimedia/009_EEG-Original.png" width="520"/> |

## Discusión
### Señales ECG
Al aplicar las wavelets Daubechies 4 (db4), Daubechies 6 (db6) y Symlet 4 (sym4) a la señal ECG, se observan diferencias en la claridad del complejo QRS y en la eliminación del ruido de baja frecuencia, que también se puede apreciar en los últimos niveles donde se descompone la onda original. Cada transformada presenta características específicas que influyen en la calidad del filtrado y la preservación morfológica de la señal.

La Daubechies 4 (db4) mostró el mejor equilibrio entre resolución temporal y frecuencial, eliminando el ruido sin distorsionar los complejos QRS. Su función base se asemeja al patrón típico del ECG, lo que favorece una delineación más precisa de los picos R [6], [7]. Diversos estudios recientes respaldan su eficacia para la detección automática y el filtrado adaptativo en señales biomédicas, destacándola como una de las más empleadas en la práctica [8].

Por otro lado, la Daubechies 6 (db6) permitió una reducción más notoria del baseline wander debido a su mejor resolución frecuencial. No obstante, su soporte más largo genera un leve suavizado en los picos QRS, reduciendo la exactitud temporal [6], [9]. Esto la hace apropiada para casos con ruido de baja frecuencia elevado, pero menos adecuada para aplicaciones donde se requiere precisión en la morfología.

La Symlet 4 (sym4), derivada de Daubechies pero con mayor simetría, redujo la distorsión temporal y mejoró la reconstrucción del ECG filtrado. Esta wavelet mantuvo la forma de las ondas P, QRS y T con menor retardo de fase, lo que la convierte en una alternativa eficaz para análisis morfológico [7], [10]. Su comportamiento estable la hace útil cuando se busca conservar la estructura del pulso cardíaco.

En conjunto, la wavelet db4 ofreció el mejor rendimiento general, al lograr una supresión de ruido efectiva y preservar la forma original del ECG. Esto coincide con múltiples investigaciones recientes que la señalan como la más apropiada para el procesamiento y detección de características del ECG [6], [8].

## Bibliografía
[1] V. Sunitha and S. S. Ali, “Wavelet Transform in Depth Study and Its Application,” Int. J. Creative Research Thoughts (IJCRT), vol. 11, no. 9, pp. 1–12, Sep. 2023. [Online]. Available: https://ijcrt.org/papers/IJCRT2309449.pdf

[2] V. Sunitha and S. S. Ali, “Wavelet Transform in Depth Study and Its Application,” International Journal of Creative Research Thoughts (IJCRT), vol. 11, no. 9, pp. 1–12, Sep. 2023. [Online]. Available: https://ijcrt.org/papers/IJCRT2309449.pdf 

[3] T.-D. Nguyen and P.-D. Nguyen, “Improvements in the Wavelet Transform and Its Variations: Concepts and Applications in Diagnosing Gearbox in Non-Stationary Conditions,” Applied Sciences, vol. 14, no. 11, Art. no. 4642, May 2024. [Online]. Available: https://www.mdpi.com/2076-3417/14/11/4642

[4] Z. Klai, M. Ayari, A. ElKamel, and M. A. Hammami, “From Theory to Practice: The Application of Wavelet Transform in Real-Time Engineering,” J. Appl. Math. & Informatics, vol. 42, no. 6, pp. 1341–1366, Oct. 2024. [Online]. Available: https://koreascience.kr/article/JAKO202404372004093.pdf

[5] T.-D. Nguyen and P.-D. Nguyen, “Improvements in the Wavelet Transform and Its Variations: Concepts and Applications in Diagnosing Gearbox in Non-Stationary Conditions,” Applied Sciences, vol. 14, no. 11, Art. no. 4642, May 2024. [Online]. Available: https://www.mdpi.com/2076-3417/14/11/4642

[6] Ahmad, N. et al. (2024). *Discrete wavelet transform based processing of embroidered textile-electrode electromyography.* **Biomedical Signal Processing and Control**, 92, 105520.  

[7] Zhang, Y. et al. (2022). *An improved wavelet threshold denoising approach for surface electromyography signal.* **IEEE Access**, 10, 65432–65440.  

[8] Raghavendra, U. et al. (2023). *An efficient ECG signals denoising technique based on the combination of PSO and wavelet transform.* **Measurement**, 216, 112985.  

[9] Singh, P. & Kaur, A. (2020). *Selection of Wavelet and Thresholding Rule for Denoising the ECG Signals.* **Int. J. Biomed. Eng. Technol.**, 34(2), 181–193.  

[10] Bairagi, V. & Pandey, N. (2022). *A Study of Chosen an Optimum Type of Wavelet Filter for De-Noising an ECG Signal.* **Signal Processing: Algorithms and Applications**, 38(4), 245–254.  

[11] Sharma, R. et al. (2023). *Wavelet-based denoising for EEG signal enhancement.* **Cognitive Neurodynamics**, 17(6), 945–959.  

[12] Das, T. & Roy, K. (2022). *Comparative analysis of EEG noise removal using DWT and hybrid approaches.* **Procedia Computer Science**, 218, 1218–1225. 
