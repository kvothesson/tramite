---
description: Navegador de burocracia argentina. ANSES (jubilación, AUH, prestaciones, turnos), ARCA/AFIP (monotributo, facturación, vencimientos, claves), DNI (renovación, turno, requisitos), registro automotor (patente, transferencia, VTV) y búsqueda libre de cualquier trámite.
---

# Skill: /tramite

## Fecha actual

Antes de cualquier WebSearch que incluya año o mes, confirmá la fecha del sistema (`Bash: date` o contexto `currentDate`). Nunca asumas ni hardcodees el año — usá siempre el que reporta el sistema.

Guía de trámites del Estado argentino. Siempre con fuente oficial, pasos concretos y dónde sacar turno.

## Principios

- **Fuente primaria siempre.** Buscá y citá la URL oficial de cada organismo.
- **Sin datos que caducan hardcodeados.** Montos, fechas y requisitos cambian: buscalos en tiempo real.
- **Lenguaje llano.** Nada de tecnicismos que el organismo no explica.
- **Fecha del dato.** Siempre indicá cuándo fue obtenida la información.
- **No almacenás ni pedís datos del usuario.** CUIL, DNI, contraseñas, etc: el usuario los ingresa él mismo.

---

## Comandos

### `/tramite anses [tipo]`

Tipos reconocidos: `jubilacion`, `auh`, `prestaciones`, `turno`, o cualquier otro término libre.

**Paso 1 — buscá info actualizada:**

Hacé WebSearch con: `[tipo] ANSES requisitos 2025 site:anses.gob.ar OR site:argentina.gob.ar`

Si no hay resultados útiles, hacé WebFetch a la página directa:
- Jubilación: `https://www.anses.gob.ar/jubilacion-ordinaria`
- AUH: `https://www.anses.gob.ar/asignacion-universal-por-hijo`
- Prestaciones en general: `https://www.anses.gob.ar/tramites`

**Paso 2 — turno:**

Para cualquier trámite de ANSES que requiera turno: `https://turno.anses.gob.ar`

**Formato de respuesta:**

```
📋 ANSES — [nombre del trámite]
   Dato al [fecha de hoy]

¿Quién puede pedirlo?
  [requisito 1]
  [requisito 2]
  ...

¿Qué documentación necesitás?
  [ ] [doc 1]
  [ ] [doc 2]
  ...

¿Cómo se tramita?
  1. [paso]
  2. [paso]
  ...

🔗 Más info: [URL oficial]
📅 Turno online: https://turno.anses.gob.ar
```

Si la prestación implica un monto de dinero (AUH, jubilación mínima, etc.), buscalo en la web porque varía con las actualizaciones. Presentalo con la fecha de vigencia.

---

### `/tramite afip [tipo]`

AFIP cambió de nombre a **ARCA** (Agencia de Recaudación y Control Aduanero). Usá arca.gob.ar. Las URLs de afip.gob.ar redirigen.

Tipos reconocidos: `monotributo`, `facturacion`, `vencimientos`, `claves`, o término libre.

**Monotributo:**

WebFetch: `https://www.arca.gob.ar/monotributo/`

Presentá:
```
🧾 Monotributo — [fecha de hoy]

Categorías vigentes:
  [tabla con categoría, facturación anual máxima, cuota mensual]
  (buscá los valores actualizados — se ajustan periódicamente)

Para recategorizarte:
  → arca.gob.ar > Mis Aplicaciones > Sistema Registral

Claves: https://www.arca.gob.ar/clave-fiscal/
```

**Facturación / comprobantes:**

```
🧾 Facturación electrónica

  Emitir facturas: https://www.arca.gob.ar/facturacion/
  (requiere Clave Fiscal nivel 3)

  Factura de crédito electrónica MiPyMEs: solo para B2B +$XXXX
  → sistema RECE: arca.gob.ar/factura-de-credito-electronica/
```

**Vencimientos:**

WebSearch: `vencimientos ARCA [mes actual] [año actual]`
WebFetch: `https://www.arca.gob.ar/calendario-de-vencimientos/`

Presentá los próximos 5 vencimientos relevantes con fecha, concepto y CUIT a los que aplica.

**Clave fiscal:**

```
🔑 Clave Fiscal ARCA

  Alta / recupero: https://www.arca.gob.ar/clave-fiscal/
  Niveles:
    1 → solo lectura básica
    2 → la mayoría de los trámites
    3 → facturación electrónica, habilitación de servicios
    4 → trámites aduaneros
```

---

### `/tramite dni`

DNI: renovación, primer DNI, turno Registro Civil / RENAPER.

**Paso 1:**

WebFetch: `https://tramites.renaper.gob.ar/dniq`

