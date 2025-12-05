# 🫀 Predicción de Muerte Súbita Cardíaca mediante Análisis de Señales ECG

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PhysioNet](https://img.shields.io/badge/Data-PhysioNet-red.svg)](https://physionet.org)

Sistema avanzado de **Machine Learning** para la predicción temprana de muerte súbita cardíaca (SCD) mediante análisis de señales electrocardiográficas (ECG). Implementa tres modelos de aprendizaje automático basados en papers científicos de alto impacto.

## 🚀 Acceso Rápido

- **📊 [Ver Dashboard Interactivo](https://felirangelp.github.io/Prediccion_Muerte_Subita_ECG_v1/)** - Visualiza resultados, métricas y análisis completos
- **📖 [Guía Paso a Paso](https://github.com/felirangelp/Prediccion_Muerte_Subita/blob/main/QUICKSTART.md)** - Instrucciones detalladas para replicar el proyecto
- **💻 [Código Fuente](https://github.com/felirangelp/Prediccion_Muerte_Subita/tree/main/src)** - Implementación completa de los 3 modelos
- **🔧 [Scripts de Ejecución](https://github.com/felirangelp/Prediccion_Muerte_Subita/tree/main/scripts)** - Scripts listos para usar

## 🎯 Resultados Principales

| Modelo | Accuracy | AUC-ROC | F1-Score |
|--------|----------|---------|----------|
| **Sparse Representations** | **94.2%** | **97.9%** | **94.2%** |
| Hierarchical Fusion | 87.9% | 86.7% | 87.8% |
| Hybrid Model | 74.8% | 85.9% | 75.1% |

## 📊 Dashboards Interactivos

### 🔗 [Acceder a los Dashboards](https://felirangelp.github.io/Prediccion_Muerte_Subita/)

**El dashboard está disponible en GitHub Pages** e incluye:
- ✅ Análisis comparativo de los 3 modelos
- ✅ Métricas de rendimiento detalladas (Accuracy, AUC-ROC, F1-Score)
- ✅ Visualizaciones temporales por intervalos pre-SCD
- ✅ Análisis de importancia de características
- ✅ Comparación con literatura científica
- ✅ Gráficos interactivos con Plotly

**Nota:** Si el dashboard no carga, configura GitHub Pages en **Settings → Pages → Source: `/docs`**

## 🚀 Inicio Rápido

### 📋 Requisitos Previos

- Python 3.8 o superior
- ~20 GB de espacio en disco (para datasets)
- Conexión a internet estable
- Registro gratuito en [PhysioNet](https://physionet.org)

### ⚡ Instalación Paso a Paso

```bash
# 1. Clonar el repositorio
git clone https://github.com/felirangelp/Prediccion_Muerte_Subita.git
cd Prediccion_Muerte_Subita

# 2. Crear ambiente virtual
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Descargar datasets de PhysioNet
python scripts/descarga_persistente.py

# 5. Entrenar modelos
python scripts/train_models.py --train-all --data-dir datasets/ --models-dir models/

# 6. Evaluar modelos
python scripts/evaluate_models.py --models-dir models/ --data-dir datasets/

# 7. Generar dashboard
python scripts/generate_dashboard.py --output results/dashboard_scd_prediction.html
```

### 📖 Guía Completa

**Para instrucciones detalladas paso a paso, consulta: [QUICKSTART.md](QUICKSTART.md)**

La guía incluye:
- ✅ Instalación detallada
- ✅ Descarga de datasets
- ✅ Entrenamiento de modelos
- ✅ Evaluación y métricas
- ✅ Generación de dashboard
- ✅ Solución de problemas

## 🔬 Modelos Implementados

### 1. Representaciones Dispersas (Sparse Representations)
- **Basado en:** Velázquez-González et al., Sensors 2021
- **Método:** Algoritmo OMP + k-SVD + SVM
- **Mejor rendimiento:** 94.2% accuracy
- **Código:** [`src/sparse_representations.py`](src/sparse_representations.py)

### 2. Fusión Jerárquica de Características (Hierarchical Fusion)
- **Basado en:** Huang et al., Symmetry 2025
- **Método:** TCN + DFA2 + Fusión multi-escala
- **Rendimiento:** 87.9% accuracy
- **Código:** [`src/hierarchical_fusion.py`](src/hierarchical_fusion.py)

### 3. Modelo Híbrido
- **Método:** Combinación innovadora de ambos métodos usando wavelets
- **Rendimiento:** 74.8% accuracy
- **Código:** [`src/hybrid_model.py`](src/hybrid_model.py)

## 📚 Datasets Utilizados

| Dataset | Código | Pacientes | Duración | Frecuencia |
|---------|--------|-----------|----------|------------|
| **SDDB** | `sddb` | 23 (SCD) | 24h | 250 Hz |
| **NSRDB** | `nsrdb` | 18 (sanos) | ≥24h | 128 Hz |
| **CUDB** | `cudb` | 35 | Varios min | 250 Hz |

Todos los datasets son de acceso público en [PhysioNet](https://physionet.org).

## 📁 Estructura del Proyecto

```
Prediccion_Muerte_Subita/
├── 📄 README.md                    # Este archivo - Guía principal
├── 📄 QUICKSTART.md                # Guía paso a paso detallada
├── 📄 LICENSE                      # Licencia MIT
├── 📄 requirements.txt             # Dependencias Python
│
├── 💻 src/                         # CÓDIGO FUENTE - Implementación completa
│   ├── sparse_representations.py      # Modelo 1: Sparse (94.2% accuracy)
│   ├── hierarchical_fusion.py        # Modelo 2: Hierarchical (87.9% accuracy)
│   ├── hybrid_model.py               # Modelo 3: Hybrid (74.8% accuracy)
│   ├── preprocessing_unified.py      # Preprocesamiento de señales ECG
│   ├── pan_tompkins_complete.py      # Detección de ondas ECG
│   ├── tachogram_analysis.py         # Análisis de intervalos RR
│   └── utils.py                      # Utilidades y funciones auxiliares
│
├── 🔧 scripts/                      # SCRIPTS DE EJECUCIÓN
│   ├── train_models.py               # Entrenar los 3 modelos
│   ├── evaluate_models.py            # Evaluar modelos y métricas
│   ├── generate_dashboard.py         # Generar dashboard interactivo
│   ├── run_complete_pipeline.py      # Pipeline completo automatizado
│   ├── descarga_persistente.py       # Descargar datasets de PhysioNet
│   └── verify_datasets.py            # Verificar integridad de datasets
│
├── 📚 docs/                          # DOCUMENTACIÓN Y DASHBOARD
│   ├── index.html                    # Dashboard interactivo (GitHub Pages)
│   ├── DATASETS_INFO.md              # Información de datasets
│   └── ENTRENAMIENTO_MODELOS.md      # Detalles de entrenamiento
│
├── 📦 models/                        # Modelos entrenados (se generan)
├── 📊 results/                       # Resultados y reportes (se generan)
└── 💾 datasets/                      # Datasets (se descargan, no en repo)
```

### 🔍 Navegación Rápida

- **Ver código de implementación:** [`src/`](src/) - Todos los modelos están aquí
- **Ver scripts de ejecución:** [`scripts/`](scripts/) - Scripts listos para usar
- **Ver documentación:** [`docs/`](docs/) - Documentación técnica
- **Ver dashboard:** [GitHub Pages](https://felirangelp.github.io/Prediccion_Muerte_Subita/)

## 💻 Uso del Código

### Ver la Implementación

Todo el código fuente está disponible en la carpeta [`src/`](src/):

- **[`sparse_representations.py`](src/sparse_representations.py)** - Modelo de Representaciones Dispersas (mejor rendimiento)
- **[`hierarchical_fusion.py`](src/hierarchical_fusion.py)** - Modelo de Fusión Jerárquica
- **[`hybrid_model.py`](src/hybrid_model.py)** - Modelo Híbrido combinado
- **[`preprocessing_unified.py`](src/preprocessing_unified.py)** - Preprocesamiento de señales ECG

### Ejemplo: Usar un Modelo

```python
from src.sparse_representations import SparseRepresentationClassifier
from src.utils import load_ecg_record

# Cargar datos
signals, labels = load_training_data()

# Crear y entrenar modelo
model = SparseRepresentationClassifier(
    n_atoms=256,
    n_nonzero_coefs=10,
    svm_kernel='rbf'
)
model.fit(signals, labels)

# Guardar modelo
model.save('models/sparse_classifier.pkl')
```

### Ejemplo: Realizar Predicción

```python
# Cargar modelo entrenado
model = SparseRepresentationClassifier.load('models/sparse_classifier.pkl')

# Cargar señal ECG
signal, metadata = load_ecg_record('datasets/sddb/30')

# Predecir
prediction = model.predict(signal)
probability = model.predict_proba(signal)

print(f"Predicción: {'SCD' if prediction == 1 else 'Normal'}")
print(f"Probabilidad: {probability[0][1]:.2%}")
```

## 📊 Pipeline Completo

Para ejecutar todo el pipeline de una vez:

```bash
python scripts/run_complete_pipeline.py \
    --data-dir datasets/ \
    --models-dir models/ \
    --results-dir results/
```

Esto ejecuta:
1. ✅ Descarga de datasets (si no existen)
2. ✅ Entrenamiento de los 3 modelos
3. ✅ Evaluación con métricas completas
4. ✅ Generación de dashboard interactivo
5. ✅ Análisis completo con validación cruzada

## 🔍 Características Técnicas

- **Preprocesamiento:** Filtrado, normalización, detección de ondas (Pan-Tompkins)
- **Extracción de características:** Lineales, no lineales, multi-escala
- **Validación:** Validación cruzada 5-fold, paradigma inter-paciente
- **Visualización:** Dashboards interactivos con Plotly
- **Optimización:** Compatible con Apple Silicon M1/M2

## 📖 Documentación

- **[QUICKSTART.md](QUICKSTART.md)** - Guía paso a paso detallada
- **[docs/DATASETS_INFO.md](docs/DATASETS_INFO.md)** - Información de datasets
- **[docs/ENTRENAMIENTO_MODELOS.md](docs/ENTRENAMIENTO_MODELOS.md)** - Detalles de entrenamiento

## 📄 Referencias Científicas

1. **Velázquez-González et al.** (2021). "Prediction of Sudden Cardiac Death Using Machine Learning Techniques". *Sensors*, 21(7), 2366.

2. **Huang et al.** (2025). "Improving Early Prediction of Sudden Cardiac Death Risk via Hierarchical Feature Fusion". *Symmetry*, 17(1), 1738.

## 🤝 Contribuciones

Este es un proyecto académico desarrollado como Proyecto Final de Maestría en Inteligencia Artificial en la Pontificia Universidad Javeriana.

Las contribuciones son bienvenidas. Por favor:
1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la Licencia MIT. Ver [LICENSE](LICENSE) para más detalles.

## 👥 Autores

- **Felipe Rangel** - *Desarrollo e Implementación*
- **Nicolás Torres** - *Colaboración*

## 🙏 Agradecimientos

- **PhysioNet** por proporcionar los datasets de acceso público
- **Pontificia Universidad Javeriana** por el apoyo académico
- La comunidad de investigación en procesamiento de señales biomédicas

## 📧 Contacto

Para preguntas o colaboraciones, puedes abrir un issue en este repositorio.

---

**⭐ Si este proyecto te resulta útil, considera darle una estrella en GitHub**

