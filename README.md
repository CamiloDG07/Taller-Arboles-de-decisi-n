# Taller de clasificación con árboles de decisión

**Autor:** Camilo Andrés Díaz García

**Asignatura:** Inteligencia Artificial, Universidad Sergio Arboleda, Bogotá, 2026-2

## Descripción

Este taller formula un problema de clasificación, construye e interpreta un
árbol de decisión con el índice Gini y evalúa un clasificador con datos que no
se usaron en su ajuste. El trabajo tiene dos partes:

1. **Caso sintético de diamantes.** Con una tabla de 12 diamantes (quilates,
   profundidad y clase de corte, aceptable o excelente) se formula el problema,
   se elige la raíz comparando dos preguntas candidatas, se construye el árbol
   a mano, se escriben sus reglas, se clasifican cuatro casos nuevos y se
   calculan las métricas de una matriz de confusión hipotética.
2. **Implementación en Python.** Se verifica el cálculo manual con
   `scikit-learn` y se ejecuta un experimento con el conjunto Iris (150 flores,
   cuatro medidas, tres especies), con particiones estratificadas de
   entrenamiento, validación y prueba, tres árboles candidatos, una evaluación
   única en prueba y una comparación con una referencia de clase mayoritaria.
   También se mide el costo computacional (tiempo y peso) de los candidatos.

Los datos sintéticos están escritos dentro del cuaderno e Iris se carga con
`scikit-learn`, por lo que no hace falta descargar ningún archivo.

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `taller_arboles_decision.ipynb` | Cuaderno con los cálculos, el árbol, las métricas, el experimento con Iris y el costo computacional, con sus salidas |
| `informe/informe_taller_arboles.pdf` | Informe del taller con el procedimiento, los resultados y las conclusiones |
| `resultados/fig_01_datos_candidatas.png` | Datos sintéticos y preguntas candidatas |
| `resultados/fig_02_comparacion_gini.png` | Reducción de impureza de las candidatas y por umbral |
| `resultados/fig_03_arbol_manual.png` | Árbol construido a mano |
| `resultados/fig_04_mapa_decision.png` | Regiones de decisión y casos nuevos |
| `resultados/fig_05_metricas_hipoteticas.png` | Matriz de confusión y métricas del ejercicio de evaluación |
| `resultados/fig_06_clase_mayoritaria.png` | Modelo que siempre predice la clase mayoritaria |
| `resultados/fig_07_plot_tree_sintetico.png` | Árbol de `scikit-learn` sobre los 12 casos |
| `resultados/fig_08_iris_particiones.png` | Iris y particiones estratificadas |
| `resultados/fig_09_iris_candidatos.png` | Comparación de los tres candidatos |
| `resultados/fig_10_iris_prueba.png` | Evaluación en prueba y comparación con la referencia |
| `resultados/fig_11_iris_arbol_seleccionado.png` | Árbol seleccionado en Iris |
| `resultados/fig_12_costo_computacional.png` | Tiempo de ajuste, de predicción y peso de los modelos |

## Cómo ejecutar el cuaderno

1. Instalar las librerías: `pip install scikit-learn pandas matplotlib numpy jupyter`.
2. Abrir `taller_arboles_decision.ipynb` en Jupyter, VS Code o Google Colab.
3. Ejecutar todas las celdas en orden. Las figuras se guardan en la carpeta
   `resultados/`.

Todas las particiones y los modelos usan la semilla 42, por lo que los
resultados son reproducibles. Los tiempos de la sección de costo
computacional cambian de un equipo a otro.

## Metodología

1. **Formulación.** Unidad de observación, características, etiqueta y clases;
   revisión de la fuga de información y de la disponibilidad de los predictores.
2. **Raíz con Gini.** Impureza de la raíz y comparación ponderada de las
   preguntas `quilates <= 0,75` y `profundidad <= 63,5`.
3. **Árbol manual.** División adicional con puntos medios entre valores
   consecutivos, árbol de profundidad máxima 2, reglas por hoja y clasificación
   de los casos nuevos.
4. **Métricas.** Exactitud, precisión, recall y F1 con A como clase positiva,
   y revisión del caso de clase mayoritaria.
5. **Verificación en Python.** `DecisionTreeClassifier` con `criterion="gini"`,
   `max_depth=2` y `random_state=42` sobre los 12 casos.
6. **Experimento con Iris.** Particiones 60 / 20 / 20, candidatos con
   profundidad máxima 1, 3 y sin límite, selección por F1 macro de validación,
   evaluación única en prueba y comparación con `DummyClassifier`.

## Resultados principales

- La raíz elegida es `profundidad <= 63,5` (reducción de Gini de 0,2500, frente
  a 0,1286 de `quilates <= 0,75`), y la segunda pregunta es `quilates <= 0,50`.
- `scikit-learn` reproduce el árbol manual y las predicciones de los casos nuevos.
- En Iris, el árbol sin límite de profundidad obtuvo el mayor F1 macro de
  validación (0,9333) y en prueba alcanzó 0,9333 de exactitud y de F1 macro,
  frente a 0,3333 y 0,1667 de la referencia de clase mayoritaria.
