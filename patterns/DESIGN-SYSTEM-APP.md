# DESIGN-SYSTEM-APP.md — Contexto de plataforma: App móvil nativa

> Este archivo documenta los tokens, reglas y componentes exclusivos de la **app móvil nativa** de T1 (iOS/Android).
> **No aplica** en dashboard/admin ni en landing pages públicas.
> Para los contextos opuestos, ver [`DASHBOARD.md`](../plataform/DASHBOARD.md) y [`LANDING.md`](../plataform/LANDING.md).

> ⚠️ **Nota de origen:** este documento no viene de un archivo de tokens fuente en Figma — se reconstruyó a partir de los patrones observados y auditados en [`T1APP.md`](../plataform/T1APP.md) (flujos y pantallas). Todo lo marcado 🔴 es un valor **en disputa o sin decidir**, citado con su origen en T1APP.md, y debe confirmarse con Figma/Karla Salazar antes de tratarse como canónico. El objetivo de este archivo es dejar de duplicar fundamentos en cada flujo — no cerrar unilateralmente decisiones de producto.

**Fuente de verdad de contenido:** Figma — `T1-App---ESP` (`viFhO18oodfFqrvyDznrA9`) · **Owner:** Karla Salazar — Head of UX/UI

---

## Diferencias clave vs Dashboard / Landing

| Propiedad | App | Dashboard | Landing |
|---|---|---|---|
| Tipografía | **Inter** (única excepción bajo evaluación: Nova/chat IA) | Manrope | Sora (headings) + Inter (cuerpo) |
| Superficie | Mobile-first, sin breakpoints desktop | Responsive `360px`–`1600px`+ | Responsive `360px`–`1220px` |
| Margen lateral de contenido | `16px` (ancho útil 328px sobre mockup 360) | `160px` desktop | Variable |
| Color primario / CTA | `#DB3B2B` | `#DB3B2B` | `#E26153` |
| Color pressed/active | `#CC0000` | `#CC0000` (hover) | N/A |
| Border radius botón primario | `16px` | `8px` | `18px` |
| Border radius cards | `12px`–`20px` (sin escala cerrada — ver §4) | `10px`–`20px` | `24px` |
| Altura botón primario | `48px` | variable | `45px` |
| Navegación | Stack nativo + bottom sheets + tab bar | Sidebar `284px` | No aplica |
| Sombra "card flotante" | `0 3.66px 21.88px rgba(0,0,0,0.1)` (ver R1) | `0 0 5px 1px rgba(0,0,0,0.1)` | `0 0 25px 2px rgba(0,0,0,0.06)` |

---

## 1. Tipografía

La App usa **Inter** como familia exclusiva.

### Regla R3 — Inter exclusivo

> La App usa **Inter** en todo contexto. **Nova (chat IA)** es la única excepción bajo evaluación — hoy hay Manrope confirmado en el chat y 🔴 **sin decidir** si es intencional (componente compartido) o debe migrarse a Inter (T1APP.md §N.5). **Fuera de Nova, cualquier Manrope en la App es siempre anomalía**, incluso si viene de un componente compartido con Dashboard — auditar el componente en origen, no la pantalla donde aparece. *(Fuente: T1APP.md §CC.23.5, regla R3)*

Se han rastreado **~15 instancias** de Manrope colándose en la App fuera de Nova (paywall de planes, contador de caracteres, tarifas de envío, etiquetas de política, KPIs de incidencias, select "Colonia", date picker, encabezados de bloque de formularios). Todas están pendientes de auditoría en origen — ver §12.

### Escala

| Token | Tamaño | Pesos observados | Uso |
|---|---|---|---|
| T1 | `24px` | SemiBold 600 | Título de paso/pantalla (headers de onboarding y wizards) |
| B1 | `16px` | Regular 400 · Medium 500 · SemiBold 600 | Cuerpo destacado, tarjetas de opción, cabeceras de card |
| B2 | `14px` | Regular 400 · Medium 500 · SemiBold 600 | Cuerpo estándar, labels, texto de botón, inputs |
| B3 | `12px` | Regular 400 · Medium 500 · SemiBold 600 · (Bold 700, uso raro) | Captions, helper text, metadata, chips |

