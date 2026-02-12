# ⚔ Ranking Selectivo — Esgrima Colombia

Dashboard interactivo para el seguimiento del ranking de selección de la **Selección Colombiana de Esgrima**.

Permite visualizar puntajes por arma, comparar el rendimiento entre esgrimistas a lo largo de la temporada y actualizar los datos fácilmente subiendo un nuevo archivo Excel — todo desde el navegador, sin necesidad de servidor ni base de datos.

---

## Qué hace

### Ranking por arma

El dashboard organiza los resultados en 6 categorías: Espada, Sable y Florete, cada una en Femenino y Masculino. Al seleccionar una pestaña se muestra la tabla de ranking correspondiente con todos los esgrimistas que participaron en esa categoría.

### Tabla de puntajes

Cada fila es un esgrimista. Las columnas representan las competencias en orden cronológico, y la última columna muestra el total acumulado. Los primeros 4 puestos se resaltan visualmente. Si un esgrimista participó en una competencia pero obtuvo 0 puntos, se muestra `0`; si no participó, se muestra `–`.

### Gráfica de evolución

Debajo de la tabla hay una gráfica de líneas que muestra cómo fue acumulando puntos cada esgrimista competencia tras competencia. Se grafican los 8 mejores de cada categoría para mantener la lectura clara.

---

## Cómo actualizar los datos

El dashboard viene con datos precargados, pero está diseñado para ser actualizado cada vez que haya nuevos resultados. El proceso es simple:

1. Haz clic en **"↑ Actualizar Datos"** (esquina superior derecha).
2. Ingresa la contraseña de administrador.
3. Arrastra o selecciona tu archivo `.xlsx`.
4. Listo — la tabla y la gráfica se actualizan al instante.

### Formato del archivo Excel

El archivo debe tener **una sola hoja** con las siguientes columnas (los nombres deben coincidir exactamente):

| Columna | Descripción | Ejemplo |
|---------|-------------|---------|
| `Esgrimista` | Nombre completo | Maria Jaramillo |
| `arma` | Código de arma | EF, EM, SF, SM, FF, FM |
| `Fecha` | Fecha de la competencia | 2022-02-06 |
| `competencia` | Nombre de la competencia | Montelimar |
| `coeficiente` | Nivel de la competencia | 1, 3 o 6 |
| `puesto` | Posición obtenida | 21 |
| `pasó poules` | Si pasó la fase de poules | 1 (sí) o 0 (no) |
| `calculo` | Cálculo bruto de puntos | 14 |
| `puntos` | Puntos finales otorgados | 14 |

Los datos dentro del archivo pueden variar entre temporadas (distintos esgrimistas, competencias, fechas, puntajes) — lo que importa es que la estructura de columnas se mantenga igual.

### Dónde se guardan los datos actualizados

Los nuevos datos se almacenan en el **localStorage** del navegador. Esto significa que persisten entre sesiones y recargas de página, pero son locales al navegador y dispositivo donde se subieron. Otros visitantes del sitio seguirán viendo los datos precargados por defecto hasta que ellos mismos suban un archivo.

Para volver a los datos originales: abre las herramientas de desarrollador del navegador → Application → Local Storage → elimina la clave `fencing-ranking-2022-v2`.

---

## Cómo publicar en GitHub Pages

### 1. Crear el repositorio

Crea un repositorio nuevo en [github.com/new](https://github.com/new) y clónalo:

```bash
git clone https://github.com/TU_USUARIO/TU_REPOSITORIO.git
cd TU_REPOSITORIO
```

### 2. Agregar los archivos

Copia los dos archivos en la carpeta del repositorio. Renombra el HTML a `index.html` para que GitHub Pages lo use como página principal:

```
TU_REPOSITORIO/
├── index.html      ← (era ranking_selectivo_2022.html)
└── README.md
```

### 3. Subir y activar

```bash
git add .
git commit -m "Ranking selectivo esgrima"
git push origin main
```

Luego en GitHub: **Settings → Pages → Source: main / root → Save**.

En unos minutos el sitio estará en `https://TU_USUARIO.github.io/TU_REPOSITORIO/`.

---

## Detalles técnicos

### Arquitectura

Es un archivo HTML único con todo el CSS y JavaScript inline. No usa frameworks ni backend. Los datos iniciales están embebidos como un arreglo JSON dentro del script.

### Dependencias externas (CDN)

| Recurso | Para qué se usa |
|---------|-----------------|
| Google Fonts (DM Sans, DM Mono) | Tipografía |
| Chart.js 4.4.1 | Gráfica de evolución |
| SheetJS 0.18.5 | Lectura de archivos Excel (se carga solo al abrir el modal de actualización) |

Requiere conexión a internet para cargar estas librerías.

### Códigos de arma

| Código | Arma | Género |
|--------|------|--------|
| EF | Espada | Femenino |
| EM | Espada | Masculino |
| SF | Sable | Femenino |
| SM | Sable | Masculino |
| FF | Florete | Femenino |
| FM | Florete | Masculino |
