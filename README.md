# 🗺️ Mapa Electoral Chile 2025 – Segunda Vuelta

## Descripción general

Este repositorio contiene un **script en Python de gran escala** destinado a generar **mapas electorales detallados de la Segunda Vuelta Presidencial de Chile 2025 (Jara vs Kast)**, incluyendo visualizaciones comunales, regionales, metropolitanas y reportes estadísticos avanzados.

El proyecto está diseñado para producir **salidas gráficas de alta calidad**, orientadas a análisis político-electoral, divulgación académica y visualización profesional de resultados.

## 🎯 Objetivos del proyecto

* Generar mapas comunales con **coloreado según diferencia porcentual de votos**
* Producir mapas regionales completos con:
  * Estadísticas agregadas
  * Gráficos comparativos
  * Leyendas y simbología detallada
* Crear mapas específicos para:
  * Gran Santiago
  * Gran Valparaíso
  * Gran Concepción
  * Isla de Pascua (Rapa Nui)
  * Archipiélago Juan Fernández
* Unificar datos geográficos y electorales provenientes de múltiples fuentes
* Manejar inconsistencias reales de datos (acentos, nombres, formatos, encoding)


## 🧠 Arquitectura general del script

El script `n2.py` está estructurado en **módulos lógicos claramente separados**, lo que facilita su mantenimiento pese a su tamaño (>3800 líneas):

1. **Configuración e imports**
2. **Constantes y diccionarios nacionales**
3. **Escalas de color electorales**
4. **Normalización de datos textuales**
5. **Carga de datos geográficos (GeoJSON / SHP / fallback)**
6. **Procesamiento de resultados electorales (CSV)**
7. **Unión espacial-electoral (merge geográfico)**
8. **Funciones de etiquetado cartográfico**
9. **Cálculos estadísticos regionales**
10. **Generación de mapas regionales completos**
11. **Mapas especiales (islas y áreas metropolitanas)**
12. **Exportación de imágenes finales**

Cada bloque está **aislado funcionalmente** y documentado internamente en el script.

---

## 📦 Dependencias

El proyecto requiere Python **3.9+** y las siguientes librerías:

* geopandas
* pandas
* numpy
* matplotlib
* shapely
* requests
* pillow

Instalación recomendada:

```bash
pip install geopandas pandas numpy matplotlib shapely requests pillow
```

> ⚠️ **Nota**: geopandas requiere dependencias del sistema (GDAL, Fiona). Se recomienda usar Anaconda o Miniconda.

---

## 📁 Estructura esperada del repositorio

```
📦 mapa-electoral-chile-2025
 ┣ 📜 n2.py
 ┣ 📜 README.md
 ┣ 📂 output/
 ┃   ┣ REGION_01_Tarapaca_COMPLETO.png
 ┃   ┣ REGION_13_Metropolitana_COMPLETO.png
 ┃   ┣ GRAN_SANTIAGO_METROPOLITANO.png
 ┃   ┗ ...
 ┗ 📂 data/ (opcional)
```

El script puede funcionar **sin carpeta `data`** descargando automáticamente los GeoJSON necesarios.

---

## 📊 Datos electorales (CSV)

El script acepta archivos CSV **flexibles**, tolerando múltiples variantes de nombres de columnas.

### Columnas mínimas requeridas

* `comuna`
* `jara_pct`
* `kast_pct`

### Columnas opcionales (mejoran precisión)

* `jara_votos`
* `kast_votos`
* `emitidos_votos`
* `blanco_votos`
* `nulo_votos`
* `region`

El sistema:

* Detecta encoding automáticamente
* Normaliza nombres
* Corrige decimales con coma
* Calcula métricas faltantes cuando es posible

---

## 🗺️ Datos geográficos

El script intenta cargar datos en el siguiente orden:

1. Archivos locales (`.geojson`, `.shp`)
2. Descarga automática desde GitHub (`caracena/chile-geojson`)
3. GeoJSON especial de Gran Santiago
4. **Fallback de emergencia** con geometrías simuladas

Esto garantiza que el script **siempre produzca salida**, incluso sin conexión estable.

---

## 🎨 Sistema de colores

La diferencia porcentual se define como:

```
Diferencia = Jara% - Kast%
```

* 🔴 Rojo → ventaja de Jara
* 🔵 Azul → ventaja de Kast
* ⚪ Gris → empate técnico

La escala es **continua y perceptualmente balanceada**, optimizada para lectura cartográfica.

---

## 📐 Mapas regionales completos

Cada mapa regional incluye:

* Mapa comunal coloreado
* Etiquetas adaptativas (nombres o números)
* Gráfico de barras con promedio regional
* Conteo de comunas ganadas
* Diferencia promedio
* Barra de color continua
* Simbología especial (cuando aplica)

Los mapas se exportan en **PNG 300 DPI**, listos para impresión o publicación.

---

## 🏙️ Áreas metropolitanas

Se generan mapas dedicados para:

* Gran Santiago
* Gran Valparaíso
* Gran Concepción

Estos mapas utilizan:

* Zoom específico
* Etiquetado especial
* Geometrías refinadas cuando están disponibles

---

## 🏝️ Islas

Las islas se tratan **por separado** para evitar distorsiones cartográficas:

* Isla de Pascua (Rapa Nui)
* Archipiélago Juan Fernández

Cada una cuenta con mapa independiente y escala adecuada.

---

## ▶️ Ejecución

Ejemplo básico:

```bash
python n2.py resultados.csv
```

El script crea automáticamente el directorio de salida y guarda todas las imágenes generadas.

---

## 🧪 Manejo de errores y robustez

El proyecto incluye:

* Manejo de CSV mal formados
* Normalización agresiva de texto
* Protección contra datos faltantes
* Fallbacks geográficos
* Logging informativo

Está pensado para **datos reales, imperfectos y heterogéneos**.

---

## 📄 Licencia

Definir según corresponda (MIT, GPL, CC, etc.).

---

## ✍️ Autoría

Proyecto desarrollado por **[Autor / Organización]**.

El volumen y nivel de detalle del script reflejan **horas de trabajo y validación empírica**, orientado a producir resultados confiables y visualmente rigurosos.

---

## 📌 Notas finales

Este README documenta el **100 % del comportamiento del sistema sin modificar el código**, respetando su integridad y diseño original.

Para cambios o extensiones, se recomienda mantener esta separación entre **lógica** y **documentación**.