> 🔴 **Gap de escala:** solo `T1` (24px) tiene notación consistente para títulos grandes. Tamaños de 18–22px aparecen en varias pantallas para subtítulos/headers de sección sin un token formal (¿T2/T3?). Falta cerrar esa capa con Figma antes de tratarla como escala completa.

### Pesos válidos

| Peso | Uso |
|---|---|
| Regular 400 | Cuerpo de texto, valores en inputs, descripciones |
| Medium 500 | Labels, metadata secundaria, valores destacados |
| SemiBold 600 | Títulos de card, CTA, encabezados de paso |
| Bold 700 | Uso puntual — confirmar necesidad antes de formalizar como token de peso estándar |

### Color de texto

| Rol | Hex | Uso |
|---|---|---|
| Primary (black-oxford) | `#4C4C4C` | Texto secundario, subtítulos, metadata |
| Texto principal | `#000000` / negro | Valores, títulos de card, labels destacados |
| Disabled | `#9CA3AF` | Texto deshabilitado (botón primario disabled) |
| Inverse | `#FFFFFF` | Texto sobre el botón primario y fondos oscuros |
| Placeholder / gris chip | `#A3A3A3` / `#C3C3C3` | Placeholders de input, texto no seleccionado |
| Accento IA (Nova) | `#7C3AED` | Links y acentos de funciones de inteligencia artificial |

> 🔴 **Anomalía documentada:** el paywall de planes (componente compartido con Dashboard, T1APP.md §10.3) usa `#101928` / `#485162` en vez de la paleta de texto de la App — refuerza que es un componente sin auditar en origen (ver §12).

### Anti-patrones tipográficos

- ❌ Manrope en cualquier pantalla de la App fuera de Nova (ver R3)
- ❌ Tratar un valor con decimales (`11.75px`, `12.824px`, `18.321px`) como si fuera un token — son *escalado horneado* de una instancia con transform; redondear al token de origen antes de documentar (**R1**)
- ❌ Ancho fijo en cualquier nodo que contenga texto variable — usar `width: 100%` + padding del contenedor (**R2**)

---

## 2. Layout y superficie

La App es **mobile-first nativa**; no tiene breakpoints de escritorio como Dashboard o Landing.

| Propiedad | Valor |
|---|---|
| Mockup base | `360×780` |
| Status bar (iPhone) | `50px` arriba |
| Home indicator | Safe area inferior |
| Margen lateral de contenido | `16px` (ancho útil `328px`) |
| Área táctil mínima | `44px` |
| Tarjeta de opción (altura) | `64px` |
| Botón (altura) | `48px` |
| Contenedor de ícono | `40×40` |

**Navegación:** stack nativo con transición horizontal entre pasos; el back conserva las selecciones del usuario. Formularios largos usan **bottom sheets**; confirmaciones y selección usan **modales**; el teclado nativo reacomoda contenido y botón al aparecer.

---

## 3. Botones

| Propiedad | Primario | Secundario / outline |
|---|---|---|
| Background | `#DB3B2B` | `#FFFFFF` / `#F8F8F8` |
| Texto | `#FFFFFF`, Inter SemiBold (B2 S) | `#4C4C4C` / negro, Inter SemiBold (B2 S) |
| Border | ninguno | `1px solid #F3F3F3` |
| Border radius | `16px` | `16px` (🔴 algunas instancias usan `12px` — ver §12) |
| Altura | `48px` | variable (~`51px` en botones sociales) |
| Pressed / active | `#CC0000` | `#F2F2F2` |
| Disabled | bg `#F3F3F3`, texto `#9CA3AF` | border `#E5E5E5`, texto `#A3A3A3` |

### Variantes adicionales

| Variante | Descripción | Uso |
|---|---|---|
| Social | Login con proveedor (Google, etc.), icono + label | Autenticación |
| Link / texto | Sin fondo/borde, texto `#7C3AED` con ícono `ai-magic` | Acciones de IA (Nova, sugerencias) |
| Split / desglose | Selector con chevron (p. ej. rango de fechas) | Filtros, selección secundaria |

---

## 4. Border radius

> 🔴 **No hay una escala cerrada todavía** (a diferencia de Dashboard). Esta es la distribución observada en T1APP.md — se presenta como diagnóstico, no como sistema cerrado. Consolidarla es uno de los pendientes de mayor apalancamiento (T1APP.md §CC.23.8, fase 2).

