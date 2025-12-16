# 🗺️ Generador de Mapas Electorales – Segunda Vuelta Chile 2025

## Descripción general
Este repositorio contiene un conjunto completo de scripts en Python para generar mapas electorales altamente detallados y personalizables de Chile. El software está diseñado específicamente para analizar y visualizar los resultados de la segunda vuelta de las elecciones presidenciales chilenas de 2025 entre **Jeannette Jara** y **José Antonio Kast**.    
El sistema automatiza la creación de más de 20 tipos distintos de visualizaciones, incluyendo mapas regionales individuales, mapas de áreas metropolitanas, reportes estadísticos nacionales y una tabla de resultados para capitales regionales. Es una herramienta técnica dirigida a analistas de datos, investigadores en ciencias políticas y desarrolladores interesados en geomática y visualización de información electoral.  

>**Nota de contexto**:  
>La segunda vuelta presidencial de Chile en 2025 representó un escenario político altamente competitivo, con una participación ciudadana significativa que reflejó un electorado fragmentado y en transformación. Este proyecto ofrece una perspectiva geográfica detallada de esos resultados.  

## ✨ Características Principales
- **Cobertura Nacional Completa:** Generación de mapas para las 16 regiones administrativas de Chile, con manejo especial de áreas metropolitanas (Gran Santiago, Gran Valparaíso, Gran Concepción) y territorios insulares (Isla de Pascua, Archipiélago Juan Fernández).
- **Procesamiento de Datos Electorales:** Sistema robusto para importar, limpiar y normalizar datos de resultados electorales desde archivos CSV, con capacidad para manejar múltiples formatos y codificaciones.
- **Visualizaciones Múltiples:**
  - Mapas regionales con nombres de comunas y tamaños de fuente ajustados por región
  - Mapa de Chile dividido en tres zonas geográficas (Norte, Centro, Sur)
  - Mapas especializados de áreas metropolitanas
  - Reportes estadísticos nacionales y regionales
  - Tabla de resultados para capitales regionales
- **Sistema de Colores Personalizado:**: Implementación de una paleta de 13 colores `(COLORES_BALOTAJE)` que representa gradientes de diferencia porcentual entre candidatos, desde Kast +50% (azul oscuro) hasta Jara +50% (rojo intenso).
- **Georreferenciación Avanzada:** Integración con múltiples fuentes de datos geográficos, incluyendo capacidades de descarga automática y creación de datos básicos de emergencia.

## 🗺️ Fuentes de Datos Geográficos y Agradecimientos

El proyecto utiliza y agradece las siguientes fuentes de datos geográficos:

>**Aspecto Técnico:**
>El sistema implementa un algoritmo de recuperación gradual que primero busca archivos locales, luego descarga datos de repositorios en línea, y finalmente genera geometrías básicas de emergencia, asegurando funcionalidad incluso en entornos con conectividad limitada.

## 🛠️ Instalación y Configuración

### Requisitos Previos
- **Python 3.8+**
- **Sistema operativo:** Cualquier sistema compatible con Python (Windows, Linux, macOS)
- **Memoria RAM:** Mínimo 4GB recomendado (8GB para procesamiento óptimo)

### Instalación de Dependencias
```bash
# Clonar el repositorio
git clone https://github.com/adroguetth/Elecciones_Chile_SegundaVuelta_2025.git
cd Elecciones_Chile_SegundaVuelta_2025

# Instalar dependencias (se recomienda usar un entorno virtual)
pip install -r requirements.txt
```  
El archivo requirements.txt incluye:
- `geopandas>=0.14.0` - Análisis geoespacial
- `pandas>=2.0.0` - Manipulación de datos electorales
- `matplotlib>=3.7.0` - Generación de visualizaciones
- `shapely>=2.0.0` - Operaciones con geometrías
- `requests>=2.31.0` - Descarga de datos geográficos
- `Pillow>=10.0.0` - Procesamiento de imágenes (para reportes con fotos)

