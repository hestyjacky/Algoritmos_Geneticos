# 🚇 Metro Route Optimizer: Algoritmos Evolutivos Aplicados

## Proyecto

Este repositorio presenta un proyecto de optimización de rutas en la red de metro de Madrid utilizando dos metaheurísticas avanzadas: el **Algoritmo Genético (AG)** y el algoritmo de **Evolución Diferencial (ED)**. El objetivo es encontrar la ruta más eficiente entre dos puntos, minimizando una función de costo que penaliza la longitud del recorrido y el número de transbordos. El proyecto incluye dos implementaciones separadas, comparando su eficacia en la convergencia hacia el óptimo y su eficiencia en tiempo de ejecución.

## Funcionalidad Principal

El código está diseñado para simular un sistema de planificación de rutas inteligente. La funcionalidad central incluye:

1.  **Modelado del Grafo:** Conversión de un archivo de texto plano de la red de metro en un **grafo** no dirigido. Cada estación es un nodo y cada tramo de línea o transbordo es una arista, a la que se le asigna un peso.
2.  **Interfaz Interactiva (Jupyter/Colab):** Una interfaz de usuario simple para definir el punto de origen, destino, estaciones **obligatorias**, y estaciones **prohibidas**.
3.  **Optimización Evolutiva:** Aplicación del AG o ED para navegar el espacio de soluciones y encontrar la ruta que minimiza la penalización total (score).
4.  **Generación de Resultados:** Muestra la ruta óptima encontrada, la secuencia de acciones (subir, seguir, transbordar), el **tiempo de ejecución**, y el **mejor *score* de aptitud**.

## Implementación del Algoritmo Genético (AG)

El archivo `Rutas_del_metro_A_Genetico` implementa el algoritmo genético tradicional.

* **Representación:** Cada individuo (cromosoma) es una lista de estaciones que forman una ruta potencial.
* **Aptitud (*Fitness*):** Se utiliza una función de aptitud que penaliza el *score* en base a:
    * La **longitud** de la ruta (número de estaciones).
    * El **número de transbordos** (cambios de línea).
    * Violaciones de las restricciones (p. ej., pasar por una estación prohibida).
* **Operadores:** Utiliza operadores clásicos de AG, incluyendo:
    * **Selección por Torneo:** Para elegir a los mejores individuos.
    * **Cruce (Crossover):** Intercambio de segmentos de ruta en un punto en común (o un punto aleatorio).
    * **Mutación:** Inserción de un sub-camino aleatorio o re-cableado de un segmento de la ruta.

## Implementación de Evolución Diferencial (ED)

El archivo `Rutas_del_metro_Differential_Evolution` implementa la optimización mediante Evolución Diferencial, un método metaheurístico robusto para la optimización global.

* **Mutación Vectorial:** La característica distintiva de ED es cómo crea nuevos individuos: muta a un individuo base utilizando la diferencia vectorial entre otros dos individuos de la población.

$$
\mathbf{v}_i(G+1) = \mathbf{x}_{r_1}(G) + F \cdot (\mathbf{x}_{r_2}(G) - \mathbf{x}_{r_3}(G))
$$
* **Cruce Binomial:** Combina los elementos del vector mutante ($\mathbf{v}$) con el vector objetivo ($\mathbf{x}$) para formar un vector de prueba, introduciendo una mayor exploración en el espacio de soluciones en comparación con el AG simple.
* **Selección:** El individuo de prueba solo reemplaza al objetivo si su aptitud es mejor, garantizando un progreso continuo.

## 🗺️ Mapa de la Red de Metro

El proyecto se basa en la topología de la red de Metro de Madrid, incluyendo todas sus líneas y estaciones de transbordo.

![Plano del Metro de Madrid - 2000](Plano-Metro-de-Madrid-diciembre-de-2000-1.jpg)

## 📊 Comparativa de Rendimiento
La tabla compara la eficiencia de los dos algoritmos evolutivos, resaltando que la diferencia en el tiempo de ejecución es una consecuencia directa de la complejidad de sus operadores matemáticos.

| Métrica | Algoritmo Genético (AG) | Evolución Diferencial (ED) | Observación Clave |
| :--- | :--- | :--- | :--- |
| **Tiempo de Ejecución** | **Más eficiente/Rápido.** Sus operadores (cruce de puntos) son sencillos. | **Menos eficiente/Lento.** Sus procedimientos de mutación son vectoriales y matemáticamente más complejos por individuo. | La diferencia de tiempo se debe a la **naturaleza de los operadores**, no a la calidad de la solución. |
| **Calidad de Solución** | **Score óptimo.** | **Score óptimo.** | Ambos métodos son igualmente **eficaces** en encontrar el óptimo global en los escenarios probados. |
| **Convergenica** | Robusta. | Robusta. | Ambos lograron mejorar el *score* inicial subóptimo en los escenarios complejos. |


## 🛠️ Requisitos e Instalación

Para ejecutar los *notebooks* o scripts, necesitarás:

```bash
pip install networkx pandas ipywidgets matplotlib