| Radio | Frecuencia observada | Uso típico |
|---|---|---|
| `4px` | Baja | Badges |
| `6px` | Media | Chips de estado/motivo |
| `8px` | Media-alta | Botones internos de popups/modales, controles compactos |
| `10px`–`13px` | Alta | Cards secundarias, contenedores de ícono, logos de carrier |
| `12px` | **La más frecuente** | Cards, popups, contenedores generales |
| `16px` | Alta | Tarjetas de opción, botón primario |
| `20px` | Alta | Inputs, textareas |

Un mismo popup se documentó con **tres radios distintos simultáneos** (`r20` en el input, `r8` en los botones internos, `r12` en "Cancelar") — T1APP.md §CC.14.4/§6415, evidencia directa de que falta esta escala.

---

## 5. Sombras

> 🔴 Sin escala cerrada. Los dos valores documentados con más evidencia:

| Nombre propuesto | Valor CSS | Uso | Nota |
|---|---|---|---|
| Shadow Card (flotante) | `0 3.66px 21.88px rgba(0,0,0,0.1)` | Cards flotantes sobre contenido | Decimales no redondos — aplicar **R1** y confirmar el valor de origen antes de fijarlo como token |
| Shadow Error/Toast | `0px 4px 6.75px rgba(255,0,0,0.05)` | Alertas/toast de error | Único caso documentado — confirmar si es un patrón reusable |

> ❌ **No reusar `shadow_card` de Dashboard** (`0 0 5px 1px rgba(0,0,0,0.1)`) en componentes de la App sin adaptarlo — se detectó al menos una card de la App usando ese token literal (T1APP.md §CC.22.2), señal de componente Dashboard sin auditar en origen.

**Overlay (modales / bottom sheets):** `rgba(0,0,0,0.4)` es el valor dominante (7 instancias documentadas). 🔴 Hay variantes sueltas en `0.2` y `0.7` sin justificación — consolidar en `0.4` salvo caso documentado en contra.

---

## 6. Colores semánticos

| Rol | Hex | Uso | Estado |
|---|---|---|---|
| Primario / CTA | `#DB3B2B` | Botón primario, borde de selección | ✅ Estable |
| Pressed / activo | `#CC0000` | Estado pressed del primario, stepper activo | ✅ Estable |
| Fondo de selección (Primary/100) | `#FFF0EF` | Tarjeta de opción seleccionada | ✅ Estable |
| Éxito | `#4FC153` **o** `#51AF70` | Confirmaciones, deltas positivos | 🔴 **Dos verdes compitiendo** por el mismo rol — sin token oficial (T1APP.md §H.5·7) |
| Error (input) | `#CC0000` / `#DB3B2B` / `#DB362B` | Borde de input inválido, mensajes de error | 🔴 **Tres rojos compitiendo** ("drift del token de error") — unificar en uno solo (T1APP.md §PC.7.3, §CC.23.4) |
| IA / Nova (fuerte) | `#7C3AED` (documentado también como `Purple/300`) | Acentos y CTA de funciones de IA | 🔴 Nomenclatura invertida — ver nota abajo |
| IA / Nova (fondo claro) | `#F5EFFF` (documentado también como `Purple/500`) | Fondo de chip/card IA | 🔴 Nomenclatura invertida |
| Advertencia (fuerte) | `#FF6700` (documentado también como `Orange/300`) | Chips de motivo/estado logístico | 🔴 Nomenclatura invertida |
| Advertencia (fondo claro) | `#FFF5F0` (documentado también como `Orange/500`) | Fondo de chip de advertencia | 🔴 Nomenclatura invertida |
| Disabled texto | `#9CA3AF` | Texto en botón/campo deshabilitado | ✅ Estable |
| Disabled / borde default | `#F3F3F3` | Borde de input, fondo deshabilitado, tarjeta default | ✅ Estable |

### Regla R6 — Escala de color

> En toda familia de color, **número mayor = tono más oscuro** (`Primary/600` oscuro, `Primary/100` claro). **Orange y Purple están invertidos** hoy: el sufijo "300" es el tono fuerte y "500" es el fondo claro, al revés de la convención. *(Fuente: T1APP.md §CC.23.5, regla R6 · decisión pendiente D10)*

