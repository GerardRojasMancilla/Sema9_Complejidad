# **Conceptos Básicos y Necesidad del MST**

Árbol de Expansión Mínima (Minimum Spanning Tree - MST) es un subgrafo acíclico y conexo de un
grafo no dirigido y ponderado G = (V, E) que conecta todos los vértices V utilizando exactamente |V| - 1
aristas, minimizando la suma total de los pesos de las aristas seleccionadas.

- **conexo** si todos los puntos están comunicados entre sí, ya sea de forma directa o indirecta.
- es **ponderado** (o valorado) cuando cada conexión (arista) tiene un número asignado, conocido como "peso" o "costo".

¿Qué necesidad fundamental resuelve el MST?

interconectar un conjunto de nodos al menor costo global posible sin generar redundancias (ciclos).

## Summary: 
* **MST es acíclico, conexo grafo no dirigido, ponderado** 

# **Estructura de Datos de Soporte: Union-Find (UFDS)**

Implementar de manera eficiente algoritmos de expansión como Kruskal, es indispensable contar con una
estructura de datos que gestione componentes conexos en tiempo casi constante. La estructura Union-Find
Disjoint Sets (UFDS) mantiene una colección de conjuntos disjuntos no solapados y resuelve el problema de
la conectividad dinámica. 

Mecanica de Operaciones Clave en Union-Find (UFDS):

• Find(i): Determina a qué conjunto pertenece el elemento i (sigue los punteros raíz). Permite verificar en tiempo
inmediato si dos vértices ya están conectados.

• Union(i, j): Une los conjuntos que contienen a los elementos i y j si pertenecen a componentes distintas.

• Optimizaciones (Weighted Union + Path Compression): Reducen la altura de las estructuras arbóreas,
logrando que las operaciones se ejecuten en tiempo amortizado casi constante O(α(N)), donde α es la función
inversa de Ackermann.

## Summary: 
* Conjunto disconjunto: elementos donde ningun elemento aparece en mas de un conjunto. Esto forma una Particion, cada elemento pertenece a su grupo y los grupos no se solapan
* Find(x) — Devuelve el representante del conjunto al que pertenece x. Ese representante identifica todo el grupo.
* Union(x, y) — Une los conjuntos que contienen a x y y, formando uno solo.

# **Algoritmos de Expansión Mínima: Kruskal y Prim**

**Algoritmo de Kruskal (Enfoque Centrado en Aristas)**

Kruskal algoritmo voraz (greedy) examinando las aristas del grafo de forma global. Ordena las aristas de menor a mayor peso 
y las agrega progresivamente al árbol de expansión, siempre que la
arista evaluada no forme un ciclo con las aristas ya seleccionadas. La detección de ciclos se realiza
eficientemente mediante la estructura Union-Find.

**Algoritmo de Prim (Enfoque Centrado en Vértices)**

Prim es un algoritmo voraz que construye el MST haciendo crecer un único árbol desde un vértice inicial
arbitrario. En cada paso, evalúa todas las aristas que conectan los vértices ya incluidos en el árbol con los
vértices no visitados, y selecciona la arista de menor peso utilizando una Cola de Prioridad (Min-Heap).

# **Cuadro Comparativo: Dijkstra vs. Kruskal vs. Prim**
A diferencia de Kruskal y Prim, que buscan conectar todos los nodos al menor costo total (MST), el Algoritmo
de Dijkstra resuelve el problema del Camino Más Corto desde un Origen (Single-Source Shortest Path), mide
distancias acumuladas desde la fuente y requiere que los pesos de las aristas sean no negativos.

# **Guía de Selección Práctica (¿Cuándo usar cuál?)**

**Criterios de Elección para Ingeniería de Algoritmos:**

1. Usa DIJKSTRA cuando: Necesites encontrar la ruta más corta o de menor costo entre dos puntos (o desde
una fuente a todos los destinos) en sistemas de navegación (GPS, Google Maps) o enrutamiento de red IP.
2. Usa KRUSKAL cuando: Necesites conectar una infraestructura completa al menor costo total y el grafo sea
disperso (pocas aristas en relación a los nodos). Su implementación con Union-Find es sumamente sencilla y
robusta.
3. Usa PRIM cuando: Necesites construir un MST y el grafo sea denso (muchas aristas en relación a los nodos),
o cuando se requiera expandir paulatinamente la red a partir de un nodo central predefinido.

