## GECOM31 (EAN) — Modification Product Master Data (EAN)

Mensaje para la declaración y mantenimiento de las modificaciones de los **códigos EAN/EDI de producto** en el WMS Generix Spain.
Complementa a la modificación del maestro de productos **GECOM31** permitiendo declarar de forma independiente los múltiples códigos de barras asociados a cada artículo.

### Características Principales

- **Dirección del flujo:** Outnound — el WMS publica este mensaje en el endpoint del cliente (`POST https://[URL_Client]/endpoint`). El ERP debe exponerlo y procesarlo.
- **Identificación del producto:** La combinación de actividad (`CODACT`), producto (`CODPRO`) y variante logística (`VALPRO`) enlaza el código EAN con su artículo en el maestro.
- **Código EDI (EDIPRO):** Es el código de barras propiamente dicho, con su designación asociada (`EANDS1`).
- **Código principal o secundario (EDIPRM):** Distingue el código primario (`true`) del secundario (`false`). Cada producto debe tener un único código primario por nivel.
- **Cualificador de nivel (EDIQLF):** Indica a qué unidad logística corresponde el código: CSU (`0`), lote multiproducto (`1`), SPCB (`2`), PCB (`3`), caja (`4`) o palé (`5`).

> **Nota importante:** Este mensaje desacopla la gestión de códigos EAN del maestro de producto principal. El producto referenciado en `CODPRO` debe existir previamente, declarado mediante **GECOM31**. Los campos obligatorios son `CODACT`, `CODPRO`, `EDIPRO`, `EDIPRM` y `EDIQLF`.
>!green El campo **RCTEXC** es muy importante que este correctamente cumplimentado, para poder redirigir los mensajes a la librería de WMS correcta. La información de este valor es diferente para test y producción, el dato podrá ser proporcionado por el consultor WMS.

### Integración

Este mensaje es enviado automáticamente por el WMS cuando modifica la ficha de EAN's del maestro de WMS. El ERP debe mantener un endpoint activo y accesible para recibir las notificaciones y actualizar la información del pedido.