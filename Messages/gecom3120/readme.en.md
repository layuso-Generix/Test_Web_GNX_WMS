## GECOM31 (EAN) — Modification Product Master Data (EAN)

Message for declaring and maintaining of the modification the **product EAN/EDI codes** in the Generix Spain WMS.
It complements modification the **GECOM31** product master by allowing the multiple barcodes associated with each item to be declared independently.

### Key Features

- **Flow direction:** Outbound — the WMS publishes this message to the client endpoint (`POST https://[URL_Client]/endpoint`). The ERP must expose and process it.
- **Product identification:** The combination of activity (`CODACT`), product (`CODPRO`) and logistics variant (`VALPRO`) links the EAN code with its item in the master.
- **EDI code (EDIPRO):** This is the barcode itself, with its associated designation (`EANDS1`).
- **Main or secondary code (EDIPRM):** Distinguishes the primary code (`true`) from the secondary one (`false`). Each product must have a single primary code per level.
- **Level qualifier (EDIQLF):** Indicates which logistics unit the code corresponds to: CSU (`0`), multi-product batch (`1`), SPCB (`2`), PCB (`3`), case (`4`) or pallet (`5`).

> **Important note:** This message decouples EAN code management from the main product master. The product referenced in `CODPRO` must already exist, declared via **GECOM31**. The required fields are `TRTEXC`, `CODACT`, `CODPRO`, `EDIPRO`, `EDIPRM` and `EDIQLF`.
>!green The **RCTEXC** field must be correctly populated, as it is essential for routing messages to the appropriate WMS library. The value for this field differs between the test and production environments. The correct value can be provided by the WMS consultant.

### Integration

This message is sent automatically by the WMS when the warehouse amend the EANs tab in the WMS master data.The ERP must keep an active and accessible endpoint to receive the notifications and update the order information.