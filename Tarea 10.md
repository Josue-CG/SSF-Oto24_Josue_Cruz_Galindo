#EJEMPLO 6.1.1

from random import random
from math import sqrt

N = 1000000
count = 0
for j in range(N):
    point = (random(), random(), random())
    if point[0]*point[0]+point[1]*point[1]+point[2]*point[2]<1:
        count = count+1
Answer = float(count)/float(N)
Answer = Answer*4
from math import sqrt
print("The volume of a hemisphere of radius 1 is %0.4f +/− %0.4f ." % (Answer ,4*sqrt(N)/float(N)))

-----------------------------------------------------------------------------------------------------

# PROBLEMA 6-0

import numpy as np

# Definimos la función a integrar
def f(x):
    return np.sin(x)

# Parámetros de la simulación
N = 100000  # Número de puntos aleatorios
a = 0       # Límite inferior
b = np.pi   # Límite superior

# Generamos N puntos aleatorios en el intervalo [a, b]
x_random = np.random.uniform(a, b, N)

# Calculamos el valor de la función en esos puntos
f_values = f(x_random)

# Calculamos la integral usando la técnica de Monte Carlo
integral_monte_carlo = (b - a) * np.mean(f_values)

# Resultado real de la integral
integral_real = 2  # Integral de sin(x) de 0 a pi es 2

# Cálculo del error absoluto y relativo
error_absoluto = np.abs(integral_real - integral_monte_carlo)
error_relativo = error_absoluto / np.abs(integral_real)

# Cálculo de la incertidumbre (desviación estándar)
incertidumbre = np.std(f_values) * (b - a) / np.sqrt(N)  # Added * for multiplication

# Resultados
print(f"Resultado de la integral (Monte Carlo): {integral_monte_carlo}")
print(f"Resultado real de la integral: {integral_real}")
print(f"Error absoluto: {error_absoluto}")
print(f"Error relativo: {error_relativo}")
print(f"Incertidumbre: {incertidumbre}")

-----------------------------------------------------------------------------------------------------

# PROBLEMA 6-2

import numpy as np

def monte_carlo_4d_sphere(radius, num_samples):
    # Generar puntos aleatorios en un hipercubo de lado 2radius
    points = np.random.uniform(-radius, radius, (num_samples, 4))
    
    # Calcular cuántos puntos están dentro de la esfera 4D
    # Change points2 to points**2 and radius2 to radius**2 to square the values 
    inside_sphere = np.sum(np.sum(points**2, axis=1) <= radius**2)
    
    # Volumen del hipercubo
    volume_hypercube = (2 * radius)**4
    
    # Estimación del volumen de la esfera 4D
    volume_sphere = (inside_sphere / num_samples) * volume_hypercube
    
    # Relación para encontrar 'a'
    a = volume_sphere / (np.pi * radius**4)
    
    return a

# Parámetros
radius = 1.0  # Radio de la esfera
num_samples = 1000000  # Número de muestras

# Estimar 'a'
a_estimated = monte_carlo_4d_sphere(radius, num_samples)
print(f"Estimación de a: {a_estimated}")
