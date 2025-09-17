# Diagrama de Flujo - Pipeline Normativos SII

## 🔄 Flujo de Operación del Sistema Batch

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           PIPELINE NORMATIVOS SII                              │
│                         Sistema de Indexación Automatizada                     │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                INICIO DEL SISTEMA                              │
│  ./start.sh → Verificación → Compilación → Inicio → Pruebas Automáticas      │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              PROCESO DE INDEXACIÓN                             │
│                                                                                 │
│  ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Escaneo   │───▶│  Procesamiento │───▶│ Extracción  │───▶│  Indexación │     │
│  │ Directorio  │    │   en Chunks   │    │   Texto     │    │   Lucene    │     │
│  │ (104 PDFs)  │    │   (10 arch.)  │    │  (PDFBox)   │    │ (Índice Inv.)│     │
│  └─────────────┘    └──────────────┘    └─────────────┘    └─────────────┘     │
│                                                                                 │
│  ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Logging   │    │   Manejo de  │    │ Estadísticas │    │ Validación  │     │
│  │ Detallado   │    │   Errores    │    │ Procesamiento│    │ Integridad  │     │
│  └─────────────┘    └──────────────┘    └─────────────┘    └─────────────┘     │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              SISTEMA OPERATIVO                                 │
│                                                                                 │
│  ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   API REST  │    │   Swagger    │    │ Health      │    │ Monitoreo   │     │
│  │ (Puerto     │    │     UI       │    │ Checks      │    │ Logs        │     │
│  │   8081)     │    │              │    │             │    │             │     │
│  └─────────────┘    └──────────────┘    └─────────────┘    └─────────────┘     │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              CAPACIDADES DE BÚSQUEDA                           │
│                                                                                 │
│  ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ Búsqueda    │───▶│ Procesamiento│───▶│ Ranking por │───▶│ Resultados  │     │
│  │ Full-Text   │    │   Consulta   │    │ Relevancia  │    │ Estructurados│     │
│  │             │    │              │    │             │    │             │     │
│  └─────────────┘    └──────────────┘    └─────────────┘    └─────────────┘     │
│                                                                                 │
│  ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ Snippets    │    │ Filtros por │    │ Paginación  │    │ Metadatos   │     │
│  │ Texto       │    │ Metadatos    │    │ Resultados  │    │ Documentos  │     │
│  └─────────────┘    └──────────────┘    └─────────────┘    └─────────────┘     │
└─────────────────────────────────────────────────────────────────────────────────┘
```

## 🎯 Flujo de Comandos de Usuario

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              COMANDOS DE USUARIO                                │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                    ┌───────────────────┼───────────────────┐
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │   Inicio       │  │   Indexación    │  │   Búsqueda      │
        │   Sistema       │  │   Documentos    │  │   Contenido     │
        │                 │  │                 │  │                 │
        │ ./start.sh      │  │ POST /api/batch │  │ GET /api/indexing│
        │                 │  │ /index-documents│ │ /search?query=  │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │ Verificación    │  │ Procesamiento   │  │ Resultados      │
        │ Prerrequisitos  │  │ Masivo          │  │ Estructurados    │
        │ Compilación     │  │ Logging         │  │ Snippets        │
        │ Inicio App      │  │ Estadísticas    │  │ Ranking         │
        │ Pruebas Auto    │  │ Manejo Errores  │  │ Metadatos       │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
```

## 🔧 Flujo de Administración

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                            ADMINISTRACIÓN DEL SISTEMA                          │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                    ┌───────────────────┼───────────────────┐
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │   Detención     │  │   Monitoreo     │  │   Mantenimiento │
        │   Sistema       │  │   Estado        │  │   Índice        │
        │                 │  │                 │  │                 │
        │ ./stop.sh       │  │ ./comandos_utiles│ │ Re-indexación  │
        │ ./kill-app.sh   │  │ .sh status      │  │ Optimización    │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │ Liberación      │  │ Verificación    │  │ Limpieza        │
        │ Puerto 8081     │  │ Procesos        │  │ Logs Antiguos   │
        │ Limpieza        │  │ Health Checks   │  │ Actualización   │
        │ Procesos        │  │ Métricas        │  │ Seguridad       │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
```

## 📊 Flujo de Datos

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                FLUJO DE DATOS                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                    ┌───────────────────┼───────────────────┐
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │   Entrada       │  │   Procesamiento │  │   Salida        │
        │   Datos         │  │   Datos         │  │   Datos         │
        │                 │  │                 │  │                 │
        │ PDF Files       │  │ Text Extraction │  │ Lucene Index    │
        │ (104 archivos)  │  │ Metadata        │  │ Search Results  │
        │ Metadata        │  │ Indexing        │  │ API Responses   │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │ Validación      │  │ Transformación  │  │ Formateo        │
        │ Formato PDF     │  │ Campos Lucene   │  │ JSON Responses  │
        │ Tamaño Archivo  │  │ Deduplicación   │  │ Snippets        │
        │ Integridad      │  │ Optimización    │  │ Metadatos       │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
```

## 🚀 Flujo de Rendimiento

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                              RENDIMIENTO DEL SISTEMA                           │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                    ┌───────────────────┼───────────────────┐
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │   Indexación    │  │   Búsqueda      │  │   Sistema       │
        │   Rendimiento   │  │   Rendimiento   │  │   Rendimiento   │
        │                 │  │                 │  │                 │
        │ 104 docs/18s    │  │ <100ms queries  │  │ 200MB RAM      │
        │ 10 docs/chunk   │  │ Ranking auto    │  │ Port 8081       │
        │ ~50KB/doc       │  │ Snippets        │  │ Persistent idx  │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │ Optimización    │  │ Cache Results   │  │ Monitoring       │
        │ Chunking        │  │ Query Parsing   │  │ Health Checks   │
        │ Error Handling  │  │ Result Pagination│  │ Logging         │
        │ Progress Logs   │  │ Metadata Filter │  │ Metrics          │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
```

## 🔄 Ciclo de Vida del Sistema

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                            CICLO DE VIDA COMPLETO                              │
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                    ┌───────────────────┼───────────────────┐
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │   Inicio        │  │   Operación     │  │   Mantenimiento │
        │   Sistema        │  │   Continua      │  │   Sistema       │
        │                 │  │                 │  │                 │
        │ 1. Verificación │  │ 1. Búsquedas    │  │ 1. Re-indexación│
        │ 2. Compilación  │  │ 2. API Calls   │  │ 2. Optimización │
        │ 3. Inicio App   │  │ 3. Monitoring   │  │ 3. Limpieza     │
        │ 4. Pruebas     │  │ 4. Logging      │  │ 4. Actualización │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
                    │                   │                   │
                    ▼                   ▼                   ▼
        ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
        │ Estado: Listo   │  │ Estado: Activo  │  │ Estado: Mantenido│
        │ Puerto: Libre   │  │ Puerto: 8081    │  │ Puerto: 8081    │
        │ Índice: Cargado │  │ Índice: Activo  │  │ Índice: Actualizado│
        │ API: Disponible │  │ API: Operativa  │  │ API: Operativa  │
        └─────────────────┘  └─────────────────┘  └─────────────────┘
```

---

*Diagramas generados para el sistema Pipeline Normativos SII*  
*Versión: 1.0*
