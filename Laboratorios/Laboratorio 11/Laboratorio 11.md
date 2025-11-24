# Laboratorio: Detección de ondas P, QRS y T en señales EKG reales

## 1. Introducción

El análisis de señales electrocardiográficas (EKG) permite identificar eventos eléctricos fundamentales del ciclo cardíaco, tales como la onda **P**, el complejo **QRS** y la onda **T**. La detección automática de estas ondas es clave para el diagnóstico de arritmias, el monitoreo cardiaco y el procesamiento digital de señales biomédicas.

En este laboratorio se utilizó una base de datos real de señales EKG proporcionada por el docente en formato **pickle (`.pkl`)**, la cual contiene 17 clases de ritmos cardíacos (por ejemplo: `NSR`, `PVC`, `AFIB`, `Trigeminy`, entre otros). El objetivo principal fue seleccionar una señal real de una de estas clases y aplicar un algoritmo que permita identificar las ondas **P**, **QRS (R)** y **T**, para luego visualizarlas y analizarlas.

## 2. Algoritmo NeuroKit2

Para completar el objetivo del laboratorio se utilizó la librería científica **[NeuroKit2](https://neuropsychology.github.io/NeuroKit/)**, la cual implementa algoritmos avanzados y validados para el procesamiento de señales fisiológicas, incluyendo la **delineación completa del ECG**.

A grandes rasgos, NeuroKit2 realiza:

- **Preprocesamiento automático** de la señal (corrección de línea base, filtrado banda).
- **Detección robusta de picos R** usando métodos derivados de Pan–Tompkins u otros enfoques modernos.
- **Delineación de ondas P, Q, R, S y T**, mediante:
  - Transformadas wavelet,
  - Análisis de la morfología de la señal,
  - Reglas heurísticas basadas en distancias temporales (intervalos PR, QT, etc.).

La función principal utilizada es:

```python
signals, info = nk.ecg_process(ecg_signal, sampling_rate=fs) 
```

donde:
- signals contiene versiones procesadas del ECG (filtrado, limpios, etc.),  
- info es un diccionario que incluye los índices de las ondas detectadas, por ejemplo:

```python
info["ECG_P_Peaks"]   # Índices de las ondas P
info["ECG_R_Peaks"]   # Índices de los picos R (QRS)
info["ECG_T_Peaks"]   # Índices de las ondas T
```
De esta forma, NeuroKit2 permite:

- Detectar ondas P,
- Detectar complejos QRS (picos R),
- Detectar ondas T,

## 3. Metodología

### 3.1 Materiales y recursos

| Recurso / Herramienta        | Descripción                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| Laptop personal              | Equipo de cómputo con procesador Intel i5/i7 (o similar) y 8–16 GB de RAM. |
| Google Colab                 | Entorno de ejecución en la nube para Python.                               |
| Python 3.x                   | Lenguaje de programación utilizado en el laboratorio.                      |
| `dataset_ekg.pkl`            | Base de datos de señales EKG reales en formato pickle.                     |
| `ecg_processing.ipynb`       | Notebook proporcionado por el docente como guía base del laboratorio.      |
| Librería `NeuroKit2`         | Librería de Python para análisis y delineación de señales EKG.             |
| Librerías `NumPy` y `Matplotlib` | Para manejo de arreglos numéricos y generación de gráficas.         |

---

### 3.2 Pasos de implementación en código

A continuación se resumen los pasos principales realizados en el notebook.

#### 3.2.1 Instalación y carga de librerías

```python
# Instalación de NeuroKit2 (en Google Colab)
!pip install neurokit2

import pickle
import numpy as np
import matplotlib.pyplot as plt
import neurokit2 as nk
```

### 3.2.2 Carga de la base de datos (.pkl)
```python
with open("dataset_ekg.pkl", "rb") as f:
    dataset = pickle.load(f)

# Visualizar las clases disponibles en el dataset
print(dataset.keys())
```

### 3.2.3 Selección de una clase y de una señal
En este laboratorio se seleccionó la clase Trigeminy y la señal de la fila 0 como ejemplo.

```python
clase = "Trigeminy"
fila = 0

# Señal ECG real de la clase y fila seleccionadas
ecg_signal = dataset[clase][fila, :]

# Frecuencia de muestreo (Hz), según la base de datos
fs = 360

# Vector de tiempo asociado a la señal
t = np.arange(ecg_signal.size) / fs

print("Clase seleccionada:", clase)
print("Forma de la señal:", ecg_signal.shape)
```

### 3.2.4 Procesamiento de la señal con NeuroKit2

```python
# Procesamiento completo del ECG con NeuroKit2
signals, info_nk = nk.ecg_process(ecg_signal, sampling_rate=fs)

# Función auxiliar para limpiar picos (remover NaN y convertir a enteros)
def limpiar_peaks(peaks):
    arr = np.array(peaks, dtype=float)
    arr = arr[~np.isnan(arr)]      # eliminar valores NaN
    return arr.astype(int)         # convertir a índices enteros

# Índices (en muestras) de ondas P, R y T
p_peaks = limpiar_peaks(info_nk["ECG_P_Peaks"])
r_peaks = limpiar_peaks(info_nk["ECG_R_Peaks"])
t_peaks = limpiar_peaks(info_nk["ECG_T_Peaks"])

print("Nº de ondas P detectadas:", len(p_peaks))
print("Nº de ondas R detectadas:", len(r_peaks))
print("Nº de ondas T detectadas:", len(t_peaks))
```

### 3.2.5 Generación de la gráfica final
```python
plt.figure(figsize=(14, 4))

# Señal ECG original
plt.plot(t, ecg_signal, label="ECG")

# Picos R (complejos QRS)
if len(r_peaks) > 0:
    plt.scatter( t[r_peaks], ecg_signal[r_peaks], s=60, marker="o", facecolors="none", edgecolors="red", label="R (QRS)",)

# Ondas P
if len(p_peaks) > 0:
    plt.scatter( t[p_peaks], ecg_signal[p_peaks], s=80, marker="^", color="green", label="P",)

# Ondas T
if len(t_peaks) > 0:
    plt.scatter( t[t_peaks], ecg_signal[t_peaks], s=80, marker="v", color="magenta", label="T", )

plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud")
plt.title(f"Detección de ondas P, QRS (R) y T – clase {clase}, fila {fila}")
plt.legend()
plt.grid(ls=":")
plt.tight_layout()
plt.show()
```

## 4. Resultados

Tras procesar la señal correspondiente a la clase **Trigeminy** (fila 0) del archivo `dataset_ekg.pkl`, se obtuvieron los siguientes resultados:

- **Nº de ondas P detectadas:** 10  
- **Nº de complejos QRS (picos R) detectados:** 10  
- **Nº de ondas T detectadas:** 8  

La diferencia entre la cantidad de ondas detectadas refleja la complejidad morfológica de esta arritmia.  
En la gráfica generada se observa:

- La **señal ECG original** (trazo azul).  
- Los **picos R** marcados con círculos rojos.  
- Las **ondas P** marcadas con triángulos verdes.  
- Las **ondas T** marcadas con triángulos magenta.  

El patrón trigeminal se manifiesta con latidos ventriculares prematuros (PVC) cada tres latidos.  
Estos latidos alterados presentan:

- Complejos QRS más anchos.  
- Variaciones en la amplitud.  
- Ondas T que pueden aparecer distorsionadas o fusionadas.  

Esto explica por qué algunas ondas T no son detectadas con claridad por el algoritmo.

## 5. Discusión

El análisis de señales EKG reales enfrenta desafíos debido a:

- **Ruido** y variabilidad fisiológica.  
- **Artefactos** generados por movimiento o interferencia.  
- **Arritmias**, como Trigeminy, que modifican la morfología típica del ciclo cardiaco.

En la señal analizada, los latidos normales y los latidos prematuros muestran diferencias claras:

- Los **complejos QRS** de los latidos prematuros son más anchos e irregulares.  
- Algunas **ondas P** pueden verse ocultas o desplazadas por la actividad ventricular prematura.  
- Las **ondas T** pueden aparecer disminuidas, invertidas o fusionadas, lo que explica que solo se detectaran 8.

El algoritmo simple del notebook docente permite **detectar QRS**, pero no P ni T.  
En cambio, **NeuroKit2** agrega:

- Filtrado avanzado  
- Detección robusta de R-peaks  
- Detección completa de ondas P/T mediante técnicas basadas en transformadas y heurísticas clínicas  

Gracias a ello fue posible delinear la señal completa, incluso en presencia de arritmias complejas.

El hecho de que haya menos ondas T que R es **consistente clínicamente** con el Trigeminy, ya que la repolarización ventricular se ve alterada en los latidos prematuros.

## 6. Conclusiones

- La base de datos `dataset_ekg.pkl` permitió trabajar con señales reales y ritmos cardíacos variados, incluyendo arritmias.  
- El algoritmo proporcionado por el docente es útil para aprender a detectar QRS, pero **no detecta ondas P ni T**, por lo que no basta para completar el laboratorio.  
- **NeuroKit2** permitió realizar una **delineación completa del ECG**, identificando P, QRS (R) y T de manera automatizada.  
- La señal de la clase **Trigeminy** mostró alteraciones morfológicas coherentes con una arritmia ventricular, afectando especialmente la onda T.  
- El procesamiento implementado cumplió correctamente con los objetivos del laboratorio, permitiendo obtener una visualización clara de las ondas y comprender su relación con el ritmo cardiaco patológico.  
- Las diferencias en la detección (10 R vs. 8 T) son explicables en función del comportamiento real del corazón bajo un patrón trigeminal.
