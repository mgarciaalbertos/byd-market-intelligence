[README.md](https://github.com/user-attachments/files/28009553/README.md)
# BYD Market Intelligence Spain — Dashboard v2.0

Panel de inteligencia de mercado del sector automovilístico español, enfocado en el seguimiento de la posición competitiva de BYD en el mercado de turismos (PC).

---

## ¿Qué es esto?

`generar_dashboard.py` es un script Python que procesa los datos de matriculaciones del mercado español y genera un único archivo HTML autocontenido (`index.html`) con todas las visualizaciones interactivas. El archivo resultante se puede abrir en cualquier navegador sin instalaciones adicionales, o publicar en GitHub Pages para acceso compartido.

---

## Fuentes de datos requeridas

Todos los archivos deben estar en la carpeta `DATA RAW/` junto al script.

| Archivo | Descripción |
|---|---|
| `Mercado_ideauto_YYYY.xlsx` | Matriculaciones nacionales PC, años 2018–año actual |
| `CP_ideauto_YYYY.xlsx` | Matriculaciones por Código Postal (archivos anuales o por semestre H1/H2) |
| `bastidores_BYD.xlsx` | Registro interno de bastidores BYD por concesionario, canal y operador |
| `OFICINA_BYD_YYYYMMDD.xlsx` | Datos de flota ARVAL — hoja `Flota` con columna `CHASIS` para identificar vehículos BYD Renting |

> Los archivos CP de más de 30MB vienen partidos por semestre (`_H1.xlsx` / `_H2.xlsx`). El script los concatena automáticamente.

---

## Requisitos técnicos

```bash
pip install pandas openpyxl
```

Python 3.8 o superior. No requiere librerías adicionales para generar el HTML.

---

## Ejecución

```bash
cd "ruta/a/la/carpeta"
python generar_dashboard.py
```

El script genera `dashboard/index.html`. El proceso tarda entre 2 y 5 minutos según el volumen de datos CP.

**Salida esperada:**
```
BYD Market Intelligence  Generando dashboard v2.0...
Leyendo datos de: DATA RAW
   Leyendo 2022... OK 813,373 uds
   ...
Dashboard v2.0 generado correctamente.
Archivo: dashboard/index.html
```

---

## Secciones del dashboard

| Sección | Contenido |
|---|---|
| **KPIs** | Resumen ejecutivo: volumen total mercado, cuota NEV, posición BYD, mix canal |
| **Mercado** | Evolución histórica del mercado PC, rankings fabricantes y marcas |
| **Electrificación** | Mix energético (ICE/MHEV/HEV/PHEV/BEV) mercado y BYD |
| **Canales** | Distribución B2C / B2B / RAC y peso del renting |
| **Rankings** | Top fabricantes, marcas y modelos por periodo |
| **BYD** | Performance BYD: evolución, modelos, mix canal, cuota |
| **Marca** | Buscador — radiografía de cualquier marca del mercado |
| **OEM Chinos** | Seguimiento competitivo BYD vs MG, OMODA, JAECOO, EBRO, DEEPAL, Leapmotor |
| **Operadores** | Actividad de operadores de renting por CP (ARVAL, AYVENS, ATHLON, ALPHABET…) |
| **BYD Renting** | Análisis del producto BYD Renting: tipología cliente, operadores, modelos |
| **Direct/Indirect** | Análisis canal directo vs indirecto, clientes directos, red concesionarios |
| **Concesionario** | Radiografía individual de concesionario: KPIs, modelos, cuotas por CP, benchmark red |

---

## Funcionalidades interactivas

- **Selector de periodo** — YTD o mes individual (Ene, Feb, Mar…)
- **Dark / Light mode** — botón en el header; preferencia guardada en el navegador
- **Filtros de canal** — Todo / B2C / B2B / B2B Renting en tablas y charts
- **Buscador de marca** — búsqueda libre sobre cualquier marca del mercado
- **Buscador de concesionario** — radiografía completa incluyendo benchmark vs red BYD
- **Exportar PDF** — genera un PDF del estado actual del dashboard

---

## Actualización mensual

1. Añadir los nuevos archivos `Mercado_ideauto_YYYY.xlsx` y `CP_ideauto_YYYY.xlsx` a `DATA RAW/`
2. Actualizar `bastidores_BYD.xlsx` con las nuevas matriculaciones
3. Ejecutar `python generar_dashboard.py`
4. Subir el nuevo `dashboard/index.html` a GitHub

```bash
# Con Git (recomendado)
cd byd-market-intelligence
copy "ruta\dashboard\index.html" index.html
git add index.html
git commit -m "Dashboard actualizado - Mayo 2026"
git push
```

El dashboard está publicado en:
**https://mgarciaalbertos.github.io/byd-market-intelligence/**

---

## Estructura del proyecto

```
📁 BYD Market Intelligence/
├── generar_dashboard.py       ← Script principal
├── README.md                  ← Este archivo
├── 📁 DATA RAW/
│   ├── Mercado_ideauto_2024.xlsx
│   ├── Mercado_ideauto_2025.xlsx
│   ├── Mercado_ideauto_2026.xlsx
│   ├── CP_ideauto_2025_H1.xlsx
│   ├── CP_ideauto_2025_H2.xlsx
│   ├── CP_ideauto_2026.xlsx
│   ├── bastidores_BYD.xlsx
│   └── OFICINA_BYD_20260504.xlsx
└── 📁 dashboard/
    └── index.html             ← Output generado
```

---

## Definiciones clave

| Término | Definición |
|---|---|
| **PC** | Passenger Cars — turismos. Mercado base de todo el análisis |
| **NEV** | New Energy Vehicle = PHEV + BEV |
| **B2B Renting** | Filtro compuesto: `Canal = B2B` AND `Renting = Renting` |
| **Venta Directa** | Matrícula facturada directamente al cliente final (sin concesionario) |
| **Venta Indirecta** | Matrícula a través de la red de concesionarios |
| **BYD Renting** | Vehículos BYD en flota ARVAL identificados por cruce de bastidor (VIN) |
| **ARVAL comercial** | Operaciones ARVAL donde BYD es proveedor libre, no producto BYD Renting |
| **Hub renting** | CP 28108 (Alcobendas) y otros CPs madrileños que son domicilio fiscal de operadores |

---

## Contacto

Manuel García — Director B2B, BYD España
