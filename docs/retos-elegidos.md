# Retos elegidos · OWASP Juice Shop v20.2.0 (PROPUESTA, 9/11/2026)

Estado: PROPUESTA pendiente de confirmación. Versión medida: imagen Docker `bkimminich/juice-shop:v20.2.0`, con el marcador filtrado a dificultad 1 y 2 estrellas y con los retos deshabilitados en Docker ocultos (18 en esta versión).

## Criterio de selección
- Solo retos habilitados en Docker, con dificultad 1 o 2 estrellas.
- Se excluyen los que requieren una API de LLM externa (AI Debugging, Chatbot Prompt Injection) y los de Web3 (Web3 Sandbox, NFT Takeover), porque dependen de servicios que no controlamos en local.
- Se excluye Score Board: ya aparece resuelto al abrir el marcador y no prueba ninguna vulnerabilidad.
- Un reto entra si su explotación se puede verificar sin ambigüedad en la aplicación.
- Máximo 2 retos por categoría del OWASP Top 10 (2021).
- La lista se fija antes de ejecutar ZAP y no se cambia después de medir.

## Retos propuestos (11 de 12)

| # | Reto | Etiqueta de Juice Shop | Dificultad | Categoría OWASP 2021 |
|---|---|---|---|---|
| 1 | Admin Section | Broken Access Control | 2 | A01 Control de acceso |
| 2 | View Basket | Broken Access Control | 2 | A01 Control de acceso |
| 3 | Weird Crypto | Cryptographic Issues | 2 | A02 Fallos criptográficos |
| 4 | Password Hash Leak | Sensitive Data Exposure | 2 | A02 Fallos criptográficos |
| 5 | Login Admin | Injection | 2 | A03 Inyección |
| 6 | DOM XSS | XSS | 1 | A03 Inyección |
| 7 | Zero Stars | Improper Input Validation | 1 | A04 Diseño inseguro |
| 8 | Error Handling | Security Misconfiguration | 1 | A05 Configuración insegura |
| 9 | Misplaced IaC Files | Security Misconfiguration | 2 | A05 Configuración insegura |
| 10 | Password Strength | Broken Authentication | 2 | A07 Fallos de autenticación |
| 11 | Exposed Metrics | Observability Failures | 1 | A09 Fallos de registro y monitorización |

Nota sobre las categorías: el mapeo de la tabla es orientativo. Juice Shop etiqueta sus retos con sus propias categorías y no siempre coinciden con el Top 10 2021; cuando haya duda, se anota aquí la decisión antes de medir.

## Hueco pendiente (12.º reto)
Faltan categorías por cubrir: A06 Componentes vulnerables, A08 Integridad de datos (deserialización) y A10 SSRF. Las capturas de esta ronda no muestran retos de esas etiquetas con dificultad 1 o 2 habilitados en Docker. El 12.º reto se elegirá de una de ellas cuando se vea el marcador filtrado por esa etiqueta. Mientras tanto, no se cuenta como elegido.

## Predicciones (antes de medir, por reto)
Esperamos que ZAP detecte:
- Login Admin (inyección SQL en el login): probable.
- DOM XSS: posible, depende de si ZAP ejecuta la parte del cliente.
- Error Handling (error sin control): posible, por la respuesta de error.
- Exposed Metrics: poco probable; es un endpoint de monitorización que ZAP no adivina sin pistas.

Esperamos que ZAP NO detecte:
- Admin Section, View Basket (control de acceso): es lógica de negocio, revisión manual.
- Weird Crypto: requiere criterio humano (no es un fallo que se vea en la respuesta).
- Password Hash Leak, Password Strength, Zero Stars, Misplaced IaC Files: requieren revisión manual o no tienen firma automática.

Predicción global: ZAP detecta entre 3 y 5 de los 11 retos propuestos. Falsos positivos: entre 0 y 3, sobre todo en cabeceras y configuración.

## Excluidos (deshabilitados o dependientes de servicios externos)
- AI Debugging y Chatbot Prompt Injection: requieren LLM API.
- Web3 Sandbox y NFT Takeover: Web3, dependen de servicios externos.
- Score Board: ya resuelto, no prueba vulnerabilidades.
- Otros 18 retos ocultos por estar deshabilitados en Docker (no revisados uno a uno).

## Pendiente
1. Confirmar la lista de 11 y elegir el 12.º reto (A06, A08 o A10) cuando se vea el marcador filtrado.
2. Escribir las predicciones definitivas por reto antes de ejecutar ZAP.
