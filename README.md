# juice-shop-security-lab

Proyecto 5b del portfolio de QA de Basilio Montes: medición de la detección de vulnerabilidades de OWASP Juice Shop con OWASP ZAP, sobre un conjunto de retos fijado de antemano.

Estado: en curso. Alcance en `docs/retos-elegidos.md`. Todavía no hay mediciones.

## Qué se mide
- Detección: de los 12 retos elegidos, cuántos detecta ZAP.
- Cobertura por categoría del OWASP Top 10 (2021).
- Falsos positivos contados a mano.
- Brechas: retos que ZAP no detecta, anotados como revisión manual.

## Limitación
Un escáner automático no cubre el OWASP Top 10. Control de acceso y lógica de negocio requieren revisión manual. La cifra reportada es "de los retos elegidos, cuántos detecta ZAP", no la seguridad de Juice Shop.

## Entorno
- Aplicación: OWASP Juice Shop en local (localhost), imagen Docker oficial, versión fijada en `resultados/resultados.json` (pendiente).
- Herramienta: OWASP ZAP, contra localhost únicamente.
- Mediciones en el Mac del autor.
