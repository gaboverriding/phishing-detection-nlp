# Benchmark de Modelos Preentrenados de Hugging Face para Ciberseguridad

Repositorio técnico enfocado en la evaluación comparativa de arquitecturas Transformer (*Zero-Shot Classification*) aplicadas a la detección automatizada de correos electrónicos de phishing.

---

## 📋 Descripción del Proyecto
Este proyecto evalúa el rendimiento predictivo y la eficiencia computacional de tres modelos preentrenados de Hugging Face (`facebook/bart-large-mnli`, `MoritzLaurer/DeBERTa-v3-base-mnli-fever-anli` y `joeddav/xlm-roberta-large-xnli`) sobre un dataset estandarizado de ciberseguridad, utilizando métricas estándar (Accuracy, Precision, Recall, F1-Score) y tiempos de latencia en inferencia.

---

## 📁 Estructura del Repositorio
El proyecto se organiza bajo la siguiente estructura de directorios estándar:
```text
phishing-detection-nlp/
├── data/
│   └── phishing_eval_dataset.csv      # Dataset exportado y normalizado para el reporte
├── notebooks/
│   └── benchmark_phishing.ipynb       # Notebook completo de Google Colab
├── results/
│   └── SalidaAnalisisModelosPreEntrenados.png # Gráficas y tablas de resultados de la ejecución
├── requirements.txt                   # Dependencias automáticas del entorno de ejecución
└── README.md                          # Documentación principal del proyecto

---

## ⚙️ Entorno de Ejecución
El prototipo está diseñado para ejecutarse en la nube utilizando **Google Colab** con aceleración por hardware (**GPU T4**).

* **Librerías principales:**
  * `torch` (PyTorch)
  * `transformers` (Hugging Face)
  * `datasets`
  * `scikit-learn`
  * `pandas`
  * `matplotlib` / `seaborn`

Para instalar las dependencias exactas del entorno de pruebas:
```bash
pip install -r requirements.txt

---

## 📊 Resultados Principales

A continuación se detallan los resultados cuantitativos obtenidos tras la ejecución del notebook en el entorno de pruebas:

| Modelo | Accuracy (%) | Precision (%) | Recall (%) | F1-Score (%) | Latencia Promedio (ms) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **BART-Large** | ~52.0% | ~26.0% | ~10.0% | ~14.0% | ~218 ms[cite: 1] |
| **DeBERTa-v3-Base** | **~58.0%**[cite: 1] | **~44.0%**[cite: 1] | **~11.0%**[cite: 1] | **~18.0%**[cite: 1] | **~80 ms**[cite: 1] |
| **XLM-RoBERTa-Large** | ~52.0% | ~26.0% | ~10.0% | ~14.0% | ~136 ms[cite: 1] |

### Análisis Gráfico y Comportamiento del Modelo
* **Rendimiento Predictivo (Estrategia Zero-Shot):**
  * **DeBERTa-v3-Base** obtuvo el mejor desempeño global, alcanzando un **Accuracy del ~58%** y una **Precision del ~44%**, superando de forma clara a las demás arquitecturas[cite: 1].
  * **BART-Large** y **XLM-RoBERTa-Large** registraron un comportamiento equivalente con un **Accuracy del ~52%** y una **Precision del ~26%**[cite: 1].
  * El **Recall (~10-11%)** y el **F1-Score (~14-18%)** mostraron valores reducidos en los tres modelos, lo que evidencia una alta tasa inicial de falsos negativos bajo la estrategia de inferencia directa sin entrenamiento previo específico[cite: 1].

* **Eficiencia y Latencia en Inferencia (GPU T4):**
  * **DeBERTa-v3-Base** demostró ser la arquitectura más eficiente, con una latencia promedio de **~80 ms por muestra**[cite: 1].
  * **XLM-RoBERTa-Large** registró una latencia media de **~136 ms**, mientras que **BART-Large** resultó ser el modelo más pesado con **~218 ms por muestra**[cite: 1].

---

## 📌 Conclusiones

1. **Superioridad de DeBERTa-v3:** Se posiciona como el modelo óptimo al combinar la mayor precisión predictiva con el menor costo computacional y tiempo de respuesta en la GPU[cite: 1].
2. **Limitaciones del Zero-Shot en Ciberseguridad:** Los modelos basados en NLI genérico tienen dificultades para identificar patrones complejos de ingeniería social sin un entrenamiento específico en el dominio, lo que se refleja en un Recall bajo[cite: 1].
3. **Próximos Pasos:** Se recomienda realizar un ajuste fino (*fine-tuning*) supervisado de la capa superior utilizando el dataset exportado (`data/phishing_eval_dataset.csv`) para elevar significativamente las métricas de F1-Score antes de un despliegue operativo en un SOC (*Security Operations Center*).

