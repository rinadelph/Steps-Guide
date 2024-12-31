# Guía de Estilo

## Colores

### Primarios
```css
--primary: #0070f3;
--primary-foreground: #ffffff;
```

### Secundarios
```css
--secondary: #f5f5f5;
--secondary-foreground: #111111;
```

### Acentos
```css
--accent: #fafafa;
--accent-foreground: #111111;
```

### Estado
```css
--destructive: #ff4444;
--destructive-foreground: #ffffff;
--success: #00c853;
--success-foreground: #ffffff;
--warning: #ffa726;
--warning-foreground: #ffffff;
```

### Fondo
```css
--background: #ffffff;
--foreground: #111111;
```

### Bordes
```css
--border: #e5e5e5;
--input: #e5e5e5;
--ring: #0070f3;
```

## Tipografía

### Fuente Principal
```css
font-family: var(--font-inter);
```

### Tamaños
```css
--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */
--text-4xl: 2.25rem;   /* 36px */
```

### Pesos
```css
--font-thin: 100;
--font-light: 300;
--font-normal: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;
```

## Espaciado

### Escala
```css
--spacing-0: 0;
--spacing-1: 0.25rem;  /* 4px */
--spacing-2: 0.5rem;   /* 8px */
--spacing-3: 0.75rem;  /* 12px */
--spacing-4: 1rem;     /* 16px */
--spacing-5: 1.25rem;  /* 20px */
--spacing-6: 1.5rem;   /* 24px */
--spacing-8: 2rem;     /* 32px */
--spacing-10: 2.5rem;  /* 40px */
--spacing-12: 3rem;    /* 48px */
--spacing-16: 4rem;    /* 64px */
```

### Breakpoints
```css
--screen-sm: 640px;
--screen-md: 768px;
--screen-lg: 1024px;
--screen-xl: 1280px;
--screen-2xl: 1536px;
```

## Bordes

### Radio
```css
--radius-sm: 0.125rem;  /* 2px */
--radius-md: 0.375rem;  /* 6px */
--radius-lg: 0.5rem;    /* 8px */
--radius-xl: 0.75rem;   /* 12px */
--radius-full: 9999px;
```

### Ancho
```css
--border-thin: 1px;
--border-medium: 2px;
--border-thick: 4px;
```

## Sombras

### Elevación
```css
--shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
--shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
--shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
--shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1);
```

## Animaciones

### Duración
```css
--duration-75: 75ms;
--duration-100: 100ms;
--duration-150: 150ms;
--duration-200: 200ms;
--duration-300: 300ms;
--duration-500: 500ms;
```

### Timing
```css
--ease-linear: linear;
--ease-in: cubic-bezier(0.4, 0, 1, 1);
--ease-out: cubic-bezier(0, 0, 0.2, 1);
--ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
```

## Z-Index

### Capas
```css
--z-0: 0;
--z-10: 10;
--z-20: 20;
--z-30: 30;
--z-40: 40;
--z-50: 50;
--z-auto: auto;
```

### Específicos
```css
--z-dropdown: 1000;
--z-sticky: 1100;
--z-fixed: 1200;
--z-modal: 1300;
--z-popover: 1400;
--z-tooltip: 1500;
```

## Mejores Prácticas

### Responsive Design
```tsx
// ✅ Bueno: Mobile-first approach
<div className="p-4 md:p-6 lg:p-8">
  <h1 className="text-lg md:text-xl lg:text-2xl">
    Título
  </h1>
</div>

// ❌ Malo: Desktop-first
<div className="p-8 sm:p-6 xs:p-4">
  <h1 className="text-2xl sm:text-xl xs:text-lg">
    Título
  </h1>
</div>
```

### Espaciado
```tsx
// ✅ Bueno: Uso consistente de la escala de espaciado
<div className="space-y-4">
  <h1>Título</h1>
  <p>Párrafo</p>
</div>

// ❌ Malo: Valores arbitrarios
<div style={{ marginBottom: '23px' }}>
  <h1>Título</h1>
  <p>Párrafo</p>
</div>
```

### Colores
```tsx
// ✅ Bueno: Uso de variables CSS
<button className="bg-primary text-primary-foreground">
  Botón
</button>

// ❌ Malo: Valores hardcodeados
<button style={{ backgroundColor: '#0070f3', color: '#fff' }}>
  Botón
</button>
```

### Tipografía
```tsx
// ✅ Bueno: Uso de clases utilitarias
<p className="text-sm font-medium text-foreground">
  Texto
</p>

// ❌ Malo: Estilos inline
<p style={{ fontSize: '14px', fontWeight: 500, color: '#111' }}>
  Texto
</p>
```

## Accesibilidad

### Contraste
- Texto normal: Mínimo 4.5:1
- Texto grande: Mínimo 3:1
- Elementos interactivos: Mínimo 3:1

### Tamaño de Toque
- Mínimo 44x44px para elementos interactivos en móvil
- Espacio mínimo de 8px entre elementos interactivos

### Modo Oscuro
```tsx
// Automático basado en preferencias del sistema
<html className="dark">
  <body className="bg-background text-foreground">
    {children}
  </body>
</html>
```

## Rendimiento

### Imágenes
- Usar formatos modernos (WebP, AVIF)
- Implementar lazy loading
- Proporcionar dimensiones explícitas

### Fuentes
- Precargar fuentes críticas
- Usar font-display: swap
- Implementar subsetting