---

## 7. Inputs y formularios

| Elemento | Valor |
|---|---|
| Border radius | `20px` |
| Border default | `#F3F3F3` |
| Padding | `16px`–`18px` |
| Altura input | `55px` |
| Altura textarea | `~181px` |
| Texto | Inter Regular, `13px`–`14px` (B2 R) |
| Label | Inter SemiBold, `14px` (B2 S) |

### Estado de error

Borde rojo + mensaje bajo el campo ("Este campo es obligatorio" / "Campo obligatorio" / mensaje específico de validación). 🔴 **El color exacto del borde/mensaje no está unificado** — ver "Error (input)" en §6. Documentar el estado visual completo (no solo el mensaje) es un pendiente explícito (T1APP.md §EN.9.14, §EN.12.4).

---

## 8. Tarjetas y componentes de selección

### Tarjeta de opción seleccionable

| Propiedad | Default | Seleccionada |
|---|---|---|
| Fondo | `#FFFFFF` | `#FFF0EF` |
| Borde | `1px #F3F3F3` | `1px #DB3B2B` |
| Radio | `16px` | `16px` |
| Altura | `64px` | `64px` |
| Indicador | — | ícono check, `20px`, derecha |

Estructura interna: contenedor de ícono `40×40`, fondo `#F8F8F8`, radio `12px` + `gap 12px` + label B2 SemiBold negro + línea secundaria opcional B3 Medium `#4C4C4C`.

### Selección única (radio)

Control circular `16×16` a la izquierda + texto de una o dos líneas. Una sola opción activa a la vez.

---

## 9. Chips y badges

| Elemento | Radio | Fondo / Texto | Uso |
|---|---|---|---|
| Chip de sugerencia (IA) | `11px` | `#F5EFFF` / `#7C3AED` SemiBold 12 | Sugerencias generadas por IA |
| Chip de sugerencia (normal) | `11px` | `#F8F8F8` / negro Regular 12 | Sugerencias sin IA |
| Chip de estado/motivo | `6px` | Fondo claro semántico / texto fuerte semántico (ver §6) | Estado de pedido, motivo de incidencia |
| Badge | `4px` | Según rol semántico | Etiquetas cortas |

> 🔴 **Un mismo chip (naranja) se usa con dos significados distintos** en incidencias — motivo de la incidencia en un flujo, estado logístico del envío en otro (T1APP.md §CC.22.2). Evaluar si necesitan diferenciarse visualmente.

---

## 10. Modales y bottom sheets

| Elemento | Patrón |
|---|---|
| Overlay | `rgba(0,0,0,0.4)` (ver §5) |
| Bottom sheet | Header (título + cerrar `cancel-01`) + contenido + botón de acción fijo; sube junto al teclado nativo en captura de texto |
| Modal de confirmación | Ícono semántico de la acción (no heredado de otro flujo — **R8**) + mensaje + CTA afirmativo que nombra la acción (**R5**) |

### Regla R4 — Criterio de confirmación

> Acciones **reversibles** guardan directo, sin modal. Acciones **irreversibles o de plazo largo** requieren confirmación. *(Fuente: T1APP.md §CC.23.5, regla R4)*

### Regla R5 — CTA afirmativo

> El botón afirmativo **nombra la acción**: "Sí, devolver", "Sí, reprogramar", "Sí, reintentar". `"Sí, confirmar"` queda reservado a confirmaciones sin verbo propio. *(Fuente: T1APP.md §CC.23.5, regla R5)*

### Regla R8 — Ícono semántico

> El ícono del modal de confirmación debe corresponder a la acción, no heredarse de otro flujo. *(Fuente: T1APP.md §CC.23.5, regla R8)*

---

## 11. Reglas de sistema (R1–R8)

Consolidado desde T1APP.md §CC.23.5 — resuelven familias completas de hallazgos y previenen su reaparición. Se citan aquí como fuente única; no duplicar en los flujos.

