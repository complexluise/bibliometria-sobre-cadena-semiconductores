# Bibliometría sobre Cadena de Semiconductores

Pipeline para el procesamiento de datos bibliométricos en la red comercial internacional de la cadena de suministro de microchips.

## Descripción

Este proyecto implementa un pipeline de datos para el análisis bibliométrico de publicaciones científicas relacionadas con la cadena de suministro de semiconductores y el comercio internacional. El pipeline consta de tres fases principales:

1. **Ingesta y carga inicial de datos**: Parseo y normalización de metadatos bibliográficos desde diferentes fuentes (BibTeX, CSV, JSON) y carga en una base de datos Neo4j.

2. **Enriquecimiento y actualización**: Consulta a APIs externas (Semantic Scholar, CrossRef, Scopus) para obtener metadatos adicionales como citas, referencias completas, ORCID de autores, y financiadores.

3. **Extracción de la red para análisis**: Generación de redes de co-citación, colaboración entre autores, colaboración entre instituciones, y co-ocurrencia de palabras clave para análisis posterior.

## Arquitectura

La arquitectura del sistema se compone de tres módulos principales:

1. **Módulo de Ingesta (consigue_los_articulos.py)**: Responsable de cargar datos desde diferentes fuentes y normalizarlos para su almacenamiento en Neo4j.

2. **Módulo de Enriquecimiento (enriquecimiento.py)**: Consulta APIs externas para obtener metadatos adicionales y actualizar la base de datos.

3. **Módulo de Análisis de Red (analisis_red.py)**: Extrae diferentes tipos de redes del grafo y las exporta para análisis posterior.

## Requisitos

- Python 3.12 o superior
- Neo4j Database (instalación local o en la nube)
- Claves de API para servicios externos (opcional):
  - Semantic Scholar API
  - Scopus API

## Instalación

1. Clonar el repositorio:
   ```
   git clone https://github.com/tu-usuario/bibliometria-sobre-cadena-semiconductores.git
   cd bibliometria-sobre-cadena-semiconductores
   ```

2. Instalar dependencias con Poetry:
   ```
   poetry install
   ```

3. Configurar variables de entorno para las claves de API (opcional):
   ```
   export SEMANTIC_SCHOLAR_API_KEY="tu_clave_api"
   export SCOPUS_API_KEY="tu_clave_api"
   export NEO4J_URI="bolt://localhost:7687"
   export NEO4J_USER="neo4j"
   export NEO4J_PASSWORD="tu_contraseña"
   ```

## Uso

El script principal `main.py` proporciona una interfaz de línea de comandos para ejecutar el pipeline completo o fases individuales:

### Ejecutar el pipeline completo:
```
python main.py --mode full
```

### Ejecutar solo la fase de ingesta de datos:
```
python main.py --mode ingest --input data/archivo.csv --file-type csv
```

### Ejecutar solo la fase de enriquecimiento:
```
python main.py --mode enrich
```

### Ejecutar solo la fase de análisis de red:
```
python main.py --mode analyze --network-type cocitation --output-dir resultados
```

### Opciones disponibles:
```
--mode: Modo de operación (ingest, enrich, analyze, full)
--input: Archivo o directorio de entrada
--file-type: Tipo de archivo (csv, bibtex, json)
--network-type: Tipo de red (cocitation, author, institution, keyword)
--min-weight: Peso mínimo para relaciones
--output-dir: Directorio para archivos de salida
--community-algorithm: Algoritmo de detección de comunidades
```

## Ejemplos de Uso

### Procesar un archivo CSV y generar una red de co-citación:
```
python main.py --mode full --input data/Citación\ semiconductores\ comercio\ internacional.txt --network-type cocitation --output-dir resultados
```

### Generar una red de colaboración entre autores:
```
python main.py --mode analyze --network-type author --output-dir resultados
```

### Generar una red de co-ocurrencia de palabras clave:
```
python main.py --mode analyze --network-type keyword --output-dir resultados
```

## Estructura del Proyecto

```
bibliometria-sobre-cadena-semiconductores/
├── data/                      # Datos de entrada
│   └── Citación semiconductores comercio internacional.txt
├── src/                       # Código fuente
│   ├── consigue_los_articulos.py  # Módulo de ingesta
│   ├── enriquecimiento.py     # Módulo de enriquecimiento
│   └── analisis_red.py        # Módulo de análisis de red
├── output/                    # Resultados generados
├── main.py                    # Script principal
├── pyproject.toml             # Configuración de Poetry
└── README.md                  # Documentación
```


