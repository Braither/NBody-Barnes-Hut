# Simulación gravitacional de N cuerpos con Barnes–Hut

Proyecto académico de simulación gravitacional de N cuerpos con masas positivas y negativas. El equipo adaptó código existente para incorporar el algoritmo Barnes–Hut en tres dimensiones y comparar su desempeño con el método directo.

El informe del proyecto, elaborado para el curso Herramientas Computacionales del Departamento de Física de la Universidad Nacional de Colombia, está disponible en [`docs/InformeFinalHerramientas.pdf`](docs/InformeFinalHerramientas.pdf). Sus autores son Braither Diaz Chiquillo, Edison Ortega Perenguez, Sergio Vargas Rodriguez y Juan Victorino Rojas.

## Trabajo y resultados

- Adaptación de código de simulación N-body existente e implementación de un Octree para aproximar las interacciones gravitacionales lejanas mediante el criterio de aceptación multipolar `theta`.
- Comparación del tiempo de ejecución del método Barnes–Hut con el método directo, usando las mismas condiciones de simulación.
- En las condiciones evaluadas, Barnes–Hut no fue más rápido que el método directo paralelizado. El informe discute como posibles causas el costo de construir y recorrer el árbol, la distribución inicial de partículas y que la versión Barnes–Hut no estaba paralelizada.
- La evaluación de precisión quedó limitada por los recursos computacionales disponibles; el informe propone optimizar y paralelizar el método y hacer una comparación de precisión más exhaustiva.

El informe incluye las referencias del código y los métodos en los que se basó el trabajo. Se conserva la licencia GPL-2.0 del código.

## Estructura

- `pipe.py`: punto de entrada que selecciona e inicializa una simulación, ejecuta la evolución N-body y genera imágenes y video. La opción inicial seleccionada es `halo`.
- `negmass_nbody/initialise/`: condiciones iniciales para halo y formación de estructura.
- `negmass_nbody/barnes/barnesHut.py`: clases `Node`, `Octree`, `Simulation` y `SimulationBody`.
- `negmass_nbody/simulate/sim.py`: evolución temporal con el método directo y con Barnes–Hut.
- `negmass_nbody/visualise/`: generación de figuras y video.
- `DATA/`: parámetros, archivos HDF5 de posición y velocidad y algunas imágenes de simulaciones.
- `docs/InformeFinalHerramientas.pdf`: informe académico del proyecto.

## Ejecución

Instala las dependencias de Python indicadas en [`requirements.txt`](requirements.txt) y ejecuta:

```bash
python pipe.py
```

El programa usa y genera archivos dentro de `DATA/`; haz una copia de los datos antes de experimentar. La opción `SPECIFY_SIM` en `pipe.py` selecciona el escenario inicial. La creación del video usa ImageMagick y el código espera encontrar `magick` en `/usr/local/bin/magick`, por lo que esa ruta puede requerir ajustes en otros equipos.
