# Proyecto Modelos Estocásticos: Gestión de Data Center

Este proyecto implementa diversos modelos estocásticos para la gestión inteligente de centros de datos, explorando diferentes enfoques de optimización y toma de decisiones bajo incertidumbre.

## Descripción General

El proyecto aborda el problema de gestión de recursos en un data center utilizando cuatro enfoques diferentes basados en procesos estocásticos:

1. **MDP Básico** - Proceso de Decisión de Markov completo
2. **Algoritmos de Value & Policy Iteration** - Métodos de programación dinámica
3. **Multi-Armed Bandits** - Exploración vs. explotación de servidores
4. **POMDP** - Procesos con observabilidad parcial

## Estructura del Proyecto

```
ProyectoEstocasticos/
│
├── Escenario_1_MDP_Basico.ipynb
│   └── MDP completo para gestión de data center
│
├── Algoritmos_de_Value_Policy_Iteration.ipynb
│   └── Implementación de algoritmos de programación dinámica
│
├── Escenario_3_Bandits.ipynb
│   └── Modelo de multi-armed bandits para selección de servidores
│
└── POMDP_para_observabilidad_parcial.ipynb
    └── Procesos de decisión con información incompleta
```

## Descripción de Notebooks

### 1. Escenario 1: MDP Básico (`Escenario_1_MDP_Basico.ipynb`)

Implementa un **Proceso de Decisión de Markov (MDP)** completo para gestión de data center.

**Características:**
- **5 servidores** con estados multidimensionales (carga, temperatura, estado operativo)
- **3 tipos de solicitudes** con diferentes prioridades:
  - Alta: 20%
  - Media: 50%
  - Baja: 30%
- ⚡ **12 acciones posibles**: asignación a servidores, rechazo, mantenimiento, balanceo
- **Transiciones estocásticas**: fallos dependientes de temperatura (40-60%)
- **Recompensas complejas**: bonos por prioridad, penalizaciones por rechazo/fallo

**Algoritmos Implementados:**
- Value Iteration (convergencia en ~15-30 iteraciones)
- Policy Iteration (convergencia en ~6-10 iteraciones)
- Greedy Baseline (política simple para comparación)

**Escenario de Evaluación:**
- Tasa de llegada: **0.90 req/step** (alta presión)
- Probabilidad de fallo: **40-60%** según condiciones
- Simulación: **3000 pasos**
- Throughput esperado: **~99.7%**

---

### 2. Algoritmos de Value & Policy Iteration (`Algoritmos_de_Value_Policy_Iteration.ipynb`)

Implementación detallada de algoritmos de **programación dinámica** para optimización de asignación de solicitudes.

**Características del Sistema:**
- **50 servidores** disponibles
- **Carga máxima**: 10 unidades discretas por servidor
- **Factor de descuento** (gamma) para decisiones a largo plazo
- **Criterio de convergencia** (theta) para garantizar optimalidad

**Implementación:**
- Definición de estados y acciones
- Matrices de transición estocásticas
- Funciones de recompensa
- Algoritmos de Value Iteration y Policy Iteration
- Visualizaciones de convergencia y políticas óptimas

**Resultados:**
- Comparación de velocidad de convergencia
- Análisis de políticas óptimas
- Métricas de rendimiento del sistema

---

### 3. Escenario 3: Multi-Armed Bandits (`Escenario_3_Bandits.ipynb`)

Aborda el problema de **exploración vs. explotación** usando modelos de bandidos multi-brazo.

**Configuración:**
- **20 servidores** (20 brazos)
- **Modelo de recompensas**: Bernoulli (éxito = 1, fallo = 0)
- **Horizonte**: T = 1000 pasos por experimento
- **Repeticiones**: 300 corridas independientes

**Algoritmos Comparados:**

1. **Índice de Gittins** (caso base)
   - Método bayesiano óptimo
   - Cálculo de índices dinámicos

2. **Upper Confidence Bound (UCB)**
   - Balance optimista de exploración
   - Reducción de incertidumbre

3. **Thompson Sampling (Muestreo de Thompson)**
   - Enfoque bayesiano
   - Priors: Beta-Bernoulli (α=β=1)

**Métricas de Evaluación:**
- Arrepentimiento acumulado
- Recompensa acumulada
- Porcentaje de selección del brazo óptimo

**Objetivo:** Determinar la cantidad óptima de servidores a explotar y la mejor estrategia de selección.

---

### 4. POMDP para Observabilidad Parcial (`POMDP_para_observabilidad_parcial.ipynb`)

Implementa **Procesos de Decisión de Markov Parcialmente Observables** para escenarios donde el estado del sistema no es completamente observable.

**Características:**
- Información incompleta sobre el estado del sistema
- **Creencias** (belief states) sobre estados ocultos
- Modelo de observaciones probabilísticas
- Optimización bajo incertidumbre de información

**Utilidades Implementadas:**
- Medición de tiempos de ejecución (`time_it`)
- Cálculo de porcentaje de solicitudes servidas (`percent_served`)
- Tiempos de respuesta promedio (`avg_response_time`)
- Semilla aleatoria para reproducibilidad

**Componentes:**
- Simulador de POMDP
- Algoritmos de inferencia de creencias
- Políticas basadas en creencias
- Visualizaciones de evolución de creencias

**Aplicación:** Gestión de data center cuando no se tiene información completa sobre temperatura, carga o estado de los servidores.

---

## Requisitos

### Dependencias Principales

```python
numpy          # Cálculos numéricos y matrices
matplotlib     # Visualización de resultados
```

### Instalación

```bash
pip install numpy matplotlib
```

## Uso

### Ejecución de Notebooks

1. Clonar el repositorio:
```bash
git clone https://github.com/camunozv/ProyectoEstocasticos.git
cd ProyectoEstocasticos
```

2. Abrir Jupyter Notebook o VS Code con extensión de Python

3. Ejecutar los notebooks
