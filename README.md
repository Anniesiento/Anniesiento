import matplotlib.pyplot as plt

# Crear el mapa base
fig, ax = plt.subplots(figsize=(10, 10))

# Dibujar el plano de la universidad (Ejemplo de cuadrícula)
for i in range(11):
    ax.plot([i, i], [0, 10], color='gray', linestyle='--', linewidth=0.5)
    ax.plot([0, 10], [i, i], color='gray', linestyle='--', linewidth=0.5)

# Añadir edificios principales
edificios = {
    'Edificio A': (2, 8),
    'Biblioteca': (5, 7),
    'Laboratorio de Computación': (8, 6),
    'Estacionamiento Norte': (3, 3),
    'Estacionamiento Sur': (7, 2),
    'Entrada Principal': (5, 1)
}

for nombre, coord in edificios.items():
    ax.plot(coord[0], coord[1], 's', markersize=10, label=nombre)
    ax.text(coord[0], coord[1] + 0.3, nombre, fontsize=9, ha='center')

# Añadir zonas de riesgo
zonas_riesgo = {
    'Zona de Riesgo Sísmico': [(1, 9), (2, 9), (2, 8), (3, 8)],
    'Zona de Inundación': [(6, 8), (7, 8), (7, 7), (8, 7)],
    'Riesgo de Incendio': [(4, 5), (5, 5), (5, 4), (6, 4)],
    'Área con Alta Tasa de Robos': [(7, 3), (8, 3), (8, 2), (9, 2)]
}

colores = {
    'Zona de Riesgo Sísmico': 'red',
    'Zona de Inundación': 'blue',
    'Riesgo de Incendio': 'yellow',
    'Área con Alta Tasa de Robos': 'black'
}

for nombre, poligono in zonas_riesgo.items():
    poligono.append(poligono[0])  # Cerrar el polígono
    xs, ys = zip(*poligono)  # Descomprimir la lista de puntos
    ax.fill(xs, ys, alpha=0.3, fc=colores[nombre], label=nombre)

# Añadir rutas de evacuación
rutas_evacuacion = [
    [(5, 1), (5, 5), (1, 9)],
    [(5, 1), (5, 5), (9, 9)]
]

for ruta in rutas_evacuacion:
    xs, ys = zip(*ruta)
    ax.plot(xs, ys, 'green', linestyle='-', linewidth=2, label='Ruta de Evacuación')

# Añadir puntos de encuentro
puntos_encuentro = [(1, 9), (9, 9)]

for punto in puntos_encuentro:
    ax.plot(punto[0], punto[1], 'go', markersize=12)
    ax.text(punto[0], punto[1] + 0.3, 'Punto de Encuentro', fontsize=9, ha='center')

# Configurar el gráfico
ax.set_xlim(0, 10)
ax.set_ylim(0, 10)
ax.set_title('Mapa de Riesgos - Universidad César Vallejo, Chimbote')
ax.set_xlabel('Metros')
ax.set_ylabel('Metros')
ax.legend()

# Mostrar el mapa
plt.show()
