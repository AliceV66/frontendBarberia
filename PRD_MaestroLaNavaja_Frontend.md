# Product Requirements Document (PRD): Rediseño Frontend Maestrolanavaja.com

**Versión:** 1.0
**Fecha:** 21 de Octubre, 2025
**Estado:** Borrador Aprobado
**Stakeholder Principal:** Dueño/Desarrollador (Tech Partner)

---

## 1. Resumen Ejecutivo
El objetivo es rediseñar el frontend de `maestrolanavaja.com` para abandonar la estética de plantilla genérica y establecer una identidad digital **Premium, Segura y Elegante**.
El sitio dejará de ser un simple folleto informativo para convertirse en una herramienta de conversión de alto ticket. La arquitectura debe ser desacoplada para permitir la futura integración de un ERP propio sin reescribir el frontend.

**Conceptos Clave:**
* **Experiencia:** Demostrada visualmente (maestría, antigüedad).
* **Seguridad:** Transmitida por la calidad técnica, sin errores, y validación social.
* **Elegancia:** Minimalismo, paleta oscura y tipografía editorial.
* **Premium:** Justificación visual de precios superiores al promedio.

---

## 2. Sistema de Diseño & Identidad Visual ("The Executive Grooming")

### 2.1. Paleta de Colores
Se abandona el esquema rojo/azul/blanco tradicional de barbería. Se adopta un esquema de club de caballeros moderno.

| Semántica | Color | Hex Code | Uso Principal | Razón Psicológica |
| :--- | :--- | :--- | :--- | :--- |
| **Base / Fondo** | **Gunmetal** | `#1A202C` | Fondos, Secciones principales | Solidez, autoridad, menos agresivo que el negro puro. |
| **Secundario** | **Deep Navy** | `#0F172A` | Footer, Modales, Tarjetas | Profundidad, elegancia corporativa. |
| **Acento / CTA** | **Burnished Copper** | `#B45309` | Botones, Iconos clave, Bordes activos | Evoca herramientas clásicas, lujo antiguo, valor. |
| **Texto Principal**| **Off-White** | `#F3F4F6` | Títulos, Cuerpo de texto | Legibilidad sin fatiga visual (alto contraste controlado). |
| **Texto Secundario**| **Dim Gray** | `#9CA3AF` | Metadatos, pies de foto | Jerarquía visual. |
| **Feedback** | **Slate Green** | `#3F6212` | Mensajes de éxito, disponibilidad | Seguridad, orgánico (evita el verde neón "digital"). |

### 2.2. Tipografía
* **Títulos (Display):** *Playfair Display* o *Cinzel*.
    * Uso: Encabezados H1, H2. Aporta el toque "Editorial" y clásico.
* **Cuerpo (Sans):** *Inter* o *Lato*.
    * Uso: Párrafos, UI, Botones. Aporta la legibilidad técnica y moderna necesaria para la confianza.

### 2.3. Estética Visual
* **Fotografía:** Estilo "Low Key" (Clave baja). Sombras duras, iluminación dramática sobre el sujeto (barba, navaja, toalla).
* **Video:** Slow-motion en el Hero. Vapor, movimiento de tijeras. Nada de ritmo frenético.

---

## 3. Arquitectura Técnica

### 3.1. Stack Recomendado
* **Core:** **Astro**.
    * *Justificación:* Performance absoluta (0 JS por defecto). Ideal para SEO local.
* **Estilos:** **Tailwind CSS**.
    * *Justificación:* Mantenibilidad del sistema de diseño y velocidad de desarrollo.
* **Estado UI:** **Preact** o **React** (solo para islas interactivas si son necesarias, como un carrusel o menú móvil).

### 3.2. Estrategia de Gestión de Reservas (Fase 1 vs Fase 2)
Actualmente, el booking es externo. Para evitar la dependencia de URLs feas y preparar el terreno para el ERP propio:

