# 📄 ScanLens

**Escáner de documentos profesional con corrección de perspectiva**

Aplicación web tipo PWA que convierte tu dispositivo móvil en un escáner de documentos de alta calidad, similar a Microsoft Lens, pero funcionando 100% en el navegador.

![Versión](https://img.shields.io/badge/versión-1.5.0-blue)
![Licencia](https://img.shields.io/badge/licencia-MIT-green)
![Responsive](https://img.shields.io/badge/responsive-mobile--first-orange)

---

## ✨ Características

### ✅ Implementadas
- 📷 **Captura múltiple**: desde cámara o archivos existentes
- 🎯 **Corrección de perspectiva real** con OpenCV.js (`warpPerspective`)
- 🖐️ **Editor de 4 puntos arrastrables** (touch + mouse)
- 📄 **Múltiples páginas**: escanea documentos de varias hojas
- 🔄 **Reordenamiento** con drag & drop (SortableJS)
- ⚡ **3 niveles de calidad**: Rápido / Equilibrado / Alta
- 💾 **Descarga individual** de páginas
- 📱 **Diseño mobile-first** estilo app nativa
- 🚀 **Carga diferida** de OpenCV.js (la app abre instantáneamente)
- 🎨 **Interfaz moderna** con tema oscuro

### 🚧 Próximas fases
- 🎨 Filtros de mejora (B/N, escala de grises, aclarar fondo, brillo, contraste, nitidez)
- 🗜️ Compresión avanzada con presets y slider manual
- 📑 Generación de PDF en formato A4 con márgenes de 10mm
- 📚 Apilado inteligente de múltiples imágenes por hoja
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
┌─────────┐     ┌─────────┐     ┌──────────┐     ┌─────────┐     ┌─────────┐
│  INICIO │ ──▶ │ EDITOR  │ ──▶ │ RESULTADO│ ──▶ │ GALERÍA │ ──▶ │   PDF   │
│         │     │         │     │          │     │         │     │  (Fase 5)│
└─────────┘     └─────────┘     └──────────┘     └─────────┘     └─────────┘
                     ▲                │
                     │    ┌───────────┘
                     │    │ (Agregar otra página)
                     └────┘
```

### Paso a paso

1. **Selecciona calidad** en la pantalla de inicio:
   - ⚡ **Rápido** (1000px, 80%): 1-2 segundos, ideal para lectura en pantalla
   - ⚖️ **Equilibrado** (1200px, 90%): 3-5 segundos, recomendado para uso general
   - 🎯 **Alta** (2000px, 92%): 5-10 segundos, para impresión profesional

2. **Captura** la imagen (cámara o archivo)

3. **Ajusta las 4 esquinas** arrastrando los puntos azules hasta las esquinas del documento

4. **Aplica la corrección** → la imagen se enderezará automáticamente

5. **Decide qué hacer**:
   - 📄 **Agregar otra página** → captura más páginas
   - ✅ **Terminar documento** → ve a la galería
   - 💾 **Descargar solo esta página** → guarda la imagen individual

6. **En la galería**:
   - Arrastra para reordenar
   - ✏️ para re-editar una página
   - 🗑️ para eliminar
   - ➕ para agregar más páginas
   - 📑 **Generar PDF A4** (próximamente en Fase 5)

---

## 🛠️ Tecnologías

| Tecnología | Uso |
|------------|-----|
| **HTML5** | Estructura semántica |
| **CSS3** | Diseño mobile-first con variables CSS |
| **JavaScript (Vanilla)** | Lógica de la aplicación |
| **OpenCV.js** | Corrección de perspectiva (`warpPerspective`) |
| **SortableJS** | Drag & drop optimizado para móvil |
| **Canvas API** | Procesamiento de imágenes |
| **jsPDF** *(pendiente)* | Generación de PDF A4 |

---

## 📐 Arquitectura

```
📁 ScanLens/
├── 📄 index.html          # Aplicación completa (single-file)
└── 📄 README.md           # Este archivo
```

**Nota:** La Fase 1 está implementada como un único archivo HTML para facilitar el despliegue. En fases posteriores se separará en módulos.

### Módulos planificados

```
📁 src/
├── 📁 core/
│   ├── capture.js          # Cámara y subida de archivos
│   ├── opencv-loader.js    # Carga diferida de OpenCV.js
│   ├── perspective.js      # Transformación homográfica
│   ├── crop.js             # Interfaz de los 4 puntos
│   ├── filters.js          # Filtros de mejora
│   ├── compress.js         # Compresión con presets
│   ├── reorder.js          # Drag & drop
│   └── pdf.js              # Generación PDF A4
├── 📁 ui/
│   └── screens/            # Las pantallas de la app
└── 📁 workers/
    └── image-processor.js  # Web Worker para no bloquear UI
```

---

## ⚙️ Configuración de calidad

La aplicación usa 3 presets de calidad que balancean velocidad y resolución:

| Preset | Tamaño máx | Calidad JPEG | DPI en A4 | Tiempo estimado | Caso de uso |
|--------|-----------|--------------|-----------|-----------------|-------------|
| ⚡ Rápido | 1000px | 80% | ~85 DPI | 1-2 seg | Lectura en pantalla |
| ⚖️ Equilibrado | 1200px | 90% | ~100 DPI | 3-5 seg | Uso general |
| 🎯 Alta | 2000px | 92% | ~170 DPI | 5-10 seg | Impresión profesional |

La preferencia se guarda en `localStorage` automáticamente.

---

## 🎯 Estado del proyecto

### ✅ Fase 1 — Esqueleto funcional
- [x] Pantalla de inicio con captura
- [x] Editor con 4 puntos arrastrables
- [x] Corrección de perspectiva con OpenCV.js
- [x] Carga diferida y precarga de OpenCV

### ✅ Fase 1.5 — Múltiples páginas
- [x] Acumulación de páginas en memoria
- [x] Pantalla de galería con thumbnails
- [x] Drag & drop para reordenar
- [x] Edición y eliminación de páginas
- [x] Límite de 50 páginas

### ✅ Optimización de rendimiento
- [x] Redimensionado previo al procesamiento
- [x] Uso de JPEG en lugar de PNG
- [x] Selector de calidad (3 presets)
- [x] Barra de progreso
- [x] Medición de tiempo de procesamiento

### 🚧 Fase 2 — Filtros (próxima)
- [ ] Blanco y negro (alto contraste)
- [ ] Escala de grises
- [ ] Modo "documento" (aclarar fondo)
- [ ] Brillo y contraste manuales
- [ ] Nitidez

### 🚧 Fase 3 — Compresión avanzada
- [ ] Presets de compresión
- [ ] Slider manual de calidad
- [ ] Vista previa de tamaño final

### 🚧 Fase 4 — Vista previa PDF
- [ ] Simulación de páginas A4
- [ ] Apilado vertical de imágenes
- [ ] Márgenes configurables

### 🚧 Fase 5 — Generación PDF
- [ ] Integración con jsPDF
- [ ] Formato A4 con márgenes de 10mm
- [ ] Múltiples imágenes por hoja si caben
- [ ] Nombre personalizado

### 🚧 Fase 6 — PWA y extras
- [ ] Manifest.json
- [ ] Service Worker (offline)
- [ ] Guardado en IndexedDB
- [ ] Web Share API
- [ ] Numeración de páginas

---

## 🧪 Compatibilidad

| Navegador | Soporte |
|-----------|---------|
| Chrome (Android) | ✅ Completo |
| Safari (iOS) | ✅ Completo |
| Firefox | ✅ Completo |
| Edge | ✅ Completo |
| Samsung Internet | ✅ Completo |

**Requisitos mínimos:**
- Navegador moderno con soporte para Canvas API
- HTTPS (para acceso a cámara)
- ~10 MB de RAM disponibles (para OpenCV.js)

---

## 🤝 Contribución

Las contribuciones son bienvenidas. Para contribuir:

1. Haz un fork del repositorio
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Haz commit de tus cambios (`git commit -m 'Add: nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

---

## 📄 Licencia

Este proyecto está bajo la licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

---

## 🙏 Créditos

- **[OpenCV.js](https://docs.opencv.org/)** — Biblioteca de visión por computadora
- **[SortableJS](https://sortablejs.github.io/Sortable/)** — Drag & drop para móvil
- **[jsPDF](https://github.com/parallax/jsPDF)** *(pendiente)* — Generación de PDF
- Inspirado en **[Microsoft Lens](https://www.microsoft.com/lens)**

---

## 📞 Soporte

¿Encontraste un bug o tienes una sugerencia?

- Abre un issue en el repositorio
- Revisa la sección de [Issues](../../issues) existentes

---

## 🗺️ Roadmap

```
2026 Q2 ──▶ Fase 2: Filtros de mejora
         ──▶ Fase 3: Compresión avanzada
         
2026 Q3 ──▶ Fase 4: Vista previa PDF
         ──▶ Fase 5: Generación PDF A4
         
2026 Q4 ──▶ Fase 6: PWA + extras
         ──▶ Versión 2.0 estable
```

---

<div align="center">

**Hecho con ❤️ para escanear documentos fácilmente**

⭐ Si te gusta el proyecto, ¡dale una estrella!

</div>
