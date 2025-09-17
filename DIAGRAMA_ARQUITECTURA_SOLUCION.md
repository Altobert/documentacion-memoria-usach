# 🏗️ DIAGRAMA DE ARQUITECTURA - SOLUCIÓN INFORMÁTICA INTEGRAL SII

## 📊 **Diagrama Principal de Arquitectura**

```mermaid
graph TB
    %% Usuario y Acceso
    U[👤 Usuario SII] --> F[🖥️ Frontend Vue.js<br/>Puerto 3000]
    
    %% Frontend
    F --> B[🔍 Backend Spring Boot<br/>Puerto 8081]
    F --> C[💬 Chat System Python<br/>Puerto 8000]
    
    %% Backend Components
    B --> L[📚 Apache Lucene<br/>Índice Invertido]
    B --> P[📄 Apache PDFBox<br/>Extracción Texto]
    
    %% Chat System Components
    C --> G[🤖 Groq Cloud<br/>LLM Llama-3.3-70B]
    C --> CA[💾 Cache CAG<br/>Documentos Procesados]
    C --> LC[🔗 LangChain<br/>Gestión Prompts]
    
    %% Pipeline Automático
    D[📁 Documentos PDF SII<br/>104 archivos] --> PA[⚙️ Pipeline Automático<br/>Procesamiento Batch]
    PA --> B
    PA --> C
    
    %% Almacenamiento
    L --> FS[💿 Filesystem<br/>Índice Persistente]
    CA --> MEM[🧠 Memoria<br/>Cache Sesiones]
    
    %% APIs y Servicios
    B --> API1[🌐 API REST<br/>Búsqueda Full-Text]
    C --> API2[🌐 API REST<br/>Chat Contextual]
    
    %% Documentación
    API1 --> SW1[📖 Swagger UI<br/>Documentación API]
    API2 --> SW2[📖 Swagger UI<br/>Documentación API]
    
    %% Estilos
    classDef frontend fill:#42b883,stroke:#369870,stroke-width:2px,color:#fff
    classDef backend fill:#6db33f,stroke:#5a9a2e,stroke-width:2px,color:#fff
    classDef chat fill:#ff6b6b,stroke:#e55a5a,stroke-width:2px,color:#fff
    classDef pipeline fill:#4ecdc4,stroke:#45b7aa,stroke-width:2px,color:#fff
    classDef storage fill:#95a5a6,stroke:#7f8c8d,stroke-width:2px,color:#fff
    classDef user fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    
    class F frontend
    class B,L,P,API1,SW1 backend
    class C,G,CA,LC,API2,SW2 chat
    class D,PA pipeline
    class FS,MEM storage
    class U user
```

## 🔄 **Flujo de Datos Principal**

```mermaid
sequenceDiagram
    participant U as 👤 Usuario
    participant F as 🖥️ Frontend Vue.js
    participant B as 🔍 Backend Spring Boot
    participant C as 💬 Chat System
    participant L as 📚 Lucene Index
    participant G as 🤖 Groq LLM
    
    Note over U,G: Flujo de Búsqueda y Chat
    
    U->>F: 1. Accede a la aplicación
    F->>B: 2. Realiza búsqueda de documentos
    B->>L: 3. Consulta índice Lucene
    L-->>B: 4. Retorna resultados
    B-->>F: 5. Envía resultados estructurados
    F-->>U: 6. Muestra resultados de búsqueda
    
    U->>F: 7. Selecciona documento para chat
    F->>C: 8. Solicita chat contextual
    C->>G: 9. Procesa consulta con LLM
    G-->>C: 10. Genera respuesta contextual
    C-->>F: 11. Envía respuesta del chat
    F-->>U: 12. Muestra respuesta inteligente
```

## 🏗️ **Arquitectura por Capas**

