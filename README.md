# Laboratorio-2-Procesamiento

# OBJETIVO DE LA PRÁCTICA 

En esta práctica se desarrollaron tres conceptos fundamentales del procesamiento de señales: la convolución, la correlación y la transformada de Fourier. Inicialmente, se aplicó la convolución a señales construidas a partir de la cédula y el código de cada integrante, realizándola tanto de manera manual como mediante Python, lo que permitió analizar la respuesta de un sistema ante una entrada específica. Posteriormente, se estudió la correlación cruzada con el fin de comprender cómo se determina el grado de similitud entre dos señales. Más adelante, se generó una señal biológica que fue digitalizada siguiendo el criterio de Nyquist, y se examinaron sus principales características estadísticas. Finalmente, se empleó la transformada de Fourier para representar la señal en el dominio de la frecuencia y analizar su espectro, facilitando así una interpretación más completa de su comportamiento.

# Parte A

En la primera parte de la prática se trabajó la convolución entre un sistema h[n], definido a partir de los dígitos del código de cada uno de los integrantes y una señal x[n] construida con los dígitos de la cédula. Inicialmente, se realizó el cálculo manual y se representó el resultado de forma gráfica. Posteriormente, el mismo procedimiento se repitió en Python, lo que permitió verificar los resultados obtenidos y generar las gráficas correspondientes.


**1. Maria Jose :**


**-Convolución manual**

<img width="728" height="729" alt="image" src="https://github.com/user-attachments/assets/39dcfc9e-e928-4a0f-ae65-f646c3a49842" />

**-Gráfica manual**

<img width="521" height="736" alt="image" src="https://github.com/user-attachments/assets/db4edf3a-012e-48a7-a5aa-53640963ec35" />

**-Convolución y gráfica en python**

```python
# Majo
import numpy as np
import matplotlib.pyplot as plt

# -------------------------------
# Señales de entrada
# -------------------------------
h = [5, 6, 0, 0, 8, 6, 8]  # Código
x = [1, 0, 7, 6, 7, 3, 7, 7, 5, 3]  # Cédula

# Convolución
y = np.convolve(x, h)

# Mostrar valores secuenciales

print("Valores de y[n]:")
for i, val in enumerate(y):
    print(f"y[{i}] = {val}")

# -------------------------------
# Graficar señal
# -------------------------------
n = np.array([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15])
plt.stem(n,y)
# Índices de tiempo
plt.title("Señal y[n] = x[n] * h[n]")
plt.xlabel("n (índice)")
plt.ylabel("y[n]")
plt.grid(True)
plt.tight_layout()
plt.show()

```

<img width="675" height="725" alt="image" src="https://github.com/user-attachments/assets/80231478-e536-4492-b5a0-0f974a1aa1dd" />


**2. Kathalina :**

**-Convolución manual**


<img width="745" height="728" alt="image" src="https://github.com/user-attachments/assets/813717eb-5885-4aeb-a718-543094deaf52" />


**-Gráfica manual**

<img width="498" height="737" alt="image" src="https://github.com/user-attachments/assets/5f7e1de8-8118-40ee-889f-3474c448f92a" />



**-Convolución y gráfica en python**

```python
import numpy as np
import matplotlib.pyplot as plt

# -------------------------------
# Señales de entrada
# -------------------------------
h = [5, 6, 0, 0, 8, 7, 5]  # Código
x = [1, 0, 9, 6, 9, 4, 7, 8, 4, 4]  # Cédula

# Convolución
y = np.convolve(x, h)

# Mostrar valores secuenciales

print("Valores de y[n]:")
for i, val in enumerate(y):
    print(f"y[{i}] = {val}")

# -------------------------------
# Graficar señal
# -------------------------------
n = np.array([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15])
plt.stem(n,y)
# Índices de tiempo
plt.title("Señal y[n] = x[n] * h[n]")
plt.xlabel("n (índice)")
plt.ylabel("y[n]")
plt.grid(True)
plt.tight_layout()
plt.show()
```

<img width="618" height="729" alt="image" src="https://github.com/user-attachments/assets/076c096b-f186-448e-adb6-5dafbec3de8c" />

**Diagrama de Flujo parte A**