| Regla | Enunciado |
|---|---|
| **R1 — Valores no redondos** | Todo valor con decimales no intencionales es escalado horneado de una instancia con transform, nunca un token. Redondear al token de origen al documentar. |
| **R2 — Prohibido el ancho absoluto en contenido de texto** | Ningún nodo con texto variable lleva ancho fijo. Usar `width: 100%` + padding del contenedor. |
| **R3 — Inter exclusivo** | Ver §1. |
| **R4 — Criterio de confirmación** | Ver §10. |
| **R5 — CTA afirmativo** | Ver §10. |
| **R6 — Escala de color** | Ver §6. |
| **R7 — Un mensaje por condición** | Una condición de validación tiene un solo mensaje, independientemente del tipo de control. |
| **R8 — Ícono semántico** | Ver §10. |

---

## 12. Anti-patrones de la App

| Anti-patrón | Corrección |
|---|---|
| Manrope en cualquier pantalla fuera de Nova | Auditar el **componente en origen** (paywall, KPIs, selects, date picker), no la pantalla — es probable reúso de Dashboard sin adaptar (R3) |
| Reusar sombras/tokens literales de Dashboard (`shadow_card` de Dashboard) | La App tiene su propia sombra flotante (§5) — no importar tokens de Dashboard sin adaptarlos |
| Tres rojos de error compitiendo (`#CC0000`/`#DB3B2B`/`#DB362B`) | Definir un único token de error antes de nuevas implementaciones |
| Dos verdes de éxito compitiendo (`#4FC153`/`#51AF70`) | Definir un único token de éxito |
| Orange/Purple con numeración invertida | Corregir para que número mayor = más oscuro (R6) |
| Radios mezclados sin escala (r6/r8/r10/r12/r13/r16/r20 sin regla de uso) | Consolidar en la escala de §4 antes de agregar componentes nuevos |
| Ancho fijo en texto variable | Usar `width: 100%` + padding (R2) |
| Valor con decimales tratado como token (`11.75px`, `12.824px`) | Redondear al token de origen (R1) |
| CTA destructivo con el mismo color que el primario | Definir variante *danger* distinta del rojo primario (T1APP.md §D.9·1) |

---

## 13. Checklist de QA — Pre-deployment

**Tipografía**
- [ ] Toda la interfaz usa Inter (Manrope solo si Nova lo confirma como excepción — hoy pendiente)
- [ ] Pesos solo: Regular 400, Medium 500, SemiBold 600
- [ ] Ningún valor de tamaño con decimales sin redondear a un token (R1)

**Colores**
- [ ] Botón primario: `#DB3B2B`, pressed `#CC0000`
- [ ] Un solo token de error usado en todos los inputs (pendiente de decidir cuál — §6)
- [ ] Un solo token de éxito usado en todos los deltas positivos (pendiente de decidir cuál — §6)
- [ ] Orange/Purple no se usan como si "500" fuera más oscuro que "300" hasta que se corrija la numeración (R6)

**Layout**
- [ ] Margen lateral `16px` respetado
- [ ] Touch targets mínimo `44px`
- [ ] Ningún nodo de texto variable con ancho fijo (R2)

**Componentes**
- [ ] Border radius documentado explícitamente por componente (no asumir — §4 no es escala cerrada todavía)
- [ ] Overlay de modal/sheet: `rgba(0,0,0,0.4)` salvo excepción documentada
- [ ] Ícono del modal de confirmación corresponde a la acción (R8)
- [ ] CTA afirmativo nombra la acción (R5)
- [ ] Acciones irreversibles llevan confirmación; reversibles no (R4)

**Antes de dar por cerrado un componente compartido con Dashboard**
- [ ] Confirmado con Figma si es realmente el mismo componente o una reconstrucción
- [ ] Auditado en origen (no parchado pantalla por pantalla)
- [ ] Documentado aquí si se decide que es intencionalmente compartido

---

## Referencias

- [`T1APP.md`](../plataform/T1APP.md) — flujos y pantallas de la App; fuente de los patrones consolidados aquí
- [`DASHBOARD.md`](../plataform/DASHBOARD.md) — contexto opuesto: admin/backoffice (Manrope)
- [`LANDING.md`](../plataform/LANDING.md) — contexto opuesto: landing pages públicas (Sora + Inter)
- T1APP.md §CC.23 — consolidado de hallazgos y reglas R1–R8 (fuente principal de este documento)