```mermaid
graph TD
    subgraph "🎨 Capa de Presentación"
        UI[🖥️ Interfaz Vue.js<br/>Componentes Reactivos]
        UX[👤 Experiencia Usuario<br/>Responsive Design]
    end
    
    subgraph "🔗 Capa de API"
        REST1[🌐 API Búsqueda<br/>Spring Boot]
        REST2[🌐 API Chat<br/>FastAPI]
        DOC[📖 Swagger UI<br/>Documentación]
    end
    
    subgraph "⚙️ Capa de Lógica de Negocio"
        SEARCH[🔍 Motor Búsqueda<br/>Lucene]
        CHAT[💬 Motor Chat<br/>CAG + LLM]
        PROC[📄 Procesamiento<br/>PDFBox + Docling]
    end
    
    subgraph "💾 Capa de Datos"
        INDEX[📚 Índice Lucene<br/>Filesystem]
        CACHE[💾 Cache CAG<br/>Memoria]
        DOCS[📁 Documentos PDF<br/>SII]
    end
    
    UI --> REST1
    UI --> REST2
    REST1 --> SEARCH
    REST2 --> CHAT
    SEARCH --> INDEX
    CHAT --> CACHE
    PROC --> DOCS
    
    classDef presentation fill:#e8f4fd,stroke:#3498db,stroke-width:2px
    classDef api fill:#fff2cc,stroke:#d6b656,stroke-width:2px
    classDef business fill:#d5e8d4,stroke:#82b366,stroke-width:2px
    classDef data fill:#f8cecc,stroke:#b85450,stroke-width:2px
    
    class UI,UX presentation
    class REST1,REST2,DOC api
    class SEARCH,CHAT,PROC business
    class INDEX,CACHE,DOCS data
```

## 🔧 **Componentes Técnicos Detallados**

```mermaid
graph LR
    subgraph "🔍 Backend Spring Boot"
        SB[Spring Boot 3.4.5]
        AL[Apache Lucene 9.6.0]
        AP[Apache PDFBox 2.0.25]
        M[Maven Build]
    end
    
    subgraph "💬 Chat System Python"
        PY[Python 3.12+]
        FA[FastAPI]
        LC[LangChain]
        CAG[CAG Technology]
        DL[Docling]
    end
    
    subgraph "🖥️ Frontend Vue.js"
        VU[Vue.js 3.5.18]
        VI[Vite 7.1.0]
        JS[JavaScript ES6+]
        CSS[CSS3 Responsive]
    end
    
    subgraph "☁️ Servicios Externos"
        GR[Groq Cloud<br/>Llama-3.3-70B]
        API[APIs REST]
    end
    
    SB --> AL
    SB --> AP
    PY --> FA
    PY --> LC
    PY --> CAG
    VU --> VI
    LC --> GR
    
    classDef backend fill:#6db33f,stroke:#5a9a2e,stroke-width:2px,color:#fff
    classDef chat fill:#ff6b6b,stroke:#e55a5a,stroke-width:2px,color:#fff
    classDef frontend fill:#42b883,stroke:#369870,stroke-width:2px,color:#fff
    classDef external fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff
    
    class SB,AL,AP,M backend
    class PY,FA,LC,CAG,DL chat
    class VU,VI,JS,CSS frontend
    class GR,API external
```

## 📊 **Métricas de Rendimiento**

```mermaid
graph TB
    subgraph "⚡ Rendimiento Backend"
        B1[104 documentos<br/>18 segundos]
        B2[Búsqueda<br/>< 100ms]
        B3[Memoria<br/>200MB]
    end
    
    subgraph "🚀 Rendimiento Chat"
        C1[Respuesta<br/>0.90 segundos]
        C2[Velocidad<br/>40.9 palabras/s]
        C3[Mejora<br/>347x más rápido]
    end
    
    subgraph "🖥️ Rendimiento Frontend"
        F1[Carga inicial<br/>< 2 segundos]
        F2[Búsqueda<br/>< 1 segundo]
        F3[Chat<br/>< 3 segundos]
    end
    
    subgraph "⚙️ Rendimiento Pipeline"
        P1[Procesamiento<br/>10 docs/chunk]
        P2[Tamaño promedio<br/>50KB/doc]
        P3[Índice persistente<br/>Filesystem]
    end
    
    classDef perf fill:#e74c3c,stroke:#c0392b,stroke-width:2px,color:#fff
    class B1,B2,B3,C1,C2,C3,F1,F2,F3,P1,P2,P3 perf
```

