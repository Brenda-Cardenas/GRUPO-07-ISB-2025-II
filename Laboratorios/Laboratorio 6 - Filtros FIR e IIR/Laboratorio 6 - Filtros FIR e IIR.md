# 🧪 Informe de Laboratorio 6: Filtros FIR e IIR

---

## 1. 📖 Introducción  
El análisis de bioseñales como la electromiografía (EMG), la electrocardiografía (ECG) y la electroencefalografía (EEG) constituye un eje central en la práctica clínica y la investigación biomédica, ya que permite obtener información cuantitativa sobre la actividad muscular, cardíaca y cerebral. Sin embargo, estas señales suelen estar afectadas por interferencias y ruidos como la línea eléctrica (50/60 Hz), artefactos de movimiento, ruido muscular de alta frecuencia y la deriva lenta de la línea base causada por fenómenos fisiológicos y técnicos [1], [2]. Estos factores dificultan la interpretación y pueden comprometer el diagnóstico clínico.

El procesamiento digital de señales (DSP) ofrece soluciones más robustas y flexibles que los métodos analógicos tradicionales. A diferencia de los filtros analógicos, los filtros digitales no dependen de componentes físicos susceptibles a tolerancias o cambios de temperatura, sino que se implementan en software, lo que garantiza estabilidad, reproducibilidad y adaptabilidad [1], [3]. Esta ventaja ha permitido el diseño de algoritmos especializados que optimizan la supresión de ruido manteniendo la información fisiológica de interés.

Los filtros FIR (Finite Impulse Response) presentan estabilidad incondicional y pueden diseñarse con fase lineal exacta, lo cual preserva la morfología temporal de la señal. Esto resulta crítico en ECG, donde pequeñas distorsiones en la forma de onda pueden alterar parámetros diagnósticos como el intervalo PR o el complejo QRS [4], [5]. Por otro lado, los filtros IIR (Infinite Impulse Response) son más eficientes en términos computacionales, pues logran pendientes de atenuación pronunciadas con órdenes menores, siendo adecuados para aplicaciones en tiempo real y sistemas embebidos [6]. Sin embargo, presentan fase no lineal y riesgo de inestabilidad si no se diseñan adecuadamente [1], [3].

En el ámbito clínico, múltiples estudios han explorado estrategias de filtrado digital. En ECG, se han propuesto combinaciones de filtros notch, IIR adaptativos y técnicas de sustracción para eliminar la interferencia de 50/60 Hz sin comprometer la morfología [7]. En EMG, el uso de filtrado digital se ha combinado con técnicas de selección de características para mejorar la clasificación de gestos musculares en interfaces hombre-máquina [8]. En EEG, investigaciones recientes han comparado métodos de diseño de filtros FIR aplicados a la eliminación de artefactos oculares y de parpadeo, evaluando su impacto en la preservación de ritmos corticales [9].

En este laboratorio se estudiará el diseño, implementación y comparación de filtros FIR e IIR aplicados a EMG, ECG y EEG, evaluando el desempeño cualitativo (observación de las formas de onda) y cuantitativo mediante métricas como la relación señal-ruido (SNR) y la correlación cruzada. Esto permitirá comprender las fortalezas y limitaciones de cada enfoque y su aplicabilidad en contextos biomédicos reales.

---

## 2. 🎯 Objetivos  
### ✅ Objetivo general  
### 🎯 Objetivos específicos  

---

## 3. 💻 Materiales y Herramientas  
### 🛠️ Software  
- Python  
- Google Colab  
- Librerías: NumPy, SciPy, Matplotlib  

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

## 5. 📝 Metodología  
### ⚡ Diseño y aplicación de filtros para señales EMG  
### ❤️ Diseño y aplicación de filtros para señales ECG  
### 🧠 Diseño y aplicación de filtros para señales EEG  
### 📈 Cálculo de SNR en señales filtradas ⭐ *(punto extra)*  
### 🔍 Implementación de correlación cruzada ⭐ *(punto extra)*  

---

## 6. 📊 Resultados  
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

## 7. 💭 Discusión de resultados  
### 🔹 Comparación entre FIR e IIR  
### 🔹 Impacto en la limpieza de la señal  
### 🔹 Evaluación de SNR ⭐  
### 🔹 Utilidad de la correlación cruzada ⭐  

---

## 8. 🏁 Conclusiones  

---

## 9. 📚 Referencias  

---

## 10. 👥 Aporte de los integrantes  

