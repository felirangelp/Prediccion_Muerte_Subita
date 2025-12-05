# 🚀 Guía de Inicio Rápido - Predicción de Muerte Súbita Cardíaca

Esta guía te llevará paso a paso para replicar el proyecto completo desde cero.

## 📋 Tabla de Contenidos

1. [Requisitos del Sistema](#requisitos-del-sistema)
2. [Instalación](#instalación)
3. [Descarga de Datasets](#descarga-de-datasets)
4. [Entrenamiento de Modelos](#entrenamiento-de-modelos)
5. [Evaluación](#evaluación)
6. [Generación de Dashboard](#generación-de-dashboard)
7. [Solución de Problemas](#solución-de-problemas)

---

## 📦 Requisitos del Sistema

### Software Necesario

- **Python 3.8+** (recomendado 3.10)
- **Git** para clonar el repositorio
- **Conexión a Internet** estable (para descargar datasets ~16.5 GB)

### Hardware Recomendado

- **RAM:** Mínimo 8 GB (recomendado 16 GB)
- **Disco:** ~20 GB libres
- **CPU:** Multi-core recomendado
- **GPU:** Opcional (optimizado para Apple Silicon M1/M2)

### Cuenta en PhysioNet

Necesitas una cuenta gratuita en [PhysioNet](https://physionet.org) para descargar los datasets.

1. Ve a https://physionet.org
2. Crea una cuenta gratuita
3. Completa el curso de certificación (requerido para descargar datos)

---

## 🔧 Instalación

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/felirangelp/Prediccion_Muerte_Subita.git
cd Prediccion_Muerte_Subita
```

### Paso 2: Crear Ambiente Virtual

**En macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

**En Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

### Paso 3: Instalar Dependencias

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

**Nota para usuarios de Mac M1/M2:**
Si tienes problemas con TensorFlow, instala las versiones específicas:
```bash
pip install tensorflow-macos tensorflow-metal
```

### Paso 4: Verificar Instalación

```bash
python -c "import numpy, pandas, sklearn, tensorflow; print('✅ Todas las dependencias instaladas correctamente')"
```

---

## 📥 Descarga de Datasets

Los datasets se descargan automáticamente desde PhysioNet. El proceso puede tomar 2-4 horas dependiendo de tu conexión.

### Opción A: Descarga Automática (Recomendada)

```bash
python scripts/descarga_persistente.py
```

Este script:
- ✅ Descarga los 3 datasets secuencialmente
- ✅ Verifica la integridad de cada archivo
- ✅ Reanuda automáticamente si se interrumpe
- ✅ Muestra progreso en tiempo real

### Opción B: Descarga Manual

Si prefieres descargar manualmente:

```bash
# 1. SDDB (Sudden Cardiac Death)
wget -r -N -c -np https://physionet.org/files/sddb/1.0.0/ -P datasets/sddb/

# 2. NSRDB (Normal Sinus Rhythm)
wget -r -N -c -np https://physionet.org/files/nsrdb/1.0.0/ -P datasets/nsrdb/

# 3. CUDB (Ventricular Tachyarrhythmia)
wget -r -N -c -np https://physionet.org/files/cudb/1.0.0/ -P datasets/cudb/
```

### Verificar Descarga

```bash
python scripts/verify_datasets.py
```

Deberías ver:
```
✅ SDDB: 23 registros encontrados
✅ NSRDB: 18 registros encontrados
✅ CUDB: 35 registros encontrados
```

---

## 🎓 Entrenamiento de Modelos

### Entrenar Todos los Modelos

```bash
python scripts/train_models.py \
    --train-all \
    --data-dir datasets/ \
    --models-dir models/
```

**Tiempo estimado:** 2-4 horas (depende del hardware)

### Entrenar Modelo Individual

**Modelo Sparse (Recomendado - Mejor rendimiento):**
```bash
python scripts/train_models.py \
    --model sparse \
    --data-dir datasets/ \
    --models-dir models/
```

**Modelo Hierarchical:**
```bash
python scripts/train_models.py \
    --model hierarchical \
    --data-dir datasets/ \
    --models-dir models/
```

**Modelo Hybrid:**
```bash
python scripts/train_models.py \
    --model hybrid \
    --data-dir datasets/ \
    --models-dir models/
```

### Entrenamiento Rápido (Solo Pruebas)

Para pruebas rápidas con menos datos:

```bash
python scripts/train_models.py \
    --train-all \
    --max-records 3 \
    --data-dir datasets/ \
    --models-dir models/
```

### Monitorear Progreso

En otra terminal:
```bash
python scripts/monitor_training.py
```

---

## 📊 Evaluación

### Evaluar Todos los Modelos

```bash
python scripts/evaluate_models.py \
    --models-dir models/ \
    --data-dir datasets/ \
    --output results/evaluation_results.pkl
```

### Ver Resultados

Los resultados se guardan en `results/evaluation_results.pkl` y también se muestran en consola:

```
📊 Resultados de Evaluación
==========================
Modelo Sparse:
  Accuracy: 94.2%
  AUC-ROC: 97.9%
  F1-Score: 94.2%

Modelo Hierarchical:
  Accuracy: 87.9%
  AUC-ROC: 86.7%
  F1-Score: 87.8%

Modelo Hybrid:
  Accuracy: 74.8%
  AUC-ROC: 85.9%
  F1-Score: 75.1%
```

---

## 📈 Generación de Dashboard

### Generar Dashboard Interactivo

```bash
python scripts/generate_dashboard.py \
    --output results/dashboard_scd_prediction.html \
    --models-dir models/ \
    --results-file results/evaluation_results.pkl
```

### Ver Dashboard

Abre el archivo generado en tu navegador:

```bash
# macOS
open results/dashboard_scd_prediction.html

# Linux
xdg-open results/dashboard_scd_prediction.html

# Windows
start results/dashboard_scd_prediction.html
```

### Publicar en GitHub Pages

Si quieres publicar el dashboard en GitHub Pages:

```bash
# Copiar dashboard a carpeta docs
cp results/dashboard_scd_prediction.html docs/index.html

# Commit y push
git add docs/index.html
git commit -m "Actualizar dashboard"
git push origin main
```

Luego configura GitHub Pages en Settings → Pages → Source: `/docs`

---

## 🔄 Pipeline Completo

Para ejecutar todo el proceso de una vez:

```bash
python scripts/run_complete_pipeline.py \
    --data-dir datasets/ \
    --models-dir models/ \
    --results-dir results/
```

Este comando ejecuta:
1. ✅ Entrenamiento de los 3 modelos
2. ✅ Evaluación completa
3. ✅ Generación de dashboard
4. ✅ Análisis completo

---

## 🐛 Solución de Problemas

### Error: "No module named 'wfdb'"

```bash
pip install wfdb==4.1.0
```

### Error: "TensorFlow no funciona en Mac M1"

```bash
pip uninstall tensorflow
pip install tensorflow-macos tensorflow-metal
```

### Error: "No hay espacio en disco"

Los datasets ocupan ~16.5 GB. Asegúrate de tener al menos 20 GB libres.

### Error: "PhysioNet requiere autenticación"

1. Verifica que tienes cuenta en PhysioNet
2. Completa el curso de certificación
3. Configura tus credenciales:
```bash
# Crear archivo .netrc en tu home
echo "machine physionet.org login TU_USUARIO password TU_PASSWORD" >> ~/.netrc
chmod 600 ~/.netrc
```

### Error: "Descarga interrumpida"

El script `descarga_persistente.py` reanuda automáticamente. Solo vuelve a ejecutarlo:

```bash
python scripts/descarga_persistente.py
```

### Modelo no converge

- Reduce el número de registros para pruebas: `--max-records 5`
- Verifica que los datasets estén completos
- Aumenta la memoria disponible

---

## 📚 Próximos Pasos

Una vez que tengas el proyecto funcionando:

1. **Explora el código:** Revisa `src/` para entender la implementación
2. **Experimenta:** Modifica hiperparámetros en los scripts
3. **Analiza resultados:** Revisa el dashboard y los reportes en `results/`
4. **Contribuye:** Abre issues o pull requests con mejoras

---

## 💡 Tips y Mejores Prácticas

1. **Usa ambiente virtual:** Siempre trabaja en un venv
2. **Monitorea recursos:** El entrenamiento puede ser intensivo
3. **Guarda checkpoints:** Los modelos se guardan automáticamente
4. **Revisa logs:** Los logs están en `logs/` para debugging
5. **Valida datos:** Siempre verifica los datasets antes de entrenar

---

## 📞 Obtener Ayuda

- **Issues:** Abre un issue en GitHub
- **Documentación:** Revisa `docs/` para más detalles
- **Código:** El código está bien comentado en `src/`

---

**¡Feliz experimentación! 🚀**

