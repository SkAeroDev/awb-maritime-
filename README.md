# Maritime Satellite-Grade AWB Templates

This subdirectory contains specialized HTML email templates designed to survive the strict filters, low bandwidth, and legacy rendering environments of vessels at sea.

## 🚢 Supported Templates

### 1. Dualog / Standard Satellite Edition
* **File**: `awb-DUALOG-MARITIME-v2.html`
* **Target Platforms**: Vessels using **Dualog Mail**, **Inmarsat FleetBroadband**, **KVH CommBox**, or **Starlink Maritime** running desktop email clients.
* **Key Specs**:
  * **Size**: ~17.3 KB (well below standard 28 KB satellite delivery warning threshold).
  * **Images**: **Zero external images** (logo is replaced with pure, styled text to prevent bandwidth billing).
  * **Style Block**: None. Every CSS style is declared strictly inline on the specific tag to prevent it from being stripped by vessel mail servers.
  * **Outlook Support**: Includes Microsoft Word engine wrappers (`[if (gte mso 9)|(IE)]`) and high-DPI scaling configurations (`o:OfficeDocumentSettings`) to prevent layout distortion on legacy Outlook 2007–2016 desktop terminals.

### 2. Iridium / Ultra-Low Bandwidth Edition
* **File**: `awb-IRIDIUM-v2.html`
* **Target Platforms**: Vessels using **Iridium Mail & Web**, **Iridium GO!**, or older bridge systems with strict size limit gateways.
* **Key Specs**:
  * **Size**: **6.74 KB** (guarantees automatic delivery and bypasses manual request verification gates on 5KB–10KB filters).
  * **HTML Standard**: Strictly written in **HTML 3.2** (uses classic markup attributes like `bgcolor`, `cellpadding`, and `<font>` tags).
  * **CSS Styling**: **None**. All CSS style blocks and inline styling attributes are stripped to prevent gateway parsing crashes and save precious bytes.
  * **Viewport Width**: Shrunk to **480px** to fit older, low-resolution bridge monitors without requiring horizontal scrollbars.

---

## ⚙️ Engineering Constraints (Why they exist)

| Constraint | Dualog Standard Edition | Iridium Legacy Edition |
| :--- | :--- | :--- |
| **DPI & Layout Wrapper** | Re-added namespaces and `[if mso]` wrappers to lock width on desktop Outlook. | Stripped completely. Viewport scaled down to 480px to save every single byte. |
| **Spam & Security Metrics** | Contains modern tags (`rel="noopener noreferrer"`) for modern web views. | Simplified to basic links to remain compatible with HTML 3.2 parsers. |
| **Progress Bar Layout** | Preserves status colors. Labels use `white-space: nowrap` to prevent wrapping. | Shortened labels (`DEST`, `DELIV`) to fit the narrow 480px table grid. |
| **Fonts & Fallbacks** | Arial/Tahoma stack declared inline. | Standard Arial/Tahoma wrapped in classic HTML `<font>` tags. |

---

## 🚀 Deployment Instructions

1. **Static Testing**: Open the files directly in a web browser to verify table structures.
2. **Variable Injection**: Replace the placeholder variables (such as AWB numbers, flights, and ETA dates) with dynamic placeholders suitable for your CRM or logistics system (e.g., CargoWise, SendGrid, Mailgun).
3. **Bandwidth Optimization**: For vessel deliveries, prioritize routing the **Iridium Edition** to vessels operating under legacy L-band satellite connections, and the **Dualog Edition** to vessels equipped with standard VSAT/Starlink.
