# 🏦 Análisis de Riesgo Crediticio Alemán (German Credit Risk)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Status](https://img.shields.io/badge/Status-Completado-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

## 📖 Descripción del Proyecto
Este proyecto desarrolla un pipeline de Machine Learning para predecir la probabilidad de incumplimiento de pago (default) en solicitantes de crédito. 

A diferencia de los enfoques estándar que solo buscan maximizar la precisión (accuracy), este proyecto se centra en **minimizar el costo financiero**. Se implementó una **Matriz de Costos de Negocio** personalizada donde el costo de un Falso Negativo (aprobar un mal crédito) es 5 veces mayor que el de un Falso Positivo (rechazar un buen crédito).

## 💼 Caso de Negocio y Matriz de Costos
El objetivo principal no es solo predecir bien, sino proteger el capital del banco. Basado en la documentación del dataset, se definieron los siguientes costos:

* **Falso Positivo (FP):** Costo = 1 (Pérdida de intereses por no dar el préstamo).
* **Falso Negativo (FN):** Costo = 5 (Pérdida del capital prestado).

El modelo óptimo es aquel que minimiza la función: 
$$Costo Total = (FP \times 1) + (FN \times 5)$$

## 📊 Dataset
Los datos provienen del repositorio UCI Machine Learning: **Statlog (German Credit Data)**.
* **Registros:** 1000 solicitantes.
* **Características:** 20 variables (7 numéricas, 13 categóricas).
* **Target:** `1` = Buen pagador, `2` = Mal pagador (recodificado a 0 y 1).

## 🛠️ Metodología y Pipeline
1.  **Preprocesamiento:**
    * Decodificación de variables categóricas para legibilidad.
    * Ingeniería de características (`installment_rate`, `credit_to_age`).
    * Codificación One-Hot y escalado estándar.
2.  **Modelado:**
    * Regresión Logística (con pesos de clase balanceados).
    * Random Forest.
    * XGBoost.
3.  **Optimización:**
    * Ajuste de hiperparámetros (GridSearch) utilizando el **Costo Financiero** como métrica de scoring personalizada.
    * Ajuste del umbral de decisión (Threshold Tuning).

## 📈 Resultados Clave

| Modelo | ROC-AUC (Test) | Costo Total (Negocio) | Observaciones |
| :--- | :---: | :---: | :--- |
| **Regresión Logística** | 0.81 | **107** | Mejor equilibrio costo/complejidad. |
| Random Forest | 0.80 | 107 | Buen desempeño, pero mayor costo computacional. |
| XGBoost | 0.78 | 277 | Requiere mayor ajuste de pesos por desbalance. |

> **Insight:** Se identificó que las variables `checking_status` (estado de cuenta) y `duration` (duración del crédito) son los predictores más fuertes del riesgo.

## 💻 Instalación y Uso

1. Clonar el repositorio:
   ```bash
   git clone [https://github.com/tu-usuario/german-credit-risk.git](https://github.com/tu-usuario/german-credit-risk.git)