<img width="298" height="721" alt="image" src="https://github.com/user-attachments/assets/6015dd48-7d08-4e04-8f7e-e17a5b86a7f3" />


# Parte B

En la segunda parte de la práctica se definieron dos señales y se calculó su correlación cruzada, con el objetivo de medir el grado de similitud entre ellas. Una vez obtenida la secuencia resultante, se representó gráficamente para analizar su comportamiento y se discutió en qué situaciones resulta útil aplicar este procedimiento dentro del procesamiento digital de señales.
Las señales cruzadas fueron:

<img width="456" height="97" alt="image" src="https://github.com/user-attachments/assets/951f4523-681f-482f-ab5c-fef5f1285c34" />

**1. Correlación Cruzada entre ambas señales**

```python
import numpy as np
import matplotlib.pyplot as plt

# Parámetros
Ts = 1.25e-3   # 1.25 ms
f = 100        # Hz
N = 9          # número de muestras
n = np.arange(N)
w0 = 2*np.pi*f*Ts  # frecuencia digital

# Definición de señales
x1 = np.cos(w0 * n)
x2 = np.sin(w0 * n)

print("x1[n] =", np.round(x1, 4))
print("x2[n] =", np.round(x2, 4))

# Correlación cruzada
r12 = np.correlate(x1, x2, mode='full')
lags = np.arange(-N+1, N)

print("\nCorrelación cruzada r12[l]:")
for l, val in zip(lags, r12):
    print(f"l={l:2d}, r12={val:.4f}")

# Gráfica
plt.figure(figsize=(7,4))
plt.stem(lags, r12, basefmt="r-")
plt.xlabel("Retardo l (muestras)")
plt.ylabel("r12[l]")
plt.title("Correlación cruzada entre x1[n] y x2[n]")
plt.grid(True)
plt.show()
```

Los resultados obtenidos fueron:

<img width="612" height="350" alt="image" src="https://github.com/user-attachments/assets/23c0617d-f1ce-4e66-a28a-22cebc70385b" />

**2. Gráfica y secuencia resultante**

<img width="618" height="361" alt="image" src="https://github.com/user-attachments/assets/78007f03-1d00-49c4-8e73-149c6fb3838b" />

La correlación cruzada entre las señales (X_1[n]) y (X_2[n]) dio como resultado una secuencia con valores tanto positivos como negativos, los cuales cambian según el retardo (l). En la gráfica se nota que los picos más altos están cerca de (l = -2) y (l = 2), lo que significa que las señales se parecen bastante cuando una se desplaza respecto a la otra en esas puntos. También se observa que la secuencia es casi simétrica respecto al origen, indicando que la similitud aparece tanto para desplazamientos hacia la derecha como hacia la izquierda. En conclusión, ambas señales comparten características similares, pero estas coinciden en diferentes desfases temporales.


**3. Importancia de la correlación cruzada en el procesamiento digital de señales**

La correlación cruzada sirve para ver qué tan relacionadas están dos señales cuando una se corre en el tiempo, con ella se pueden detectar coincidencias, repeticiones o desfases entre ambas. En aplicaciones reales esto es  útil por ejemplo  en señales biomédicas permite analizar sincronización de ritmos, en telecomunicaciones ayuda a identificar una señal aunque esté contaminada con ruido, y en imágenes facilita encontrar similitudes entre patrones. En este ejercicio, permitió comprobar qué tanto se parecen las dos señales dependiendo del desplazamiento aplicado, mostrando de forma clara su relación temporal.

**Diagrama de Flujo parte B**

<img width="324" height="723" alt="image" src="https://github.com/user-attachments/assets/415dabf4-0fef-4a90-a680-6f11b4c9aeb8" />

# Parte C

En la ultima parte de esta práctica, se capto una señal EOG (electrooculograma) del generador de señales con ayuda del DAQ. Para esto, se utilizó el siguiente codigo:
Para esta señal se calculó primero la frecuencia de Nyquist. Se tomó como referencia la frecuencia máxima de la señal EOG, que es aproximadamente 50 Hz, y se multiplicó por 2, obteniendo así una frecuencia de Nyquist de 100 Hz (50 Hz × 2).

