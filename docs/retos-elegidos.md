# Retos elegidos · OWASP Juice Shop (BORRADOR, 9/11/2026)

Estado: BORRADOR. La lista concreta de 12 retos NO está cerrada. Falta verificarla contra el marcador (Score Board) de la versión de Juice Shop que se fije en local. No se listan nombres de retos hasta comprobarlos en esa versión.

## Criterio de selección
- Un reto entra si su explotación se puede verificar sin ambigüedad en la propia aplicación.
- Entre 1 y 2 retos por categoría del OWASP Top 10 (2021), omitiendo las categorías sin reto claro en la versión fijada.
- Se fija antes de ejecutar ZAP. No se cambia después de medir.

## Categorías del Top 10 a cubrir
| Categoría | Retos a elegir | Nota |
|---|---|---|
| A01 Control de acceso | 2 | Revisión manual, ZAP suele fallar aquí |
| A02 Fallos criptográficos | 1 | |
| A03 Inyección | 2 | |
| A04 Diseño inseguro | 1 | Revisión manual |
| A05 Configuración insegura | 2 | |
| A06 Componentes vulnerables | 1 | |
| A07 Fallos de identificación y autenticación | 1 | |
| A08 Fallos de integridad de datos | 1 | |
| A09 Fallos de registro y monitorización | 0 o 1 | Si la versión tiene reto claro |
| A10 SSRF | 1 | |

Total previsto: 12 retos. Las categorías y el número pueden ajustarse al marcador real; los cambios se anotan aquí antes de medir.

## Predicciones (antes de medir)
- ZAP detecta entre 4 y 6 de los 12 retos.
- Detecta mejor A03 y A05 que A01 y A04.
- Falla en los retos de control de acceso que dependen de cambiar un identificador de otro usuario.
- Entre 0 y 3 falsos positivos, sobre todo en cabeceras y configuración.

## Pendiente
1. Fijar la versión de Juice Shop (imagen Docker oficial, la más reciente estable en el momento de empezar).
2. Copiar el listado de retos del marcador de esa versión.
3. Elegir los 12 retos aplicando el criterio y escribir la lista final aquí, con su categoría OWASP.
