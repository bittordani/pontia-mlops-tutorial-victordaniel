# 🛠️ Proyecto DevOps con MLflow y Azure 🚀

Este repositorio contiene un proyecto DevOps / MLOps educativo cuyo objetivo es automatizar el ciclo completo de desarrollo, entrenamiento y despliegue de un modelo de Machine Learning utilizando:

GitHub Actions para CI/CD

MLflow para gestión del ciclo de vida del modelo

Docker para contenerización

Azure (ACR + ACI) para despliegue en la nube

FastAPI como servidor de predicciones

# 📦 Estructura del Proyecto

📁 .github/workflows      # Pipeline (integración continua, training modelo y cre imagen Docker con Api en Azure Container)

📁 data/                  # Este proyecto usa el dataset Adult Income del UCI Machine Learning Repository

📁 models/                # Modelos y artefactos generados

📁 model_tests/           # Tests automáticos del modelo

📁 deployment/            # Dockerfile y dependencias de despliegue

📁 scripts/               # Scripts auxiliares para el registro del modelo en MLflow

📁 src/                   # Código fuente de entrenamiento

📁 unit_test/             # Test de prueba del modelo


# ⚙️ Workflows CI/CD

El repositorio está configurado con tres pipelines automáticos:

✅ Integration (.github/workflows/integration.yml)

Ejecutado en Pull Requests

Corre los tests y muestra los resultados directamente en el PR

Asegura calidad antes de integrar código a main

🏗️ Build (.github/workflows/build.yml)

Entrena el modelo usando src/main.py

Guarda y registra artefactos en MLflow

Ejecuta tests de modelo (model_tests/)

Guarda el run_id para posterior despliegue

🚀 Deploy (.github/workflows/deploy.yml)

Construye imagen Docker con FastAPI

Sube la imagen a Azure Container Registry

Despliega la API a Azure Container Instances

Prueba automáticamente el endpoint /health

# 🔮 Endpoints de la API

Una vez desplegado, el modelo es accesible mediante una API REST:

Método

Ruta

Descripción

GET

/health

Verifica que la API está operativa

POST

/predict

Recibe datos y devuelve predicción

GET

/metrics

Estadísticas básicas del uso de la API

# 🌐 Variables de entorno usadas

Variable

Descripción

MLFLOW_TRACKING_URI

URL del servidor MLflow

MODEL_URI

Ruta del modelo en el registry (ej. models:/...)

AZURE_CREDENTIALS

Credenciales de Azure (JSON)

ACR_NAME, ACR_USERNAME...

Datos de login para Azure Container Registry

🧶 Cómo ejecutar localmente (entrenamiento)

## 📥 Dataset: Adult Income (UCI)
Este proyecto usa el dataset Adult Income del UCI Machine Learning Repository.

➤ En pipelines (CI/CD)
Durante la ejecución de las workflows (como build.yml), el dataset se descarga automáticamente o se recupera desde MLflow.

➤ En ejecución local
Si clonas el repositorio y quieres probarlo localmente, necesitas:

Crear el directorio data/raw/

Descargar los siguientes archivos manualmente:

adult.data

adult.test

Colocarlos en data/raw/

# Crear entorno virtual e instalar dependencias
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Entrenar el modelo
python src/main.py

🎓 Créditos

Este proyecto ha sido desarrollado como parte del máster en Inteligencia Artificial, Cloud Computing y DevOps.

#Autor: 
Víctor Daniel Martínez

🧐 ¿Qué he aprendido?

✔️ Integración continua (CI)✔️ Despliegue continuo (CD)✔️ Entrenamiento automático y registro de modelos✔️ Despliegue cloud con Azure y Docker✔️ MLOps con MLflow y APIs productivas