### Estructura de Datos Necesaria (pendiente)
```text
directorio_proyecto/
├── Generador_de_Mapas_Electorales.py
├── datos_electorales.csv          # Tus datos electorales
├── comunas_chile.geojson          # (Opcional) Datos geográficos locales
└── output/                        # Directorio para resultados
```  
## 📈 Uso del Sistema
### Formato de Datos Electorales (CSV)
Prepare un archivo CSV con los resultados electorales (99,97% de los votos contabilizados). El sistema detecta automáticamente variaciones de nombres de columnas:
```csv
comuna,region,jara_votos,kast_votos,jara_pct,kast_pct,emitidos_votos,blanco_votos,nulo_votos
Santiago,Metropolitana,150000,120000,55.5,44.5,270000,2000,3000
Valparaíso,Valparaíso,80000,75000,51.6,48.4,155000,1000,1500
```
**Columnas mínimas requeridas:** `comuna`, `jara_pct`, `kast_pct`

### Ejecución Básica
```bash
# Ejecutar con configuración por defecto
python Generador_de_Mapas_Electorales.py

# Especificar archivo CSV y directorio de salida
python Generador_de_Mapas_Electorales.py --csv "ruta/a/tus/datos.csv" --output "mis_mapas"

# Procesar solo regiones específicas
python Generador_de_Mapas_Electorales.py --regions "1,5,13"  # Tarapacá, Valparaíso, Metropolitana

# Procesar todas las regiones
python Generador_de_Mapas_Electorales.py --regions "all"
```
### Salida Generada
El sistema crea en el directorio de salida:
```text
mapas_regionales_completos/
├── REGION_01_Tarapaca_COMPLETO.png
├── REGION_05_Valparaiso_COMPLETO.png
├── REGION_13_Metropolitana_COMPLETO.png
├── GRAN_SANTIAGO_METROPOLITANO.png
├── GRAN_VALPARAISO_METROPOLITANO.png
├── GRAN_CONCEPCION_METROPOLITANO.png
├── CHILE_MAP_COMPLETO.png
├── REPORTE_NACIONAL_COMPLETO.png
├── REPORTE_GRAN_SANTIAGO_COMPLETO.png
├── TABLA_CAPITALES_REGIONALES.png
├── TABLA_CAPITALES_REGIONALES.csv
├── ISLA_DE_PASCUA_RAPA_NUI.png
├── ARCHIPIELAGO_JUAN_FERNANDEZ.png
├── datos_combinados.geojson
├── datos_combinados.csv
└── REPORTE_FINAL.txt
```

## 🏗️ Arquitectura del Sistema

### Módulos Principales
1. Carga de Datos Geográficos (cargar_datos_geograficos())
  -  Búsqueda jerárquica de fuentes de datos
  -  Descarga automática desde GitHub como fallback
  -  Generación de datos básicos de emergencia
2. Procesamiento Electoral (procesar_csv())
  - Detección automática de codificación
  - Normalización de nombres de columnas
  - Cálculo de diferencias porcentuales
  - Validación de rangos (0-100%)
3. Sistema de Visualización
  - **Mapas Regionales:** Grid layouts con estadísticas integradas
  - **Sistemas de Etiquetado:** Lógica adaptable al tamaño de comunas
  - **Paleta de Colores:** 13 niveles de diferencia electoral
4. Gestión de Output
  - Nomenclatura estandarizada de archivos
  - Formatos múltiples (PNG, GeoJSON, CSV, TXT)
  - Metadatos de generación automáticos
 
 ## 🎨 Personalización Avanzada
 ### Ajuste de Paleta de Colores
 Modifique la lista COLORES_BALOTAJE en el código para personalizar la escala:  
