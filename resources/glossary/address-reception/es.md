## DIRECCIÓN DE RECEPCIÓN

Información utilizada para recibir bitcoins. Una dirección se construye generalmente mediante el hash de una clave pública, usando `SHA256` y `RIMPEMD160`, y añadiendo metadatos a este resumen. Las claves públicas utilizadas para construir una dirección de recepción son parte de la cartera del usuario y, por lo tanto, se derivan de su semilla. Por ejemplo, las direcciones SegWit están compuestas por la siguiente información:
* Un HRP para designar "bitcoin": `bc`;
* Un separador: `1`;
* La versión de SegWit utilizada: `q` o `p`;
* La carga útil: el resumen de la clave pública (o directamente la clave pública en el caso de Taproot);
* La suma de control: un código BCH.

Pero una dirección de recepción también puede representar algo diferente dependiendo del modelo de script utilizado. Por ejemplo, las direcciones P2SH se construyen usando el hash del script. Las direcciones Taproot, por su parte, contienen directamente la clave pública modificada (*tweaked*) sin que sea hasheada.

Una dirección de recepción puede representarse en forma de una cadena de caracteres alfanuméricos o como un código QR. Cada dirección puede utilizarse varias veces, pero es una práctica muy desaconsejada. De hecho, con el objetivo de mantener un cierto nivel de privacidad, se recomienda usar cada dirección Bitcoin solo una vez. Es necesario generar una nueva para cada pago entrante hacia su cartera. Una dirección está codificada en `Bech32` para las direcciones SegWit V0, en `Bech32m` para las direcciones SegWit V1, y en `Base58check` para las direcciones Legacy. Desde un punto de vista técnico, una dirección no permite realmente recibir bitcoins, sino más bien bloquear bitcoins usando un script, poniendo restricciones sobre su gasto.

![](../../dictionnaire/assets/23.webp)