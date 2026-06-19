# 📄 ScanLens

**Escáner de documentos profesional con corrección de perspectiva**

Aplicación web tipo PWA que convierte tu dispositivo móvil en un escáner de documentos de alta calidad, similar a Microsoft Lens, pero funcionando 100% en el navegador.

![Versión](https://img.shields.io/badge/versión-5.0.0-blue)
![Licencia](https://img.shields.io/badge/licencia-MIT-green)
![Responsive](https://img.shields.io/badge/responsive-mobile--first-orange)

---

## ✨ Características

### ✅ Implementadas
- 📷 **Captura múltiple**: desde cámara, archivos individuales o selección múltiple
- 🎯 **Corrección de perspectiva real** con motor propio de homografía en JavaScript puro
- 🖐️ **Editor de 4 puntos arrastrables** (touch + mouse)
- 📄 **Múltiples páginas**: escanea documentos de varias hojas
- 🔄 **Reordenamiento** con drag & drop (SortableJS)
- ⚡ **3 niveles de calidad de captura**: Rápido (600px) / Normal (1000px) / Alta (1500px)
- 📑 **Generación real de PDF A4** con jsPDF
- 🗜️ **3 presets de compresión PDF**: Alta (90%) / Equilibrado (75%) / Máxima (50%)
- 📐 **Apilamiento vertical inteligente** con centrado automático
- 🎨 **Modo "Sin corrección"** para fotos bien tomadas
- 💾 **Descarga individual** de páginas
- 📱 **Diseño mobile-first** estilo app nativa
- 🚀 **Procesamiento ultrarrápido** (1-3 segundos por imagen)
- 🎨 **Interfaz moderna** con tema oscuro

### 🚧 Próximas fases
- 🎨 Filtros de mejora (B/N, escala de grises, aclarar fondo, brillo, contraste, nitidez)
- 🗜️ Compresión avanzada con slider manual
- 📚 Vista previa PDF antes de generar
- 💿 PWA instalable con funcionamiento offline
- 🗂️ Guardado de proyectos en IndexedDB
- 🌐 Multiidioma

---

## 🎥 Demo

> **Pruébalo ahora:** Sube el archivo `index.html` a cualquier hosting estático (GitHub Pages, Netlify, Vercel) y ábrelo desde tu móvil.

**Nota importante:** La cámara requiere contexto seguro (HTTPS) para funcionar.

---

## 🚀 Instalación rápida

### Opción 1: Servidor local (recomendado para desarrollo)

```bash
# Con Python
python -m http.server 8000

# Con Node.js (http-server)
npx http-server -p 8000

# Con PHP
php -S localhost:8000
```

Luego abre: `http://localhost:8000`

### Opción 2: Abrir directamente

Simplemente abre `index.html` en tu navegador (la cámara no funcionará, pero sí la subida de archivos).

### Opción 3: Hosting estático

Sube el archivo `index.html` a:
- [GitHub Pages](https://pages.github.com/)
- [Netlify](https://www.netlify.com/)
- [Vercel](https://vercel.com/)
- Cualquier otro hosting estático

---

## 📖 Guía de uso

### Flujo principal

```
┌─────────┐     ┌─────────┐     ┌──────────┐     ┌─────────┐     ┌──────────┐     ┌─────────┐
│  INICIO │ ──▶ │ EDITOR  │ ──▶ │ RESULTADO│ ──▶ │ GALERÍA │ ──▶ │ CONFIG   │ ──▶ │   PDF   │
│         │     │         │     │          │     │         │     │   PDF    │     │DESCARGA │
└─────────┘     └─────────┘     └──────────┘     └─────────┘     └──────────┘     └─────────┘
                     ▲                │
                     │    ┌───────────┘
                     │    │ (Agregar otra página)
                     └────┘
```

### Paso a paso

#### 1. Configurar calidad de captura
En la pantalla de inicio, selecciona la calidad:
- ⚡ **Rápido** (600px): 1-2 segundos, ideal para lectura en pantalla
- ⚖️ **Normal** (1000px): 2-4 segundos, recomendado para uso general
- 🎯 **Alta** (1500px): 4-6 segundos, para impresión profesional

#### 2. Capturar imágenes
Tienes 3 opciones:
- 📷 **Tomar Foto**: abre la cámara directamente
- 🖼️ **Subir 1 imagen**: selecciona una foto de tu galería
- 📚 **Subir varias imágenes**: selecciona múltiples fotos de una vez (procesamiento en lote)

#### 3. Ajustar esquinas (Editor)
- Arrastra los 4 puntos azules hasta las esquinas del documento
- Toca **🔄 Reset** para reiniciar las esquinas
- Toca **⏭️ Sin corrección** si la foto ya está bien tomada (más rápido)
- Toca **✨ Aplicar** para corregir la perspectiva

#### 4. Decidir qué hacer (Resultado)
Después de corregir cada página:
- 📄 **Agregar otra página** → captura más páginas
- ✅ **Terminar documento** → ve a la galería
- 💾 **Descargar solo esta página** → guarda la imagen individual

#### 5. Organizar páginas (Galería)
- **Arrastra** las páginas para reordenarlas
- ✏️ **Editar** una página específica
- 🗑️ **Eliminar** páginas que no necesites
- ➕ **Agregar más** páginas
- 📑 **Generar PDF A4** → abre la configuración del PDF

#### 6. Configurar PDF
Antes de generar, configura:
- 📝 **Nombre del documento** (se permite acentos y espacios)
- 🗜️ **Compresión**:
  - 🎯 **Alta calidad (90%)**: máximo detalle, archivo más grande
  - ⚖️ **Equilibrado (75%)**: recomendado (por defecto)
  - ⚡ **Máxima compresión (50%)**: archivo más pequeño

La vista previa muestra en tiempo real:
- Número de páginas
- Hojas A4 estimadas
- Tamaño original total
- **Tamaño estimado del PDF**

#### 7. Generar y descargar
Toca **📥 Generar y descargar** y el PDF se descargará automáticamente con el nombre configurado.

---

## 📐 Formato del PDF generado

El PDF generado tiene las siguientes características técnicas:

| Característica | Valor |
|----------------|-------|
| **Formato** | A4 (210 × 297 mm) |
| **Márgenes** | 10 mm en los 4 lados |
| **Área útil** | 190 × 277 mm |
| **Espaciado entre imágenes** | 3 mm |
| **Apilamiento** | Vertical automático |
| **Alineación** | Centrada horizontalmente |
| **Escalado** | Contain (respeta aspect ratio) |
| **Compresión** | JPEG 50-90% según preset |
| **Redimensionado máx** | 1000-1800px según preset |

### Comportamiento de escalado

| Tipo de imagen | Comportamiento |
|----------------|----------------|
| **Vertical** (documento A4) | Ocupa todo el alto (277mm), centrada horizontalmente |
| **Horizontal** (tabla ancha) | Ocupa todo el ancho (190mm), arriba de la hoja |
| **Cuadrada** | Centrada en ambos ejes |
| **Muy pequeña** | Centrada, no se estira |
| **Múltiples en 1 hoja** | Apiladas verticalmente con 3mm de espaciado |

**Garantías:**
- ✅ Nunca se cortan imágenes
- ✅ Nunca hay páginas en blanco
- ✅ Nunca se deforman las imágenes
- ✅ Máximo uso del espacio disponible

---

## 🛠️ Tecnologías

| Tecnología | Uso |
|------------|-----|
| **HTML5** | Estructura semántica |
| **CSS3** | Diseño mobile-first con variables CSS |
| **JavaScript (Vanilla)** | Lógica de la aplicación |
| **Motor propio de homografía** | Corrección de perspectiva optimizada (JS puro) |
| **SortableJS** | Drag & drop optimizado para móvil |
| **Canvas API** | Procesamiento de imágenes |
| **jsPDF** | Generación de PDF A4 |

### ¿Por qué motor propio en lugar de OpenCV.js?

En versiones anteriores usamos OpenCV.js, pero tenía problemas:
- ❌ 8 MB de descarga
- ❌ 30-60+ segundos de procesamiento en móvil
- ❌ Dependencia de WebAssembly

**Solución actual:**
- ✅ Motor propio de homografía en JavaScript puro
- ✅ 0 MB adicionales (ya está en el código)
- ✅ 1-3 segundos de procesamiento
- ✅ Funciona offline desde el primer momento
- ✅ 10x más rápido que OpenCV.js

---

## 📐 Arquitectura

```
📁 ScanLens/
├── 📄 index.html          # Aplicación completa (single-file)
└── 📄 README.md           # Este archivo
```

**Nota:** La aplicación está implementada como un único archivo HTML para facilitar el despliegue. En fases posteriores se separará en módulos.

### Módulos planificados

```
📁 src/
├── 📁 core/
│   ├── capture.js          # Cámara y subida de archivos
│   ├── homography.js       # Motor propio de corrección de perspectiva
│   ├── crop.js             # Interfaz de los 4 puntos
│   ├── filters.js          # Filtros de mejora (pendiente)
│   ├── compress.js         # Compresión con presets
│   ├── reorder.js          # Drag & drop
│   └── pdf.js              # Generación PDF A4
├── 📁 ui/
│   └── screens/            # Las pantallas de la app
└── 📁 workers/
    └── image-processor.js  # Web Worker para no bloquear UI (pendiente)
```

---

## ⚙️ Configuración de calidad

### Calidad de captura

La aplicación usa 3 presets de calidad para el procesamiento inicial:

| Preset | Tamaño máx | Calidad JPEG | Tiempo estimado | Caso de uso |
|--------|-----------|--------------|-----------------|-------------|
| ⚡ Rápido | 600px | 82% | 1-2 seg | Lectura en pantalla |
| ⚖️ Normal | 1000px | 88% | 2-4 seg | Uso general |
| 🎯 Alta | 1500px | 92% | 4-6 seg | Impresión profesional |

### Compresión PDF

Al generar el PDF, puedes elegir entre 3 niveles de compresión:

| Preset | Calidad JPEG | Tamaño máx | Caso de uso |
|--------|--------------|-----------|-------------|
| 🎯 Alta | 90% | 1800px | Impresión profesional |
| ⚖️ Equilibrado | 75% | 1400px | Uso general (recomendado) |
| ⚡ Máxima | 50% | 1000px | Compartir por email/WhatsApp |

La preferencia de calidad de captura se guarda en `localStorage` automáticamente.

---

## 🎯 Estado del proyecto

### ✅ Fase 1 — Esqueleto funcional
- [x] Pantalla de inicio con captura
-
