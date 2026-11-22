# Auditoría del Atlas Fiscal Europeo — 22 de noviembre de 2026

## Alcance

Revisión de datos OCDE `DF_TW_DECOMP 2.1` (2025), Eurostat `earn_nt_net` (2016–2025) y `prc_ppp_ind_1` (PPA, consumo individual efectivo). Se ha reconstruido la web a partir de los archivos aportados; los HTML de versiones previas no estaban presentes en el entorno de esta revisión.

## Diagnóstico y mejoras aplicadas

| Área | Riesgo o problema | Corrección |
|---|---|---|
| Cuña fiscal | Sumar impuestos y cotizaciones como % del bruto no reproduce el *tax wedge* oficial | Fórmula con cotizaciones empresariales, impuestos sobre nómina, prestaciones y denominador de coste laboral |
| Unidades | Mezclar importes en EUR y factores PPA en moneda nacional | OCDE: moneda nacional / factor PPA. Eurostat: restringir PPS a países que utilizaban el euro en el año seleccionado |
| Disponibilidad | Mostrar cuña fiscal de Eurostat sin variables suficientes | Cuña y marginal disponibles solo para OCDE; opciones desactivadas al cambiar a Eurostat |
| Fuente | Mezclar seis escenarios Eurostat con 201 OCDE en una curva | Selector de fuente, series separadas y etiquetas explícitas |
| Interpretación | Confundir escenarios modelizados con trabajadores observados | Nota explicativa en gráfico y metodología ampliada |
| Visualización | Gráficos poco legibles y leyendas duplicadas | Gráfico ancho, ejes fijos 10.000–100.000 PPS, Y desde 0, rombos 100%, leyenda incluida en exportación |
| Exploración | Falta de información en puntos | Hover con salario bruto en moneda original, PPS, nivel relativo y tasa |
| Internacionalización | Textos solo en castellano | Selector ES/EN para controles, gráfico, leyenda, notas y metodología |
| Exportación | Pérdida de contexto al compartir la imagen | PNG de 5.000 px y SVG con título, leyenda, fuentes y firma |
| Auditoría | Dificultad para replicar cálculos | CSV de escenarios con componentes, denominadores y tasas |

## Fórmulas

- IRPF efectivo = 100 × (−IT_CG − IT_LG) / GWE.
- IRPF + cotizaciones del trabajador = 100 × (−IT_CG − IT_LG − EESSC) / GWE.
- Coste laboral = GWE − ERSSC − PT.
- Cuña fiscal OCDE = 100 × (−IT_CG − IT_LG − EESSC − ERSSC − PT − CB) / LC.
- Salario en PPS = salario en moneda nacional / PPP (unidades de moneda nacional por PPS, categoría AIC).

## Validación cuantitativa

- 38 países OCDE, **7.638** escenarios fiscales completos del perfil soltero sin hijos (201 por país).
- Diferencia absoluta máxima entre cuña reconstruida y `AV_TW` oficial: **5,02 × 10⁻⁹ puntos porcentuales**.
- Error absoluto máximo al conciliar el coste laboral con `GWE − ERSSC − PT`: **8,22 × 10⁻⁶ unidades monetarias**.
- España, salario medio 2025: bruto **32.678,398389 EUR**, cuña **41,444078%**, factor PPA AIC **0,910799**, bruto aproximado **35.879 PPS**.

## Pruebas funcionales

Pruebas en Chromium mediante Playwright con `page.set_content` (la navegación a `file://` y `localhost` está bloqueada en el entorno): inicialización de años y países, alternancia de IRPF, carga personal, cuña y marginal, selección ES/EN, modo Eurostat y año 2018, desactivación de cuña en Eurostat, hover de un rombo y exportación SVG/PNG. Sin excepciones JavaScript durante las pruebas. Exportación PNG comprobada a **5.000 × 3.307 píxeles**.

## Límites pendientes

- No hay simulación fiscal de un salario PPS arbitrario idéntico entre países: los puntos se derivan de salarios relativos a la media de cada país. No se interpolan escenarios.
- La PPA de consumo individual efectivo es una aproximación agregada y no refleja el coste de vida particular de cada hogar.
- No se incluyen otros perfiles familiares, distribuciones salariales, pagos obligatorios no tributarios ni prestaciones en especie.
- Los escenarios OCDE corresponden a 2025; la serie histórica Eurostat presenta cambios metodológicos desde 2024.
- Las diferencias OCDE–Eurostat no se han atribuido causalmente a reformas fiscales.