Luego, para realizar la digitalización, se utilizó una frecuencia de muestreo cuatro veces mayor que la de Nyquist, es decir, 400 Hz. Finalmente, se graficó la señal con una duración de 5 segundos, una frecuencia de muestreo de 400 Hz y un total de 2000 muestras, obteniendo el siguiente resultado:

<img width="572" height="432" alt="image" src="https://github.com/user-attachments/assets/2994f3de-3b34-416a-ae3e-e6857b72d2e1" />

Después de esto, la señal fue analizada estadísticamente calculando su media, mediana, desviación estándar, así como sus valores máximo y mínimo.


```python
#media
media=np.mean(voltaje)
print (f"Media: {media} ")

#mediana
mediana=np.median(voltaje)
print (f"Mediana: {mediana} ")

#desviación estandar
desviacion_muestra=np.std(voltaje, ddof=1)
print (f"Desviacion estandar: {desviacion_muestra} ")

print(f"Máximo:", np.max(voltaje))
print(f"Mínimo:", np.min(voltaje))

print("Es una señal aleatoria, ya que depende de movimientos oculares y ruido fisiológico")
print("Es aperiódica, porque los movimientos oculares no ocurren en ciclos regulares.")
print("Aunque se digitaliza al muestrearla, se representa una señal originalmente análoga tomada con DAQ")

```
Los valores obtenidos fueron:

<img width="723" height="140" alt="image" src="https://github.com/user-attachments/assets/c0db8426-8f08-4ccd-98b1-71334b705530" />

La señal puede considerarse aleatoria, ya que está influenciada por los movimientos oculares y por el ruido fisiológico. Aunque un movimiento repetido puede producir una forma de onda similar, al tratarse de una señal EOG —de origen biológico— puede variar debido a factores como la respuesta individual del paciente.

Además, es aperiódica porque los movimientos oculares no siguen un patrón cíclico regular. Finalmente, aunque se digitaliza al momento de muestrearla, en esencia corresponde a una señal originalmente análoga adquirida mediante un sistema DAQ.

Ahora bien, se aplicó la transformada de Fourier:


```python
import matplotlib.pyplot as plt

#centra señal en cero
x = voltaje - np.mean(voltaje)
#numero de muestras y frecuencia de muestreo
N = len(x)
fs = 400

#funcion de transformada rapida de Fourier, rfft porque la señal es real y para devolver las frecuencias positivas
X = np.fft.rfft(x)
#vector de frecuencias para cada valor de la transformada, d=1/fs es el período de muestreo
f = np.fft.rfftfreq(N, d=1/fs)

#margnitud del espectro
mag = np.abs(X) / N

#grafica
plt.figure()
plt.plot(f, mag, color="red")
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Magnitud")
plt.title("Transformada de Fourier")
plt.grid(True)
plt.show()

```

<img width="550" height="430" alt="image" src="https://github.com/user-attachments/assets/6fbbefcf-9f98-4f53-a7f5-4cfa6fe58a15" />


Además, se realizó la gráfica de la densidad espectral de potencia de la señal para analizar cómo se distribuye su energía en el dominio de la frecuencia.

```python
fs = 400
N = len(voltaje)

fft_vals = np.fft.fft(voltaje)
fft_freq = np.fft.fftfreq(N, 1/fs)

fft_vals = fft_vals[:N//2]
fft_freq = fft_freq[:N//2]

psd = (1/(fs*N)) * np.abs(fft_vals)**2
psd[1:-1] *= 2   # <-- corrección clave

plt.figure(figsize=(8,4))
plt.semilogy(fft_freq, psd, color="blue")
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Densidad espectral (V²/Hz)")
plt.title("Densidad espectral de potencia")
plt.grid()
plt.show()
```


<img width="707" height="372" alt="image" src="https://github.com/user-attachments/assets/0c55da61-7507-44fb-957d-5f363d9ff05c" />


También se calcularon la media, la mediana y la desviación estándar, pero esta vez en el dominio de la frecuencia, para analizar el comportamiento estadístico de la señal desde su contenido espectral.

Los resultados obtenidos fueron:

<img width="319" height="58" alt="image" src="https://github.com/user-attachments/assets/eb4c6981-3071-4a52-95c7-ee0861a561e7" />

De igual manera, se realizó un histograma de frecuencias.

