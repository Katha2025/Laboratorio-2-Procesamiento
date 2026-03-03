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

<img width="618" height="729" alt="image" src="https://github.com/user-attachments/assets/076c096b-f186-448e-adb6-5dafbec3de8c" />



