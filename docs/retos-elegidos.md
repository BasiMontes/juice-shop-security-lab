# Retos elegidos · OWASP Juice Shop v20.2.0 (PROPUESTA, 9/11/2026)

Estado: PROPUESTA pendiente de confirmación. Versión medida: imagen Docker `bkimminich/juice-shop:v20.2.0`, con el marcador filtrado a dificultad 1-2 para la selección inicial, y ampliado a 3-5 para revisar A06 y A08. Los retos deshabilitados en Docker se excluyen (18 en esta versión).

## Criterio de selección
- Solo retos habilitados en Docker.
- Dificultad 1 a 5 estrellas. Subido de 1-2 a 1-5 para cubrir A06, que no tenía retos en el rango inicial.
- Se excluyen los que requieren una API de LLM externa (AI Debugging, Chatbot Prompt Injection, Greedy Chatbot Manipulation) y los de Web3 (Web3 Sandbox, NFT Takeover, Wallet Depletion), porque dependen de servicios que no controlamos en local.
- Se excluye Score Board: aparece resuelto al abrir el marcador y no prueba ninguna vulnerabilidad.
- Un reto de explotación entra si su resultado se puede verificar sin ambigüedad en la aplicación.
- Un reto de verificación manual (informar a la tienda) se incluye solo si cubre una categoría sin otro reto; se anota aparte.
- Máximo 2 retos por categoría del OWASP Top 10 (2021).
- La lista se fija antes de ejecutar ZAP y no se cambia después de medir.

## Retos propuestos (11 de explotación + 1 de verificación manual)

| # | Reto | Etiqueta de Juice Shop | Dificultad | Categoría OWASP 2021 | Tipo |
|---|---|---|---|---|---|
| 1 | Admin Section | Broken Access Control | 2 | A01 Control de acceso | Explotación |
| 2 | View Basket | Broken Access Control | 2 | A01 Control de acceso | Explotación |
| 3 | Weird Crypto | Cryptographic Issues | 2 | A02 Fallos criptográficos | Explotación |
| 4 | Password Hash Leak | Sensitive Data Exposure | 2 | A02 Fallos criptográficos | Explotación |
| 5 | Login Admin | Injection | 2 | A03 Inyección | Explotación |
| 6 | DOM XSS | XSS | 1 | A03 Inyección | Explotación |
| 7 | Zero Stars | Improper Input Validation | 1 | A04 Diseño inseguro | Explotación |
| 8 | Error Handling | Security Misconfiguration | 1 | A05 Configuración insegura | Explotación |
| 9 | Misplaced IaC Files | Security Misconfiguration | 2 | A05 Configuración insegura | Explotación |
| 10 | Password Strength | Broken Authentication | 2 | A07 Fallos de autenticación | Explotación |
| 11 | Exposed Metrics | Observability Failures | 1 | A09 Fallos de registro y monitorización | Explotación |
| 12 | Legacy Typosquatting | Vulnerable Components | 4 | A06 Componentes vulnerables | Verificación manual |

Nota sobre las categorías: el mapeo es orientativo. Juice Shop etiqueta sus retos con sus propias categorías, que no siempre coinciden con el Top 10 2021. Cuando haya duda, se anota aquí la decisión antes de medir.

## Categorías sin cobertura
- **A08 Fallos de integridad de datos (deserialización):** sin retos habilitados en Docker. Los tres de la etiqueta (Blocked RCE DoS, Memory Bomb y Successful RCE DoS) aparecen como "potentially harmful on Docker" y están deshabilitados.
- **A10 SSRF:** su reto (SSRF, 7 estrellas) está deshabilitado en Docker.

Estas dos categorías quedan fuera de la medición y se declaran como límite.

## Predicciones (antes de medir, por reto)
Esperamos que ZAP detecte:
- Login Admin (inyección SQL en el login): probable.
- DOM XSS: posible, depende de si ZAP ejecuta la parte del cliente.
- Error Handling (error sin control): posible, por la respuesta de error.
- Exposed Metrics: poco probable; es un endpoint de monitorización que ZAP no adivina sin pistas.

Esperamos que ZAP NO detecte:
- Admin Section, View Basket (control de acceso): lógica de negocio, revisión manual.
- Weird Crypto: requiere criterio humano.
- Password Hash Leak, Password Strength, Zero Stars, Misplaced IaC Files: requieren revisión manual o no tienen firma automática.
- Legacy Typosquatting: es de verificación manual por definición.

Predicción global sobre los 11 de explotación: ZAP detecta entre 3 y 5. Falsos positivos: entre 0 y 3, sobre todo en cabeceras y configuración.

## Excluidos
- LLM: AI Debugging, Chatbot Prompt Injection, Greedy Chatbot Manipulation.
- Web3: Web3 Sandbox, NFT Takeover, Wallet Depletion.
- Score Board: ya resuelto, no prueba vulnerabilidades.
- Deshabilitados en Docker: los 18 ocultos, incluidos SSRF y los de deserialización.

## Pendiente
1. Confirmar la lista de 12.
2. Escribir las predicciones definitivas por reto antes de ejecutar ZAP.
3. Reiniciar el contenedor de Juice Shop antes de cada medición, para que el estado de retos resueltos no afecte.
