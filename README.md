# Exploración de Datos y Segmentación de Clientes — ConnectaTel

## 🎯 Objetivo del Proyecto
El objetivo principal de este proyecto es realizar un **Análisis Exploratorio de Datos (EDA)** y una **segmentación de usuarios** para la empresa de telecomunicaciones **ConnectaTel**. El análisis busca comprender los patrones de consumo de servicios (llamadas y mensajes de texto), identificar perfiles clave según su nivel de uso y grupo etario, detectar valores atípicos (*power users*) y proponer recomendaciones comerciales estratégicas para optimizar la oferta de planes de la compañía.

---

## 📊 Datasets Utilizados
El análisis se fundamenta en los siguientes conjuntos de datos:

1. **`users` (Perfil de Clientes):**
   * `user_id`: Identificador único del cliente.
   * `age`: Edad del usuario.
   * `plan`: Tipo de plan contratado (`Básico` o `Premium`).
   * `reg_date`: Fecha de registro en la plataforma.

2. **`usage` (Tráfico de Consumo):**
   * `user_id`: Identificador único del cliente.
   * `is_call` / `is_text`: Indicadores del tipo de servicio utilizado.
   * `duration`: Duración de la llamada en minutos (presenta valores `NaN` en registros de SMS por tratarse de un dato no aplicable, MAR).
   * `length`: Longitud en caracteres del mensaje enviado (presenta valores `NaN` en registros de llamadas por tratarse de un dato no aplicable, MAR).

---

## 🛠️ Etapas del Análisis Realizadas

1. **Limpieza y Preparación de Datos:**
   * Evaluación de valores nulos estructurales (`MAR`) y estandarización de tipos de datos.
   * Corrección de inconsistencias en fechas de registro (`reg_date`).
   * Agregación del tráfico de consumo por usuario (`usage_agg`) mediante *Named Aggregation*.
   * Fusión de tablas (`merge left`) con la base de usuarios e imputación de ceros para clientes sin consumo activo.

2. **Visualización de Distribuciones:**
   * Generación de histogramas comparativos por plan (`hue='plan'`) para evaluar la forma de las distribuciones (edad, cantidad de llamadas, minutos y mensajes).

3. **Detección y Tratamiento de Outliers:**
   * Identificación de valores atípicos mediante diagramas de caja (*Boxplots*).
   * Cálculo de límites superiores mediante el método del **Rango Intercuartílico (IQR)** ($Q3 + 1.5 \times IQR$).
   * Justificación de negocio para la conservación de los *power users* en el dataset.

4. **Segmentación de Clientes:**
   * **Por nivel de uso (`grupo_uso`):** Clasificación en *Bajo uso*, *Uso medio* y *Alto uso* según umbrales de llamadas y mensajes.
   * **Por rango de edad (`grupo_edad`):** Clasificación en *Joven*, *Adulto* y *Adulto Mayor*.
   * Visualización gráfica de las proporciones de cada segmento.

5. **Insight Ejecutivo:**
   * Traducción de hallazgos estadísticos en recomendaciones estratégicas sobre migración de planes (*up-selling*) y empaquetado de servicios.