## 🔄 **Ciclo de Vida del Sistema**

```mermaid
stateDiagram-v2
    [*] --> Inicio: ./start.sh
    
    Inicio --> Verificacion: Verificar prerrequisitos
    Verificacion --> Compilacion: Java, Maven OK
    Compilacion --> Aplicacion: Build exitoso
    Aplicacion --> Pruebas: Spring Boot iniciado
    Pruebas --> Operativo: Tests automáticos OK
    
    Operativo --> Indexacion: POST /api/batch/index-documents
    Indexacion --> Procesamiento: Escaneo directorio
    Procesamiento --> Extraccion: Procesamiento chunks
    Extraccion --> Indexado: PDFBox extracción
    Indexado --> Operativo: Lucene indexado
    
    Operativo --> Busqueda: GET /api/search
    Busqueda --> Resultados: Consulta Lucene
    Resultados --> Operativo: Respuesta estructurada
    
    Operativo --> Chat: POST /sessions/{id}/chat
    Chat --> ProcesamientoChat: CAG + LLM
    ProcesamientoChat --> RespuestaChat: Groq Cloud
    RespuestaChat --> Operativo: Respuesta contextual
    
    Operativo --> Mantenimiento: Re-indexación
    Mantenimiento --> Operativo: Índice actualizado
    
    Operativo --> [*]: ./stop.sh
```

## 🎯 **Casos de Uso Principales**

```mermaid
graph TD
    subgraph "🔍 Caso 1: Búsqueda de Documentos"
        U1[👤 Usuario] --> B1[🔍 Busca "IVA"]
        B1 --> R1[📋 Resultados relevantes]
        R1 --> S1[📄 Selecciona documento]
    end
    
    subgraph "💬 Caso 2: Chat Contextual"
        U2[👤 Usuario] --> C1[💬 Pregunta sobre ley]
        C1 --> P1[🧠 CAG procesa documento]
        P1 --> LLM1[🤖 LLM genera respuesta]
        LLM1 --> A1[💡 Respuesta contextual]
    end
    
    subgraph "⚙️ Caso 3: Pipeline Automático"
        D1[📁 Nuevos documentos] --> P2[⚙️ Pipeline detecta]
        P2 --> I1[📚 Indexación automática]
        I1 --> D2[✅ Disponible para búsqueda]
    end
    
    classDef user fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    classDef process fill:#e67e22,stroke:#d35400,stroke-width:2px,color:#fff
    classDef result fill:#27ae60,stroke:#229954,stroke-width:2px,color:#fff
    
    class U1,U2 user
    class B1,C1,P1,LLM1,P2,I1 process
    class R1,S1,A1,D2 result
```

---

## 📋 **Resumen del Diagrama**

### **Componentes Principales:**
1. **🖥️ Frontend Vue.js** - Interfaz de usuario moderna y responsive
2. **🔍 Backend Spring Boot** - Motor de búsqueda con Apache Lucene
3. **💬 Chat System Python** - Sistema inteligente con CAG y Groq Cloud
4. **⚙️ Pipeline Automático** - Procesamiento automatizado de documentos

### **Flujos Principales:**
1. **Búsqueda**: Usuario → Frontend → Backend → Lucene → Resultados
2. **Chat**: Usuario → Frontend → Chat System → CAG → Groq → Respuesta
3. **Pipeline**: Documentos → Procesamiento → Indexación → Disponible

### **Tecnologías Clave:**
- **Vue.js 3** + **Vite** para frontend moderno
- **Spring Boot** + **Apache Lucene** para búsqueda eficiente
- **Python** + **FastAPI** + **CAG** + **Groq** para chat inteligente
- **Pipeline automatizado** para procesamiento de documentos

---

*Diagramas generados para la Solución Informática Integral SII*  
*Versión: 1.0 - Enero 2025*