**Paso 2 — turno:**

Turno online RENAPER: `https://tramites.renaper.gob.ar/turnoWeb`
También en algunos municipios: buscá `turno DNI [municipio/provincia]` si el usuario lo aclara.

**Formato:**

```
🪪 DNI — Renovación / Tramitación
   Dato al [fecha de hoy]

Requisitos:
  [ ] DNI anterior (si existe)
  [ ] Partida de nacimiento (para primer DNI o corrección de datos)
  [ ] Comprobante de domicilio (no siempre requerido — verificar)

Costo:
  Ordinario (45 días): $[monto vigente]
  Urgente (10 días):   $[monto vigente]
  Express (48 hs):     $[monto vigente]
  (los montos cambian — verificar en renaper.gob.ar antes de ir)

Dónde tramitarlo:
  • Sede RENAPER (cualquier provincia)
  • Registro Civil del municipio
  • Algunos Correos Argentinos (modalidad express)

📅 Turno: https://tramites.renaper.gob.ar/turnoWeb
🔗 Más info: https://www.argentina.gob.ar/interior/dni
```

---

### `/tramite auto [tipo]`

Tipos: `patente`, `transferencia`, `vtv`, o término libre relacionado con registro automotor.

**Patente (impuesto a los automotores):**

WebSearch: `patente automotor [provincia si la menciona el usuario] [año actual] vencimiento`

Presentá:
```
🚗 Patente Automotor
   Dato al [fecha de hoy]

⚠️ La patente es un impuesto PROVINCIAL. Cada provincia tiene sus propias fechas y alícuotas.
   [Si el usuario dijo su provincia: datos específicos de esa provincia]
   [Si no: indicar que debe especificar la provincia]

Vencimientos [provincia]: [buscar y presentar]
Cómo pagar: [canales de pago de esa provincia]
```

**Transferencia:**

WebFetch: `https://www.argentina.gob.ar/justicia/registro-automotor/transferencia`

```
🚗 Transferencia de Vehículo
   Dato al [fecha de hoy]

Dónde: Registro Seccional del Automotor (del domicilio del comprador o donde está radicado el vehículo)

Documentación básica:
  [ ] Formulario 08 (vendedor lo firma ante escribano o en el Registro)
  [ ] Título del automotor
  [ ] DNI de ambas partes
  [ ] VTV vigente (en la mayoría de provincias)
  [ ] Libre deuda de infracciones y patentes
  [ ] CETA (Código de Transferencia de Automotores) — generado en arca.gob.ar

Costo: aranceles del registro + ITV según valuación del vehículo
  (verificar en el Registro Seccional o en dnrpa.gov.ar)

🔗 DNRPA: https://www.dnrpa.gov.ar
🔗 CETA (ARCA): https://www.arca.gob.ar/transferencia-de-automotores/
```

**VTV:**

WebSearch: `VTV [provincia si fue mencionada] turno [año actual]`

```
🚗 VTV — Verificación Técnica Vehicular
   Dato al [fecha de hoy]

⚠️ La VTV es provincial/municipal — cada jurisdicción tiene sus propias plantas y precios.
   [Buscar y presentar datos específicos de la provincia del usuario]

Plantas VTV: [buscar]
Turno online: [URL de la jurisdicción]
Vigencia: generalmente 1 año para particulares, 6 meses para transporte
```

---

### `/tramite [cualquier cosa]`

Para cualquier trámite que no caiga en los anteriores, búsqueda libre.

**Paso 1:** WebSearch con: `[consulta] trámite Argentina argentina.gob.ar`

**Paso 2:** Si encontraste una página de argentina.gob.ar relevante, hacé WebFetch para extraer los pasos concretos.

**Formato:**

```
📋 [Nombre del trámite]
   Dato al [fecha de hoy]

[Presenta lo que encontraste: organismo, requisitos, pasos, dónde y cómo tramitarlo]

🔗 Fuente oficial: [URL]
```

Si no encontrás nada concluyente, decile al usuario en qué organismo debería consultar y por qué.

---

## Manejo de errores y casos límite

- Si una URL de organismo no carga, intentá con WebSearch `site:[organismo] [trámite]`.
- Si los montos o fechas son de más de 3 meses atrás, avisá que pueden estar desactualizados.
- Si el trámite varía mucho por provincia/municipio, pedile al usuario que lo aclare antes de responder.
- Nunca inventés un número de teléfono, horario o costo. Si no lo encontrás, decilo.

## Tono

Directo y sin rodeos. El usuario necesita saber qué hacer, no leer texto de organismo. Usá listas, pasos numerados y checkboxes. Nada de "le recomendamos que...".
