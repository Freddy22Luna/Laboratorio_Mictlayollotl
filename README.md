# Laboratorio_Mictlayollotl
Implementación de tres algoritmos de renderizado (Scanline, Ray Tracing y Oclusión Ambiental) sobre una misma escena 3D en una paleta de matices verdes y rojos, evaluando su calidad visual contra su tiempo de ejecución.

## Proceso de Desarrollo e Integración por Partes

El proyecto se construyó de forma modular en `index.html` mediante ramas individuales e integración por Pull Requests:

### 1. Estructura Base y Scanline (Integrante 1 - ALFREDO ISRAEL CARCAMO LUNA)
* **Rama:** `main`
* **Desarrollo:** Se diseñó la interfaz inicial en `index.html`, el módulo de matemáticas vectoriales (`Vec3`) y la definición de la escena compartida (cámara, fuente de luz puntual, plano base, un cubo y tres esferas en tonos rojos y verdes). Para el renderizado **Scanline**, se programó la teselación de las figuras a mallas de triángulos, la proyección en perspectiva 2D y el barrido horizontal de píxeles aplicando **Z-Buffer** para la profundidad y **sombreado plano (Flat Shading)** por cara.

### 2. Ray Tracing (Integrante 2 - Victor Alexis Martinez Ahuateno)
* **Rama:** `RayTracingVictor`
* **Desarrollo:** Sobre la misma escena base, se implementó el lanzamiento de rayos primarios desde la cámara por cada píxel y las funciones de intersección analítica exacta para esferas, plano y cubo (`intersectScene`). Se agregó el cálculo de **sombras duras** mediante rayos secundarios hacia la fuente de luz y **un rebote de reflejo especular** recursivo (`traceRay`).

### 3. Oclusión Ambiental (Integrante 3 - Manuel Mendoza Lopez)
* **Rama:** `feature/Oclusion-Manuel`
* **Desarrollo:** Se reutilizó la detección de intersecciones para calcular la accesibilidad de luz en cada punto visible de la superficie. Se programó un generador de direcciones aleatorias (`randomHemisphereDir`) que dispara $N$ rayos dentro del hemisferio orientado según la normal del punto, oscureciendo las uniones y esquinas según la proporción de rayos bloqueados. Se integró en pantalla el control para ajustar dinámicamente el número de muestras.

### 4. Medición y Comparación (Integrante 4 - Stephanie Reyes)
* **Rama:** `Laboratorio_Stephanie`
* **Desarrollo:** Se construyó el panel de control interactivo con el selector de técnica, el selector de resolución (`160x120`, `320x240`, `480x360`) y el botón de ejecución comparativa. Se instrumentó cada algoritmo con `performance.now()` para medir en milisegundos el costo de renderizado en tiempo real y volcar los resultados automáticamente en la tabla comparativa en pantalla.

---
### Capturas de pantalla
<img width="1159" height="571" alt="imagen" src="https://github.com/user-attachments/assets/c11034e6-13f5-42f3-92f6-a8a7ba05893f" />
<img width="1156" height="564" alt="imagen" src="https://github.com/user-attachments/assets/b485d9bc-3ee3-48b0-8e11-b8bc446062cd" />
<img width="1171" height="560" alt="imagen" src="https://github.com/user-attachments/assets/e2ecd062-b1ea-41a6-9706-76c929475f20" />


## Conclusión: Calidad vs. Tiempo de Render

1. **Scanline** ofrece el menor tiempo de respuesta (pocos milisegundos) porque proyecta geometría directamente al espacio 2D y solo evalúa profundidad en el Z-Buffer, siendo la opción adecuada cuando se prioriza el rendimiento en tiempo real sobre el realismo lumínico.
2. **Ray Tracing** logra un salto en calidad visual (bordes curvos exactos, sombras duras y reflejos entre objetos) con un incremento moderado de tiempo, ya que calcula intersecciones matemáticas por píxel y rayos secundarios de luz y reflexión.
3. **Oclusión Ambiental** genera las sombras de contacto y profundidad más suaves de las tres técnicas, pero es computacionalmente la más costosa en rendimiento debido a que multiplica las pruebas de intersección por la cantidad de muestras hemisféricas configuradas en cada píxel.
