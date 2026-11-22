# Atlas Fiscal Europeo | European Tax Atlas

**Comparador interactivo de fiscalidad del trabajo en Europa**, basado en escenarios fiscales de la OCDE y Eurostat. Compara el IRPF efectivo, las cotizaciones del trabajador, la cuña fiscal completa (*tax wedge*) y el tipo marginal personal neto. Incluye salarios expresados en estándares de poder adquisitivo (PPS), selección de países y exportación de gráficos y datos.

**Interactive European labour-tax comparator** with Spanish/English interface, OECD and Eurostat data, PPP-adjusted earnings, and exportable charts.

## Abrir la web / Open the website

Una vez publicado en GitHub Pages:

`https://TU-USUARIO.github.io/atlas-fiscal-europeo/`

Sustituye `TU-USUARIO` por tu usuario de GitHub.

Para ejecutarla localmente, abre `index.html` en un navegador moderno. No necesita servidor ni instalar dependencias: el CSS, JavaScript y los datos utilizados están integrados en el HTML.

## Funcionalidades

- Interfaz en **español e inglés**.
- Fuente **OCDE (2025)**: hasta 201 niveles salariales modelizados por país (50–250% del salario medio).
- Fuente **Eurostat (serie histórica del archivo)**: escenarios salariales publicados por país y año.
- Indicadores: IRPF efectivo, IRPF + cotizaciones del trabajador, cuña fiscal completa OCDE y tipo marginal personal neto OCDE.
- Eje salarial en PPS o en porcentaje del salario medio nacional.
- Rombo de referencia en el 100% del salario medio nacional.
- Descargas de PNG, SVG y CSV.

## Fuentes de datos

1. **OCDE** — `DF_TW_DECOMP`, Taxing Wages decomposition, versión 2.1, datos de 2025. [OECD Data Explorer](https://data-explorer.oecd.org/).
2. **Eurostat** — [`earn_nt_net`](https://ec.europa.eu/eurostat/databrowser/view/earn_nt_net/default/table?lang=en), Annual net earnings.
3. **Eurostat** — [`prc_ppp_ind_1`](https://ec.europa.eu/eurostat/databrowser/view/prc_ppp_ind_1/default/table?lang=en), PPP para consumo individual efectivo (AIC).

Los datos utilizados están incorporados en `index.html` para permitir el uso sin conexión. **No se actualizan automáticamente**. La documentación de validación y fórmulas se encuentra en [`docs/auditoria.md`](docs/auditoria.md).

## Metodología en breve

- **IRPF efectivo:** impuesto sobre la renta dividido por salario bruto.
- **IRPF + cotizaciones personales:** suma de ambos conceptos dividida por salario bruto.
- **Cuña fiscal OCDE:** impuestos personales, cotizaciones personales y empresariales e impuestos sobre nómina, menos prestaciones monetarias, divididos por **coste laboral total** (no por salario bruto).
- **Salario en PPS:** salario expresado en moneda nacional dividido por el factor PPA en moneda nacional por PPS, utilizando la categoría AIC.

**Interpretación:** los puntos OCDE son escenarios fiscales modelizados, no declaraciones individuales. La comparación PPS aproxima el poder adquisitivo de los salarios brutos, no simula necesariamente un mismo salario para todos los países. La cobertura y las definiciones difieren entre OCDE y Eurostat; no deben mezclarse sin armonización. El indicador de cuña fiscal solo se ofrece donde existen sus componentes.

## Publicación con GitHub Pages

En **Settings → Pages → Build and deployment**, selecciona **Deploy from a branch**, rama **main**, carpeta **/(root)**, y guarda. GitHub Pages publicará el archivo `index.html` de la raíz.

## Estructura

```text
atlas-fiscal-europeo/
├── index.html           # Aplicación web completa
├── README.md            # Presentación y fuentes
├── .nojekyll            # Publicación directa de archivos estáticos
└── docs/
    └── auditoria.md    # Diagnóstico, fórmulas y validación
```

## Autoría y licencia

Autor indicado en el gráfico: **@jongonzlz**.

No se ha añadido una licencia de reutilización del código. Si deseas permitir expresamente su copia, modificación o redistribución, selecciona una licencia adecuada (por ejemplo, MIT para el código), respetando las condiciones de atribución y reutilización de los datos de terceros.
