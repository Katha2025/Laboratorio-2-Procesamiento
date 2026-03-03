# Laboratorio-2-Procesamiento

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


**3. Kathalina :**

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

<img width="618" height="729" alt="image" src="https://github.com/user-attachments/assets/076c096b-f186-448e-adb6-5dafbec3de8c" 

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









