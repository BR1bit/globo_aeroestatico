# Material para publicar en Fab

Todo listo para copiar y pegar. Los campos marcados **[tuyo]** los tenés que
completar vos (cuenta, contrato, datos fiscales, precio).

---

## 1. Título

```
Hot Air Balloon — Real Scale 1:1 for VR (PBR, Game Ready)
```

Alternativas si querés probar otra:

```
Realistic Hot Air Balloon — 1:1 Scale, VR Ready, PBR
Hot Air Balloon with Detailed Basket, Burner and Gas Tanks — Real Scale
```

## 2. Descripción corta

```
Photorealistic hot air balloon at true 1:1 scale, built for VR. Enterable basket,
detailed burner and gas tanks. 33,750 tris, PBR, GLB/FBX/OBJ/BLEND.
```

---

## 3. Descripción completa (inglés — la que va en el listado)

```markdown
A complete hot air balloon modelled at **true 1:1 real-world scale in metres**,
built specifically so a person can stand inside the basket in VR.

The basket floor sits exactly at **y = 0**, so an XR Origin drops straight in with
no offset, and the 1.08 m walls land at chest height on an adult.

## Measurements

| | |
|---|---|
| Envelope | 18.00 m diameter x 21.39 m tall |
| Total height | 25.31 m |
| Walkable basket floor | 1.60 x 1.79 m |
| Basket wall above floor | 1.08 m |
| Gas tanks | 31 cm diameter x 62 cm |

Comfortable for one person with both tanks aboard, or two to three people.

## What's modelled

- **Envelope** — 20-gore teardrop with load tapes, a crown ring and a crown vent
- **Rigging** — 20 complete load chains: webbing patch stitched to the fabric with
  a box-and-cross pattern, webbing tab, steel ring and load cable
- **Burner** — twin heat-tempered coils, nozzles, gimbal frame and four shackles
- **Basket** — woven wicker, plank floor, leather rim and base trim, corner
  guards, four leather-padded uprights, skid runners with straps, reinforced
  step holes
- **Gas tanks** — two brushed aluminium cylinders with brass valves, handwheels,
  retaining straps and braided hoses running to the burner

## Technical

- **161 objects · 33,750 triangles · 34,086 vertices · 19 materials**
- Zero n-gons, zero hidden geometry, scale applied, rotation zeroed
- Single root node with five named groups: Envelope, Rigging, Burner, Basket, Tanks
- Every object and its mesh share the same descriptive name — no `Cylinder.003`
- PBR metallic-roughness, 28 PNG maps (2048² down to 512² on the tileables)
- Y-up, metres, in all formats

## Formats

| File | Notes |
|---|---|
| `.glb` | Textures embedded — drop straight into Unity, Unreal or the web |
| `.fbx` | For Maya, 3ds Max, Cinema 4D |
| `.obj` + `.mtl` | Generic interchange |
| `.blend` | Blender 5.2 source with the full node materials |

FBX and OBJ reference the `textures` folder next to them, so keep the folder
structure as shipped.

## Notes before you import

- The envelope material must be **double sided** — from inside the basket a
  single-sided setting shows the sky through the fabric. The GLB already ships
  `doubleSided: true`.
- The envelope panels carry a low **emissive** value (22%), which is what makes
  them glow from the inside the way a real balloon does under sunlight.
- The **ripstop weave ships as a separate tileable detail map**, not baked into
  the envelope texture. glTF allows one normal map per material, and the weave
  needs hundreds of repeats. Apply `tela_ripstop_normal` and
  `tela_ripstop_detail_albedo` in the Detail Inputs at a tiling of **226 x 110**.
- The flame is a simple emissive mesh meant to be read with Bloom on.

A full README with a step-by-step Unity import checklist is included.
```

---

## 4. Descripción completa (español, por si el listado lo admite)

```markdown
Globo aerostático completo modelado a **escala real 1:1 en metros**, pensado para
que una persona esté parada dentro de la canasta en VR.

El piso de la canasta está exactamente en **y = 0**: el XR Origin entra directo,
sin offset, y la pared de 1,08 m queda a la altura del pecho de un adulto.

Medidas: globo de 18,00 m de diámetro por 21,39 m de alto, 25,31 m de altura
total, piso pisable de 1,60 × 1,79 m, tanques de 31 cm × 62 cm.

161 objetos · 33.750 triángulos · 34.086 vértices · 19 materiales · 28 texturas
PBR. Cero n-gons, escala aplicada, jerarquía con un único nodo raíz y cinco
grupos nombrados. Se entrega en GLB, FBX, OBJ y BLEND, con un README con la
checklist de importación a Unity.
```

---

## 5. Tags

```
hot air balloon, balloon, vr, virtual reality, real scale, pbr, game ready,
aircraft, aviation, basket, burner, wicker, gas tank, flight, sky, vehicle,
quest, unity, unreal, low poly, exterior, transport
```

Fab suele limitar la cantidad. Si hay que recortar, priorizá estos ocho:
`hot air balloon`, `vr`, `pbr`, `game ready`, `real scale`, `aviation`,
`vehicle`, `balloon`.

---

## 6. Imágenes de la galería

En `preview/`, en este orden. La **01 es la miniatura** y es la que decide si
alguien entra al listado.

| # | Archivo | Qué muestra |
|---|---|---|
| 1 | `01_hero.png` | Conjunto completo, 3/4, fondo de estudio |
| 2 | `09_medidas.png` | Medidas reales acotadas + detalle de la canasta |
| 3 | `06_interior.png` | Vista desde adentro mirando arriba — el argumento VR |
| 4 | `03_canasta.png` | Canasta, montantes y quemador |
| 5 | `05_tanques.png` | Interior con los tanques montados |
| 6 | `04_quemador.png` | Quemador en detalle |
| 7 | `08_uniones.png` | Cadena de anclaje parche → cincha → anillo → cable |
| 8 | `07_tela.png` | Gajos, costuras y arrugas de la tela |
| 9 | `11_wireframe.png` | Topología |
| 10 | `10_texturas.png` | Los mapas incluidos |
| 11 | `02_perfil.png` | Perfil completo |

Todas en 1920×1080 salvo `09_medidas.png`, que es 1920×1440.

---

## 7. Campos que completás vos

- **[tuyo]** Cuenta de vendedor de Fab (cuenta Epic + contrato de distribución)
- **[tuyo]** Formulario fiscal — si estás en Uruguay es el W-8BEN
- **[tuyo]** Datos de cobro
- **[tuyo]** Precio
- **[tuyo]** Licencia: Fab ofrece *Personal* y *Professional*. Para un asset así
  lo habitual es publicar la *Professional*, que permite uso comercial.

### Sobre el precio

No te puedo dar una recomendación de negocio con fundamento, porque no conozco el
mercado actual de Fab ni cómo está saliendo lo comparable. Lo que sí conviene:
antes de fijarlo, buscá en Fab "hot air balloon" y mirá qué piden los modelos con
un conteo de polígonos y un nivel de detalle parecidos. Es un dato de cinco
minutos y vale más que cualquier número que yo tire de memoria.

---

## 8. Archivo a subir

`globo_aerostatico_v1.zip` — contiene los cuatro formatos, la carpeta `texturas/`
y el README. No incluye los renders: esos van por separado, en la galería.