```python
plt.figure(figsize=(8, 4))
plt.hist(f, bins=50, weights=mag, color='pink', edgecolor='green')
plt.title("Histograma de Frecuencias")
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Magnitud acumulada")
plt.grid(True)
plt.show()

```

<img width="678" height="378" alt="image" src="https://github.com/user-attachments/assets/cf2fe3ff-5053-451a-8cf6-2b1eea910d1b" />

# RESULTADOS

**Parte A**



**Parte B**

En esta parte de la práctica se trabajó con dos señales discretas: una señal coseno  y una señal seno , ambas con una frecuencia de 100 Hz y un período de muestreo de . Estas dos señales tienen la misma frecuencia y forma de onda, pero presentan un desfase entre ellas, ya que el seno y el coseno están desplazados aproximadamente 90° en fase.

Para analizar la relación entre estas señales se calculó la correlación cruzada, la cual permite medir qué tan parecidas son dos señales cuando una se desplaza en el tiempo respecto a la otra. A partir de los resultados obtenidos se observó que la correlación presenta valores positivos y negativos dependiendo del retardo aplicado. El valor máximo de correlación aparece aproximadamente en el retardo , con un valor cercano a 3.5, lo que indica que las señales se parecen más cuando una se desplaza dos muestras respecto a la otra. Por otro lado, el valor mínimo se observa alrededor de , con un valor aproximado de -3.5, lo cual indica una relación inversa entre las señales en ese punto.

Al observar la gráfica de la correlación cruzada se nota que la secuencia tiene un comportamiento casi simétrico alrededor del origen. Además, cuando el retardo es cercano a cero, la correlación es prácticamente nula. Esto ocurre porque las señales seno y coseno, aunque tienen la misma frecuencia, están desfasadas, por lo que no coinciden cuando se comparan sin desplazamiento.

Este análisis permite entender que ambas señales comparten características similares, pero su mayor coincidencia se presenta cuando una de ellas se desplaza ligeramente en el tiempo. En general, la correlación cruzada es una herramienta muy útil en el procesamiento digital de señales, ya que permite identificar similitudes, detectar desfases y analizar relaciones temporales entre señales. En aplicaciones reales, este tipo de análisis se utiliza en áreas como señales biomédicas, telecomunicaciones y procesamiento de imágenes para encontrar patrones, sincronizar señales o identificar información relevante dentro de una señal.

**Parte C**

En esta parte de la práctica se trabajó con dos señales discretas: una señal coseno  y una señal seno , ambas con una frecuencia de 100 Hz y un periodo de muestreo de . Estas dos señales tienen la misma frecuencia y una forma muy parecida, pero no están alineadas exactamente en el tiempo, ya que el seno y el coseno tienen un desfase aproximado de 90°.

Para estudiar qué tan parecidas son estas señales se calculó la correlación cruzada, que es una herramienta del área de Procesamiento Digital de Señales. Esta técnica permite comparar dos señales mientras una de ellas se va desplazando en el tiempo, con el objetivo de encontrar en qué punto coinciden más.

Al realizar el cálculo se obtuvo una secuencia de valores que cambian dependiendo del retardo aplicado. Se observó que el valor máximo de correlación aparece aproximadamente cuando el retardo es , con un valor cercano a 3.5. Esto significa que cuando una señal se desplaza dos muestras con respecto a la otra, ambas coinciden mejor en su forma. Por otro lado, el valor mínimo aparece alrededor de , con un valor cercano a −3.5, lo que indica que en ese desplazamiento las señales presentan un comportamiento opuesto.

Al analizar la gráfica de la correlación también se puede notar que tiene una forma casi simétrica alrededor del origen. Además, cuando el retardo es cercano a cero, la correlación es aproximadamente igual a cero. Esto ocurre porque las funciones seno y coseno, aunque tienen la misma frecuencia, no coinciden exactamente cuando se comparan sin desplazamiento debido al desfase que existe entre ellas.

En general, este resultado muestra que las dos señales están relacionadas, pero desplazadas en el tiempo. Por medio de la correlación cruzada fue posible identificar ese desfase y observar en qué punto las señales presentan mayor similitud. Esto demuestra cómo esta herramienta es útil para analizar relaciones temporales entre señales en diferentes aplicaciones del procesamiento de señales.

