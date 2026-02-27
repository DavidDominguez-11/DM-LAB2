# DM-LAB2 - Algoritmos de Aprendizaje no Supervisado

**Universidad del Valle de Guatemala**  
Facultad de Ingeniería  
Departamento de Ciencias de la Computación  
CC3074 – Minería de Datos  
Semestre I – 2026

## 📋 Descripción

Este laboratorio implementa y analiza algoritmos de aprendizaje no supervisado aplicados a un dataset de películas (`movies_2026.csv`). Se exploran técnicas de clustering, reducción de dimensionalidad y reglas de asociación para descubrir patrones ocultos en los datos cinematográficos.

## 🎯 Objetivos

- Aplicar algoritmos de **clustering** (K-Means y Jerárquico) para segmentar películas
- Evaluar la calidad de clusters mediante métricas (Silhouette Score, Hopkins Statistic)
- Implementar **PCA** (Análisis de Componentes Principales) para reducir dimensionalidad
- Descubrir patrones mediante **Reglas de Asociación** (algoritmo Apriori)
- Interpretar y visualizar resultados de análisis no supervisado

## 📊 Dataset

**Archivo:** `movies_2026.csv`

**Variables utilizadas para clustering:**
- `popularity`, `budget`, `revenue`, `runtime`
- `voteAvg`, `voteCount`
- `genresAmount`, `productionCoAmount`, `productionCountriesAmount`
- `actorsAmount`, `castWomenAmount`, `castMenAmount`
- `releaseYear`

**Variables excluidas:** Identificadores, texto libre, variables con alta proporción de nulos

## 🛠️ Instalación

### 1. Crear entorno virtual

```powershell
python -m venv dm_lab2
```

### 2. Activar entorno

```powershell
.\dm_lab2\Scripts\Activate.ps1
```

### 3. Instalar dependencias

```powershell
pip install -r requirements.txt
```

### 4. Desactivar entorno (cuando termines)

```powershell
deactivate
```

## 📦 Dependencias

Las principales librerías utilizadas son:

- `pandas`, `numpy` - Manipulación de datos
- `matplotlib`, `seaborn` - Visualización
- `scikit-learn` - Clustering, PCA, preprocesamiento
- `scipy` - Clustering jerárquico
- `mlxtend` - Reglas de asociación (Apriori)
- `pyclustertend` - Hopkins statistic
- `factor_analyzer` - Test KMO y Bartlett para PCA
- `yellowbrick`, `umap`, `pyod` - Análisis adicionales

Ver archivo completo: [requirements.txt](requirements.txt)

## 🚀 Uso

Abrir y ejecutar el notebook principal:

```
lab02.ipynb
```

## 📁 Estructura del Proyecto

```
DM-LAB2/
│
├── lab02.ipynb           # Notebook principal con todo el análisis
├── test.ipynb            # Notebook de pruebas
├── movies_2026.csv       # Dataset de películas
├── requirements.txt      # Dependencias del proyecto
└── README.md            # Este archivo
```

## 🔍 Análisis Implementados

### 1. **Clustering**

#### K-Means
- Determinación del número óptimo de clusters (método del codo y silhouette)
- Implementación con k=6 clusters
- Silhouette Score: **0.3798**

#### Clustering Jerárquico
- Dendrograma para visualizar jerarquía
- Comparación con K-Means
- Silhouette Score: **0.3683**

#### Clusters Identificados (K-Means con k=6)

| Cluster | Nombre | % Películas | Características |
|---------|--------|-------------|-----------------|
| 0 | Cine Mainstream Establecido | 48.4% | Popularidad moderada, presupuesto medio, audiencia consolidada |
| 1 | Cine Independiente/Reciente | 46.1% | Baja popularidad, presupuesto mínimo, sin tracción aún |
| 2 | Blockbusters Virales | 0.04% | Popularidad extrema, alto presupuesto, éxitos virales |
| 3 | Blockbusters Clásicos | 3.5% | Alta popularidad, muy alto presupuesto y revenue |
| 4 | Producciones Fragmentadas | 0.5% | Coproducciones con múltiples compañías |
| 5 | Producciones Multinacionales | 1.4% | Coproducciones entre muchos países |

### 2. **PCA (Análisis de Componentes Principales)**

- Test de KMO y Bartlett para validar adecuación
- Reducción de 13 variables a componentes principales
- Visualización de varianza explicada
- Interpretación de componentes

### 3. **Reglas de Asociación (Apriori)**

#### Preprocesamiento
- Discretización de variables numéricas:
  - `popularity` → 4 categorías (baja/media/alta/viral)
  - `budget` → 5 categorías (cero/bajo/medio/alto/blockbuster)
  - `revenue` → 5 categorías
  - `voteAvg`, `voteCount`, `runtime` → categorías relevantes
  - `releaseYear` → eras cinematográficas

#### Ejecución Apriori
Se ejecutaron múltiples rondas con diferentes parámetros:

1. **Ronda 1:** Soporte=0.05, Confianza=0.7 (reglas muy frecuentes)
2. **Ronda 2:** Soporte=0.03, Confianza=0.6 (reglas moderadas)
3. **Ronda 3:** Soporte=0.01, Confianza=0.6 (reglas específicas)

#### Limpieza
Eliminación de variables redundantes que generaban ruido:
- `era_reciente` (muy frecuente)
- `votos_ninguno` / `sin_votos` (duplicadas)
- `un_genero` (poca discriminación)

### 4. **Métricas de Evaluación**

- **Silhouette Score:** Mide la cohesión y separación de clusters
- **Hopkins Statistic:** Evalúa tendencia al clustering de los datos
- **Método del Codo:** Determina k óptimo observando inercia
- **Lift, Support, Confidence:** Métricas para reglas de asociación

## 📈 Resultados Principales

✅ **K-Means superó al Clustering Jerárquico** (0.3798 vs 0.3683)  
✅ Se identificaron **6 segmentos bien diferenciados** de películas  
✅ El 94.5% de películas pertenecen a 2 grandes clusters (mainstream vs independiente)  
✅ Se descubrieron **reglas de asociación significativas** entre variables categorizadas  
✅ Variables redundantes eliminadas mejoraron la calidad de las reglas

## 💡 Insights Clave

- La mayoría de películas se dividen entre **mainstream establecido** e **independiente reciente**
- Existe un pequeño grupo élite de **blockbusters virales** (0.04%)
- Las **coproducciones internacionales** tienen características distintivas
- El año de lanzamiento y presupuesto son predictores fuertes de popularidad
- Las reglas de asociación revelan patrones entre género, época y éxito comercial

## 🤝 Contribuciones

Este es un proyecto académico. Para sugerencias o mejoras, contactar al equipo del curso.

## 📝 Licencia

Proyecto académico - Universidad del Valle de Guatemala © 2026