1.  **Redirección Interna (Proxy de URL):**
    * Crear una ruta/redirect en el servidor o configuración de deploy: `maestrolanavaja.com/reserva`.
    * Esta ruta redirige (301 o 302) a la URL larga de `conectasitios.cl`.
    * *Beneficio:* Si el proveedor cambia, solo actualizamos el redirect. El frontend nunca se entera.
2.  **Componente `BookingCTA`:**
    * Un componente aislado que encapsula la lógica del botón.
    * Atributos obligatorios: `target="_blank"`, `rel="noopener noreferrer"`.
    * *Roadmap:* En el futuro, este componente dejará de ser un enlace `<a>` para convertirse en un trigger de Modal que cargue el formulario del ERP propio.

---

## 4. Requerimientos Funcionales (Secciones Clave)

### 4.1. Header / Navegación
* **Diseño:** Flotante (Sticky) con efecto "glassmorphism" (desenfoque) sutil al hacer scroll.
* **Elementos:** Logo minimalista (izquierda), Links de anclaje (centro), Botón "Reservar" (derecha, variante pequeña).

### 4.2. Hero Section (La Promesa)
* **Contenido:** Video de fondo o Imagen Hero de alta calidad.
* **Copy:** "Maestría y Distinción." (O similar).
* **CTA Principal:** Botón grande en *Burnished Copper*.
* **Prueba Social Inmediata:** "Más de 500 clientes satisfechos" o "4.9/5 Estrellas" (pequeño, bajo el título).

### 4.3. Menú de Servicios (La Carta)
* **Formato:** Lista limpia, estilo menú de restaurante de lujo.
* **Precios:** Visibles, tipografía alineada a la derecha.
* **Distinción VIP:** Los servicios premium deben tener un borde sutil o un fondo ligeramente más claro para destacar.

### 4.4. El Maestro (Autoridad)
* **Contenido:** Foto profesional del barbero (mirando a cámara o trabajando).
* **Bio:** Breve. Enfocada en años de experiencia y técnica.
* **Objetivo:** Humanizar la marca y generar seguridad ("Sé quién me va a cortar el pelo").

### 4.5. Footer
* **Datos:** Dirección, Teléfono, Horarios.
* **Legal:** Links a privacidad (necesario para percepción de seguridad).
* **Redes:** Iconos minimalistas.

---

## 5. Implementation Roadmap

### Fase 1: Setup & Estilos (Día 1-2)
* [ ] Inicializar proyecto Astro.
* [ ] Configurar `tailwind.config.mjs` con la paleta "Executive Grooming".
* [ ] Configurar fuentes (Google Fonts: Playfair + Inter).
* [ ] Crear componente base `BookingButton`.

### Fase 2: Desarrollo de Contenido (Día 3-5)
* [ ] Implementar redirección `/reserva`.
* [ ] Maquetar Landing Page (Hero, Servicios, Bio).
* [ ] Optimización de imágenes (formato WebP/AVIF).

### Fase 3: Performance & Deploy (Día 6)
* [ ] Auditoría Lighthouse (Meta: 95+ en Performance, SEO, Accesibilidad).
* [ ] Configuración de Headers de seguridad (HSTS).
* [ ] Despliegue.

---

## 6. Snippets de Configuración

### Tailwind Config (Colores)
```javascript
theme: {
  extend: {
    colors: {
      primary: { DEFAULT: '#1A202C', dark: '#0F172A' }, // Gunmetal
      accent: { DEFAULT: '#B45309', light: '#D97706' }, // Copper
      surface: { DEFAULT: '#F3F4F6', dim: '#9CA3AF' },  // Off-White
      success: '#3F6212',
    }
  }
}


// Pseudo-código del componente
const BookingBtn = ({ className }) => (
  <a 
    href="/reserva" // Usar el redirect interno, NO el link externo directo
    target="_blank"
    rel="noopener noreferrer"
    className={`bg-accent text-surface hover:bg-accent-light transition-all ${className}`}
  >
    Reservar Cita
    <ExternalLinkIcon className="w-4 h-4 ml-2 opacity-80" />
  </a>
);