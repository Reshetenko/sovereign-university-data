---
term: MINISCRIPT
---

Framework que permite proporcionar un marco para programar scripts de manera segura en Bitcoin. El lenguaje nativo de Bitcoin se llama script. Este es bastante complejo de usar en la práctica, especialmente para aplicaciones sofisticadas y personalizadas. Es muy difícil verificar las limitaciones de un script. Miniscript utiliza un subconjunto de scripts de Bitcoin para simplificar su creación, análisis y verificación. Cada miniscript es equivalente 1 a 1 con un script nativo. Se utiliza un lenguaje de Policies fácil de usar, que luego se compila en Miniscript, para finalmente corresponder a un Script nativo.

![](./assets/30.webp)

Miniscript permite así a los desarrolladores construir scripts sofisticados de una manera más segura y confiable. Las propiedades esenciales de Miniscript son las siguientes:
* Permite un análisis estático del script, incluyendo las condiciones de gasto que permite y su costo en términos de recursos;
* Permite realizar scripts que respetan el consenso;
* Permite analizar si sí o no, los diferentes caminos de gasto respetan las reglas estándar de los nodos;
* Permite establecer un estándar general, comprensible y componible, para todos los softwares y hardwares de billetera.

El proyecto Miniscript fue lanzado en 2018 por Peter Wuille, Andrew Poelstra y Sanket Kanjalkar, a través de la empresa Blockstream. Miniscript se añadió al wallet Bitcoin Core en modo watch-only en diciembre de 2022 con la versión 24.0, y luego completamente en mayo de 2023 con la versión 25.0.
