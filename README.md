# tramite

Compatible con **Claude Code** y **OpenAI Codex** — navegador de burocracia argentina.

## Qué hace

`/tramite` explica paso a paso cómo hacer trámites del Estado argentino: ANSES, ARCA/AFIP, DNI, registro automotor y cualquier otro. Siempre con fuente oficial, sin datos hardcodeados que se quedan viejos.

## Instalación

```bash
claude --plugin-dir /ruta/a/tramite
```

### OpenAI Codex

No requiere instalación. Codex lee `AGENTS.md` automáticamente al abrirse en este directorio.

```bash
git clone https://github.com/kvothesson/tramite ~/tramite
cd ~/tramite
codex
```

## Comandos y ejemplos

### `/tramite anses auh`

```
📋 ANSES — Asignación Universal por Hijo (AUH)
   Dato al 3 may 2026

¿Quién puede pedirlo?
  Madres, padres o tutores de menores de 18 años (o sin límite si tienen discapacidad)
  que no tengan trabajo en relación de dependencia o sean monotributistas categoría A o B.

¿Qué documentación necesitás?
  [ ] DNI del titular
  [ ] DNI y partida de nacimiento del/los hijo/s
  [ ] Libreta Nacional de Seguridad Social, Salud y Educación (para cobrar el 20% anual)

Monto vigente (mayo 2026):
  $141.285,31 por hijo
  (80% mensual: $113.028,25 — 20% anual al presentar libreta)

¿Cómo tramitarla?
  1. Ingresá a Mi ANSES con CUIL y Clave de la Seguridad Social
  2. Sección "Asignaciones" > "Asignación Universal por Hijo"
  3. Si es primera vez, pedí turno presencial

🔗 Más info: https://www.anses.gob.ar/asignacion-universal-por-hijo
📅 Turno online: https://turno.anses.gob.ar

Fuente: ANSES — anses.gob.ar
```

---

### `/tramite anses jubilacion`

```
📋 ANSES — Jubilación Ordinaria
   Dato al 3 may 2026

¿Quién puede pedirla?
  Hombres: 65 años + 30 años de aportes
  Mujeres: 60 años + 30 años de aportes (pueden optar por jubilarse a los 65)

¿Qué documentación necesitás?
  [ ] DNI
  [ ] Historial laboral (ANSES lo cruza automáticamente con AFIP)
  [ ] Constancias de aportes de empleos informales (si corresponde)

Haber mínimo vigente (mayo 2026):
  $393.174,10 + bono extraordinario $70.000 = $463.174,10

¿Cómo iniciar el trámite?
  1. Verificá tus aportes en Mi ANSES > "Mis datos registrados"
  2. Pedí turno en turno.anses.gob.ar
  3. Presentate con la documentación

🔗 Más info: https://www.anses.gob.ar/jubilacion-ordinaria
📅 Turno online: https://turno.anses.gob.ar

Fuente: ANSES — anses.gob.ar
```

---

### `/tramite afip monotributo`

```
🧾 Monotributo — Categorías vigentes (feb 2026)
   Dato al 3 may 2026

   Categ.   Facturación anual máx.    Cuota mensual (aprox.)
   ──────   ──────────────────────    ─────────────────────
   A        $10.273.463               [consultá en arca.gob.ar]
   B        $15.051.819               [consultá en arca.gob.ar]
   ...      ...                       ...
   K        $108.309.385              [consultá en arca.gob.ar]

   ⚠️ Los montos de cuotas se actualizan trimestralmente.
   Consultá la tabla completa con valores exactos en:
   → https://www.afip.gob.ar/monotributo/categorias.asp

Recategorización:
  Próximo período: enero–febrero cada año (o cuando superás/bajás de categoría)
  Dónde: arca.gob.ar > Mis Aplicaciones > Sistema Registral

Clave Fiscal para operar: https://www.arca.gob.ar/clave-fiscal/

Fuente: ARCA — afip.gob.ar/monotributo
```

---

### `/tramite dni`

