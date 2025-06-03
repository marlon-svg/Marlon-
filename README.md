# Re-ejecutar tras reinicio de entorno

import random
import string
import timeit
from dataclasses import dataclass
from typing import List, Optional

# Representación del usuario usando dataclass
@dataclass
class Usuario:
    id: int
    nombre: str
    edad: int

# Generar nombre aleatorio
def generar_nombre(longitud=6):
    return ''.join(random.choices(string.ascii_lowercase, k=longitud)).capitalize()

# Generar 100,000 usuarios únicos con IDs aleatorios
def generar_usuarios(n=100000) -> List[Usuario]:
    ids = random.sample(range(n * 10), n)  # Asegura IDs únicos
    return [Usuario(id=ids[i], nombre=generar_nombre(), edad=random.randint(18, 80)) for i in range(n)]

# Búsqueda lineal
def busqueda_lineal(usuarios: List[Usuario], objetivo: int) -> Optional[Usuario]:
    for usuario in usuarios:
        if usuario.id == objetivo:
            return usuario
    return None

# Búsqueda binaria (requiere lista ordenada por ID)
def busqueda_binaria(usuarios: List[Usuario], objetivo: int) -> Optional[Usuario]:
    izquierda, derecha = 0, len(usuarios) - 1
    while izquierda <= derecha:
        medio = (izquierda + derecha) // 2
        if usuarios[medio].id == objetivo:
            return usuarios[medio]
        elif usuarios[medio].id < objetivo:
            izquierda = medio + 1
        else:
            derecha = medio - 1
    return None

# Preparar datos y medir tiempos
usuarios = generar_usuarios()
usuarios_ordenados = sorted(usuarios, key=lambda u: u.id)
objetivo_id = usuarios_ordenados[len(usuarios_ordenados) // 2].id  # ID en el medio

# Medir tiempos
tiempo_lineal = timeit.timeit(lambda: busqueda_lineal(usuarios, objetivo_id), number=10)
tiempo_binaria = timeit.timeit(lambda: busqueda_binaria(usuarios_ordenados, objetivo_id), number=10)

import pandas as pd
import ace_tools as tools

# Mostrar resultados
df_resultados = pd.DataFrame({
    "Método": ["Búsqueda Lineal", "Búsqueda Binaria"],
    "Tiempo (s) en 10 ejecuciones": [tiempo_lineal, tiempo_binaria]
})

tools.display_dataframe_to_user(name="Comparación de Tiempos de Búsqueda", dataframe=df_resultados)
