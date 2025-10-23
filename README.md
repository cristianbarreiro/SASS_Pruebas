# 🎨 SASS Pruebas - Guía Completa

Este proyecto es una introducción completa a **SASS (Syntactically Awesome Style Sheets)**, un preprocesador CSS que nos permite escribir estilos más eficientes, organizados y mantenibles.

## 📋 Tabla de Contenidos

- [¿Qué es SASS?](#qué-es-sass)
- [Instalación y Configuración](#instalación-y-configuración)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Comandos Disponibles](#comandos-disponibles)
- [Características de SASS](#características-de-sass)
- [Ejemplos Prácticos](#ejemplos-prácticos)
- [Recursos Adicionales](#recursos-adicionales)

## 🤔 ¿Qué es SASS?

**SASS** es un preprocesador CSS que extiende las capacidades del CSS estándar añadiendo características como:

- **Variables**: Para reutilizar valores
- **Nesting**: Para anidar selectores
- **Mixins**: Para reutilizar bloques de código
- **Funciones**: Para cálculos y manipulación de datos
- **Imports**: Para organizar el código en múltiples archivos
- **Herencia**: Para extender estilos existentes

### SASS vs SCSS

SASS tiene dos sintaxis:
- **SASS** (indentado): Sin llaves ni punto y coma
- **SCSS** (Sassy CSS): Sintaxis similar a CSS con llaves y punto y coma

Este proyecto utiliza **SCSS** por su similitud con CSS tradicional.

## ⚙️ Instalación y Configuración

### Requisitos Previos

```bash
# Instalar Node.js (si no lo tienes)
# Descargar desde: https://nodejs.org/

# Verificar instalación
node --version
npm --version
```

### Instalación de SASS

```bash
# Instalación global
npm install -g sass

# Verificar instalación
sass --version
```

### Configuración del Proyecto

```bash
# Clonar el proyecto
git clone https://github.com/cristianbarreiro/SASS_Pruebas.git
cd SASS_Pruebas

# No requiere instalación de dependencias adicionales
```

## 📁 Estructura del Proyecto

```
SASS_Pruebas/
│
├── index.html              # Archivo HTML principal
├── package.json           # Configuración del proyecto
├── README.md              # Esta guía
│
└── utils/
    ├── scss/
    │   └── styles.scss    # Archivos fuente SASS
    └── css/
        ├── styles.css     # CSS compilado
        └── styles.css.map # Mapa de sourcemap
```

## 🚀 Comandos Disponibles

### Compilación Manual

```bash
# Compilar una vez
sass utils/scss/styles.scss utils/css/styles.css

# Compilar con sourcemap
sass --source-map utils/scss/styles.scss utils/css/styles.css
```

### Modo Watch (Recomendado)

```bash
# Usar el comando configurado en package.json
npm run sass

# O directamente con SASS
sass --watch utils/scss/styles.scss:utils/css/styles.css
```

### Servidor de Desarrollo

```bash
# Si tienes Live Server en VS Code
# 1. Instala la extensión "Live Server"
# 2. Clic derecho en index.html
# 3. Selecciona "Open with Live Server"
# 4. Se abrirá en http://127.0.0.1:5500/
```

## 🎯 Características de SASS

### 1. Variables

```scss
// Definir variables
$primary-color: #3498db;
$secondary-color: #2ecc71;
$font-size: 16px;
$margin-base: 10px;

// Usar variables
.button {
    background-color: $primary-color;
    font-size: $font-size;
    margin: $margin-base;
}
```

### 2. Nesting (Anidamiento)

```scss
.navbar {
    background: #333;
    padding: 1rem;
    
    ul {
        list-style: none;
        margin: 0;
        
        li {
            display: inline-block;
            
            a {
                color: white;
                text-decoration: none;
                
                &:hover {
                    color: $primary-color;
                }
            }
        }
    }
}
```

### 3. Mixins

```scss
// Definir mixin
@mixin button-style($bg-color, $text-color) {
    background-color: $bg-color;
    color: $text-color;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    
    &:hover {
        opacity: 0.8;
    }
}

// Usar mixin
.btn-primary {
    @include button-style($primary-color, white);
}

.btn-secondary {
    @include button-style($secondary-color, white);
}
```

### 4. Funciones

```scss
// Función para calcular rem
@function rem($pixels, $base: 16px) {
    @return $pixels / $base * 1rem;
}

// Usar función
.title {
    font-size: rem(24px); // Resultado: 1.5rem
}
```

### 5. Imports y Partials

```scss
// _variables.scss (partial)
$primary-color: #3498db;

// _mixins.scss (partial)
@mixin flex-center {
    display: flex;
    justify-content: center;
    align-items: center;
}

// styles.scss (archivo principal)
@import 'variables';
@import 'mixins';

.container {
    @include flex-center;
    background: $primary-color;
}
```

### 6. Extend/Herencia

```scss
%message-shared {
    border: 1px solid #ccc;
    padding: 10px;
    color: #333;
}

.message {
    @extend %message-shared;
}

.success {
    @extend %message-shared;
    border-color: green;
}

.error {
    @extend %message-shared;
    border-color: red;
}
```

## 💡 Ejemplos Prácticos

### Ejemplo 1: Sistema de Colores

```scss
// Paleta de colores
$colors: (
    primary: #3498db,
    secondary: #2ecc71,
    danger: #e74c3c,
    warning: #f39c12,
    info: #17a2b8
);

// Función para obtener colores
@function color($name) {
    @return map-get($colors, $name);
}

// Uso
.alert-danger {
    background: color(danger);
    color: white;
}
```

### Ejemplo 2: Responsive Breakpoints

```scss
// Breakpoints
$breakpoints: (
    mobile: 480px,
    tablet: 768px,
    desktop: 1024px,
    wide: 1200px
);

// Mixin para media queries
@mixin respond-to($breakpoint) {
    $size: map-get($breakpoints, $breakpoint);
    @media (min-width: $size) {
        @content;
    }
}

// Uso
.container {
    width: 100%;
    
    @include respond-to(tablet) {
        width: 750px;
    }
    
    @include respond-to(desktop) {
        width: 970px;
    }
}
```

### Ejemplo 3: Grid System

```scss
// Variables del grid
$grid-columns: 12;
$grid-gutter: 20px;

// Mixin para columnas
@mixin col($size) {
    width: percentage($size / $grid-columns);
    float: left;
    padding: 0 $grid-gutter / 2;
}

// Generar clases de columnas
@for $i from 1 through $grid-columns {
    .col-#{$i} {
        @include col($i);
    }
}
```

## 🔧 Configuración Avanzada

### Configuración de VS Code

Instala estas extensiones útiles:
- **Live Sass Compiler**: Compilación automática
- **Sass**: Sintaxis highlighting
- **Live Server**: Servidor de desarrollo

### Configuración de Live Sass Compiler

```json
// settings.json
{
    "liveSassCompile.settings.formats": [
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": "/utils/css"
        }
    ],
    "liveSassCompile.settings.generateMap": true,
    "liveSassCompile.settings.autoprefix": ["> 1%", "last 2 versions"]
}
```

## 🐛 Solución de Problemas Comunes

### Problema: Los estilos no se cargan

**Solución**: Verificar la ruta del CSS en HTML
```html
<!-- Incorrecto -->
<link rel="stylesheet" href="/utils/css/styles.css">

<!-- Correcto -->
<link rel="stylesheet" href="utils/css/styles.css">
```

### Problema: Permisos de archivo

```bash
# Cambiar propietario
sudo chown -R $USER:$USER SASS_Pruebas/

# Verificar permisos
ls -la
```

### Problema: SASS no se compila

```bash
# Verificar si SASS está instalado
sass --version

# Reinstalar si es necesario
npm uninstall -g sass
npm install -g sass
```

## 📚 Recursos Adicionales

### Documentación Oficial
- [SASS Official Documentation](https://sass-lang.com/documentation)
- [SASS Guidelines](https://sass-guidelin.es/)

### Tutoriales Recomendados
- [SASS Crash Course](https://www.youtube.com/watch?v=nu5mdN2JIwM)
- [Advanced SASS](https://www.youtube.com/watch?v=roywYSEPSvc)

### Herramientas Útiles
- [SassMeister](https://www.sassmeister.com/) - Playground online
- [Sassifier](http://sassifier.com/) - Convertir CSS a SASS

## 👥 Contribuir

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/nueva-caracteristica`)
3. Commit tus cambios (`git commit -am 'Agregar nueva característica'`)
4. Push a la rama (`git push origin feature/nueva-caracteristica`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia ISC. Ver el archivo [LICENSE](LICENSE) para más detalles.

## 📞 Contacto

- **Autor**: CB
- **GitHub**: [cristianbarreiro](https://github.com/cristianbarreiro)
- **Proyecto**: [SASS_Pruebas](https://github.com/cristianbarreiro/SASS_Pruebas)

---

⭐ **¡No olvides dar una estrella al proyecto si te ha sido útil!**