```
🪪 DNI — Renovación / Tramitación
   Dato al 3 may 2026

Requisitos:
  [ ] DNI anterior (si existe)
  [ ] En caso de pérdida o robo: denuncia policial
  [ ] Primer DNI: partida de nacimiento

Costos vigentes (desde marzo 2026):
  Ordinario (~45 días): $10.000
  Exprés   (~10 días):  $26.000
  24 horas:             $41.000
  Al instante (oficinas habilitadas): $57.000
  (los montos se actualizan — verificar en argentina.gob.ar antes de ir)

Dónde tramitarlo:
  • Sedes RENAPER en cualquier provincia
  • Registro Civil del municipio
  • Correo Argentino (modalidad exprés en puntos habilitados)

📅 Turno: https://mitramite.renaper.gob.ar
🔗 Más info: https://www.argentina.gob.ar/servicio/tramitar-un-nuevo-ejemplar-de-dni

Fuente: RENAPER / argentina.gob.ar
```

---

### `/tramite auto patente`

```
🚗 Patente Automotor — Provincia de Buenos Aires
   Dato al 3 may 2026

⚠️ La patente es un impuesto PROVINCIAL. Cada provincia tiene sus propias
   fechas y alícuotas. Especificá tu provincia para datos exactos.

Provincia de Buenos Aires (ARBA):
  Desde marzo 2026 el sistema cambió: se paga mensualmente (10 cuotas, mar–dic)
  Alícuota: 1% del valor fiscal para vehículos hasta $14.100.000

  Fecha de vencimiento de cada cuota: consultá en arba.gob.ar
  Cómo pagar: homebanking, Pago Fácil, Rapipago, o arba.gob.ar

CABA (AGIP):
  Sistema de cuotas separado — consultá en agip.gob.ar

🔗 ARBA (PBA): https://www.arba.gov.ar
🔗 AGIP (CABA): https://www.agip.gob.ar
🔗 Padrones de valuación: DNRPA — https://www.dnrpa.gov.ar

Fuente: ARBA / Infobae (feb 2026)
```

---

### `/tramite auto transferencia`

```
🚗 Transferencia de Vehículo
   Dato al 3 may 2026

Dónde: Registro Seccional del Automotor
  (del domicilio del comprador o donde está radicado el vehículo)

Documentación básica:
  [ ] Formulario 08 (vendedor lo firma ante escribano o en el Registro)
  [ ] Título del automotor
  [ ] DNI de comprador y vendedor
  [ ] VTV vigente (requerido en la mayoría de provincias)
  [ ] Libre deuda de infracciones y patentes
  [ ] CETA — Código de Transferencia de Automotores (se genera en ARCA)

Costo: aranceles del Registro + ITI según valuación fiscal
  (verificar en el Registro Seccional correspondiente)

🔗 DNRPA: https://www.dnrpa.gov.ar
🔗 Generar CETA: https://www.arca.gob.ar/transferencia-de-automotores/
🔗 Guía completa: https://www.argentina.gob.ar/justicia/registro-automotor/transferencia

Fuente: DNRPA / argentina.gob.ar
```

---

### `/tramite pasaporte`

Ejemplo de búsqueda libre:

```
📋 Pasaporte argentino — Renovación
   Dato al 3 may 2026

¿Quién puede tramitarlo?
  Cualquier ciudadano argentino nativo, naturalizado o por opción.

Documentación:
  [ ] DNI vigente
  [ ] Pasaporte anterior (si existe)
  [ ] En caso de menor: autorización del otro progenitor si viaja solo

Costos vigentes (desde marzo 2026):
  Ordinario (~20 días hábiles): $47.000
  Exprés   (~5 días hábiles):   $79.000
  Urgente  (24–48 hs):          $157.000

Dónde tramitarlo:
  • RENAPER (sede central y delegaciones)
  • Consulados argentinos en el exterior

📅 Turno: https://mitramite.renaper.gob.ar
🔗 Tarifario oficial: https://www.argentina.gob.ar/interior/renaper/tarifario-de-tramites-de-renaper

Fuente: RENAPER / argentina.gob.ar
```

---

## Fuentes

- **ANSES:** [anses.gob.ar](https://www.anses.gob.ar) — turnos, prestaciones, montos
- **ARCA/AFIP:** [arca.gob.ar](https://www.arca.gob.ar) — monotributo, facturación, vencimientos
- **DNI / Pasaporte:** [renaper.gob.ar](https://www.argentina.gob.ar/interior/renaper)
- **Registro automotor:** [dnrpa.gov.ar](https://www.dnrpa.gov.ar)
- **Portal unificado:** [argentina.gob.ar](https://www.argentina.gob.ar/tramites)

Los datos son de fuentes públicas y oficiales. Este plugin no almacena ni transmite información del usuario. Montos y requisitos se consultan en tiempo real — nunca hardcodeados.
