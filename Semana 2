import csv
import random
import faker

# Crear un generador de datos ficticios
fake = faker.Faker()

# Número de usuarios a generar
num_usuarios = 100000

# Crear lista de usuarios
usuarios = []

for i in range(num_usuarios):
    usuario = {
        'ID': i + 1,
        'nombre': fake.name(),
        'edad': random.randint(18, 90)  # Edad entre 18 y 90 años
    }
    usuarios.append(usuario)

# Guardar usuarios en un archivo CSV
with open('usuarios.csv', mode='w', newline='', encoding='utf-8') as archivo_csv:
    campos = ['ID', 'nombre', 'edad']
    writer = csv.DictWriter(archivo_csv, fieldnames=campos)

    writer.writeheader()
    for usuario in usuarios:
        writer.writerow(usuario)

print(f'Se han generado {num_usuarios} usuarios en el archivo usuarios.csv.')