```python
COLORES_BALOTAJE = [
    '#0F2D5C',  # Kast +50% o más
    '#1A3D7C',  # Kast +40% a +50%
    '#2A58A6',  # Kast +30% a +40%
    '#3D76D1',  # Kast +20% a +30%
    '#5E91E8',  # Kast +10% a +20%
    '#8BB2F0',  # Kast +1% a +10%
    '#9CA3AF',  # Empate técnico (±1%)
    '#F8A0A0',  # Jara +1% a +10%
    '#F28787',  # Jara +10% a +20%
    '#E86969',  # Jara +20% a +30%
    '#DA4A4A',  # Jara +30% a +40%
    '#C92A2A',  # Jara +40% a +50%
    '#B91C1C',  # Jara +50% o más
]
```
### Configuración de Fuentes por Región
Ajuste tamaños de fuente para etiquetas de comunas en el diccionario `TAMANOS_FUENTE_REGION:`
```python
TAMANOS_FUENTE_REGION = {
    1: 9,   # Tarapacá
    2: 9,   # Antofagasta
    # ...
    13: 9,  # Metropolitana
    16: 9,  # Ñuble
}
```
### Definición de Áreas Metropolitanas
Extienda las listas de comunas para análisis metropolitanos:
```python
CONURBACION_SANTIAGO = [
    "Cerrillos", "Cerro Navia", "Conchalí", "El Bosque", "Estación Central",
    # ... 30+ comunas actuales
    # Agregue nuevas comunas aquí si es necesario
]
```
## 📄 Formatos de Salida y Metadatos
### Especificaciones Técnicas de Imágenes
| Tipo de Mapa | Dimensiones (píxeles) | DPI | Tamaño Aprox. | Características |
|--------------|--------------|--------------|--------------|--------------|
| Regional      | 5400×4200 - 5400×4800      | 300      | 3-5 MB     | 	Estadísticas integradas, leyenda      |
| Gran Santiago      | 	10800×9600      | 400      | 8-12 MB      | 	Máximo detalle, simbología expandida      |
| Nacional     | 6000×3600      | 300      | 2-4 MB      | Vista completa de Chile      |
| Reportes      | 8400×6000      | 300      | 4-7 MB      | Paneles múltiples, infografías      |

### Metadatos Automáticos
Cada visualización incluye automáticamente:
- Fecha y hora de generación
- Nombre de la región o reporte
- Fuente de datos electoral (basado en CSV de entrada)
- Referencia al proyecto

## 🔍 Métodos Analíticos
### Cálculo de Resultados Regionales


## ⚖️ Licencia y Atribuciones
Este proyecto se distribuye bajo licencia MIT.  
### Atribuciones requeridas:

## 📚 Recursos y Referencias (OK)
- [Mapas vectoriales de la BCN](https://www.bcn.cl/siit/mapas_vectoriales) - Shapefiles oficiales de Chile
- [Esri Demographics Chile](https://doc.arcgis.com/en/esri-demographics/latest/esri-demographics/chile.htm) - Estructura geográfica administrativa
- [Análisis político elección 2025](https://latinoamerica21.com/es/chile-entre-dos-vueltas-y-un-nuevo-mapa-electoral/) - Contexto electoral
- [Seguimiento de encuestas AS/COA](https://www.as-coa.org/articles/poll-tracker-chiles-2025-presidential-runoff) - Contexto pre-electoral

## 🐛 Solución de Problemas [OK]
### Problemas Comunes y Soluciones
| Problema  | Causa Probable | Solución     |
|----------|------|------------|
| "No hay datos electorales para X región"     | CSV no tiene datos o nombres no coinciden   | Verificar normalización de nombres de comunas    |
| Error de memoria   | Geometrías muy detalladas o muchas regiones   | Reducir DPI o procesar regiones por separado  |
| Mapa en blanco    | Error en carga de datos geográficos   | Verificar conexión a internet para descarga   |
| Colores incorrectos   | Datos fuera de rango (0-100%)   | Validar porcentajes en CSV de entrada   |
| Fuentes muy pequeñas/grandes    | Configuración regional no óptima   | Ajustar `TAMANOS_FUENTE_REGION`   |

### Obtención de Ayuda
1. Revisar el archivo `REPORTE_FINAL.txt` generado para estadísticas de procesamiento
2. Verificar que el CSV tenga al menos las columnas requeridas
3. Probar con una sola región primero `(--regions "13")`
4. Abrir un issue en GitHub con:
  - Fragmento del CSV (primeras 5 líneas)
  - Comando ejecutado
  - Mensaje de error completo
  - Sistema operativo y versión de Python
---
**Nota:** Este proyecto es una herramienta de análisis técnico. Los resultados deben interpretarse en su contexto político y social apropiado, considerando las complejidades del sistema electoral chileno y las transformaciones en su panorama político
