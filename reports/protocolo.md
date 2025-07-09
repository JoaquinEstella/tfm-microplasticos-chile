# Protocolo de Investigación: TFM Ricardo Estella

**Título Provisional:** Mapeo y predicción de ‘hotspots’ de microplásticos en las aguas costeras del Sistema de la Corriente de Humboldt (Chile) mediante datos abiertos y aprendizaje automático.

**Autor:** Ricardo Joaquin Estella Vilche
**Tutor:** Manuel Campoy Naranjo
**Fecha:** 11 de julio de 2025

---

### 1. Pregunta de Investigación Principal
*¿Qué variables físicas (oceanográficas, atmosféricas) y antropogénicas (socioeconómicas, geográficas), después de controlar explícitamente por los sesgos de muestreo inherentes a los datos publicados, explican y predicen mejor la distribución de concentraciones de microplásticos reportadas en las aguas costeras de Chile?*

### 2. Hipótesis
* **H1:** Se espera que la proximidad a desembocaduras de ríos con alto caudal y la densidad poblacional costera sean los predictores positivos más fuertes de la concentración de microplásticos.
* **H2:** Se espera que las variables de control de sesgo (e.g., distancia al centro de investigación marina más cercano) también muestren una fuerte importancia predictiva, validando la necesidad de este enfoque metodológico.
* **H3:** ... (añade otras hipótesis que tengas)

### 3. Fuentes de Datos
* **Variable Objetivo:** NOAA NCEI Marine Microplastics Database.
* **Predictores Físicos:** Copernicus Marine Service (corrientes), Copernicus CDS/ERA5 (vientos), DGA SNIH (caudales).
* **Predictores Antropogénicos:** Banco Mundial (gestión de residuos), GHSL/WorldPop (densidad poblacional), OpenStreetMap (distancia a puertos/ciudades).
* **Predictores de Sesgo:** Ubicación de principales centros de investigación marina en Chile.

### 4. Estrategia Metodológica
1.  **Ingeniería de Características:** Se crearán variables agregadas temporalmente (e.g., caudal promedio 7 días) y espacialmente (e.g., distancia a...). Se incluirán explícitamente las variables de control de sesgo.
2.  **Modelo:** Se entrenará un modelo de Gradient Boosting (CatBoost/XGBoost).
3.  **Validación:** Se usará un esquema de validación cruzada por bloques espaciales (`GroupKFold`) para obtener una estimación robusta del error del modelo en ubicaciones no vistas. El rendimiento se comparará con un modelo baseline simple.

### 5. Plan de Mitigación de Riesgos
* **Riesgo:** La API de la DGA es inestable. **Mitigación:** Descargar todos los datos históricos necesarios al principio del proyecto. El código incluirá manejo de errores para reintentar conexiones.
* **Riesgo:** La densidad de datos de NOAA es muy baja en ciertas regiones. **Mitigación:** Se documentará explícitamente el sesgo geográfico. Las predicciones en zonas sin datos se presentarán con un alto grado de incertidumbre, enmarcándolas como "áreas prioritarias para futuro muestreo".