# Globo aerostático — modelo para VR (Meta Quest 3)

Modelo a escala real 1:1 en metros, pensado para que una persona esté parada dentro
de la canasta. Construido procedimentalmente en Blender 5.2.

---

## 1. Medidas

| Elemento | Medida |
|---|---|
| Globo (envoltorio) | 18,00 m diámetro × 21,39 m alto |
| Altura total del conjunto | 25,31 m |
| Canasta — tejido de cuerda | 1,75 × 1,95 m |
| Canasta — borde de cuero (máximo) | 1,90 × 2,10 m |
| **Piso pisable** | **1,60 × 1,79 m** |
| Altura de pared sobre el piso | **1,082 m** (altura de pecho de un adulto) |
| **Piso pisable** | **y = 0** |
| Punto más bajo (patines) | y = −0,07 |
| Tanques de gas | 31 cm diámetro × 62 cm |

> El piso está exactamente en **y = 0**. El XR Origin va ahí directo, sin offset.

Capacidad real: 1 persona cómoda con los dos tanques, o 2–3 personas.

**Presupuesto:** 161 objetos · **33.750 triángulos** · 34.086 vértices · 19 materiales
· 32 texturas

Todo malla poligonal: **cero n-gons**, cero geometría oculta, cero objetos vacíos de
relleno. El modelo está en el origen, con escala 1,0 aplicada y rotación en cero.

---

## 2. Formatos incluidos

| Archivo | Tamaño | Para qué |
|---|---|---|
| `globo_aerostatico.glb` | 21 MB | **Unity / Unreal / web.** Texturas embebidas, PBR completo, listo para importar |
| `globo_aerostatico.fbx` | 2,5 MB | Maya, 3ds Max, Cinema 4D. Texturas por ruta relativa a `texturas/` |
| `globo_aerostatico.obj` + `.mtl` | 2,9 MB | Intercambio genérico. Texturas por ruta relativa a `texturas/` |
| `globo_aerostatico.blend` | 440 KB | Fuente editable (Blender 5.2), con los materiales nodales completos |

Los tres exports salen de la misma escena y coinciden objeto por objeto: 161 mallas,
33.750 triángulos. FBX y OBJ **no duplican** las texturas — las referencian en
`texturas/`, así que esa carpeta tiene que viajar al lado del modelo.

Orientación: **Y arriba, −Z al frente**, unidades en metros, en los tres formatos.

---

## 3. Nomenclatura y jerarquía

Todo cuelga de un único empty raíz, agrupado por subsistema:

```
HotAirBalloon_Root
├── GRP_Envelope   (3)   Envelope_Fabric, Envelope_CrownRing, Envelope_CrownValve
├── GRP_Rigging   (80)   Rigging_TapePatch_01..20, Rigging_TapeStrap_01..20,
│                        Rigging_Ring_01..20, Rigging_Cable_01..20
├── GRP_Burner    (16)   Burner_Coil_L/R, Burner_Nozzle_L/R, Burner_FrameSide_01..04,
│                        Burner_FrameDiag_01..02, Burner_GimbalRing,
│                        Burner_Shackle_01..04, Burner_Flame
├── GRP_Basket    (40)   Basket_Weave, Basket_Floor, Basket_RimTop, Basket_TrimBase,
│                        Basket_CornerGuard_01..04, Basket_Upright_01..04,
│                        Basket_UprightPad_01..04, Basket_PadBand_01..08,
│                        Basket_Runner_01..02, Basket_RunnerStrap_01..06,
│                        Basket_StepHole_01..08
└── GRP_Tanks     (22)   Tank_Body_L/R, Tank_Foot, Tank_Collar, Tank_Valve, Tank_Outlet,
                         Tank_Handwheel, Tank_HandwheelHub, Tank_Strap, Tank_Hose,
                         Tank_HoseFitting_*_A/B
```

El nombre del objeto y el de su malla son **idénticos** — en Unity cada mesh asset
entra con su nombre real, no como `Cylinder.003`.

Materiales, todos con prefijo `M_`:

```
M_Envelope_Fabric      M_Envelope_Crown       M_Basket_RopeWeave   M_Basket_Floor
M_Basket_StepHole      M_Leather_RimTop       M_Leather_RimBase    M_Leather_CornerGuard
M_Leather_UprightPad   M_Leather_Plain        M_Metal_Stainless    M_Metal_HeatTempered
M_Metal_Brass          M_Metal_Aluminium      M_Hose_Braid         M_Webbing_Strap
M_Rope                 M_Valve_Red            M_Flame
```

---

## 4. Checklist de importación a Unity

```
[ ] 1. Package Manager -> Add package by name -> com.unity.cloud.gltfast
[ ] 2. Arrastrar globo_aerostatico.glb a Assets/
[ ] 3. Scale factor 1, sin rotación  (ya viene Y-up y en metros)
[ ] 4. XR Origin en y = 0            (el piso de la canasta está ahí)
[ ] 5. M_Envelope_Fabric -> Render Face: Both
[ ] 6. Emisivo activado en M_Envelope_Fabric y M_Flame
[ ] 7. Detail Normal + Detail Albedo en M_Envelope_Fabric, tiling 226 x 110  (ver 6.4)
[ ] 8. Compresión de texturas ASTC 6x6
[ ] 9. Stereo Rendering: Single Pass Instanced
[ ] 10. Box Colliders en piso y paredes (no Mesh Collider)
```

---

## 5. Archivos

```
globo_aerostatico/
├── globo_aerostatico.glb      ← Unity / Unreal / web (texturas embebidas)
├── globo_aerostatico.fbx      ← Maya / 3ds Max / C4D
├── globo_aerostatico.obj      ← intercambio genérico
├── globo_aerostatico.mtl         (acompaña al .obj)
├── globo_aerostatico.blend    ← fuente editable
├── texturas/                  ← los 32 PNG sueltos (los usan el .fbx y el .obj)
├── preview/                   ← imágenes de galería para las tiendas
└── renders/                   ← 9 ángulos del modelo actual
```

Las rutas de textura del `.blend` son **relativas** (`//texturas/...`), así que la
carpeta tiene que viajar al lado. Si quedaran absolutas, al abrirlo en otra
máquina faltarían las 26 imágenes.

### Texturas

| Archivo | Resolución | Uso |
|---|---|---|
| `globo_basecolor` / `globo_normal` | 2048² | Tela del globo |
| `cuerda_basecolor` / `_normal` / `_roughness` | 1024² | Tejido de cuerda de la canasta (mosaico, tile de 0,75 m) |
| `piso_basecolor` / `_normal` / `_roughness` | 1024² | Piso de tablones de la canasta |
| `borde_basecolor` / `borde_normal` | 4096×512 | Borde de cuero (tira) |
| `cuero_basecolor` / `_normal` / `_roughness` | 1024² | Cuero en mosaico: montantes, cinchas y bandas |
| `zocalo_basecolor` / `zocalo_normal` | 2048×256 | Zócalo de cuero (tira) |
| `tanque_basecolor` / `_roughness` / `_normal` | 1024² | Aluminio cepillado |
| `tela_ripstop_normal` / `_detail_albedo` | 1024² | **Trama de la tela — va aparte, ver 6.4** |
| `tela_ripstop_height` | 1024² | Fuente del anterior (solo para Blender) |
| `metal_inox_*` | 512² | Acero cepillado: marco, aro, grilletes |
| `metal_calor_*` | 512² | Revenido: serpentinas y picos del quemador |
| `metal_laton_*` | 512² | Latón: válvulas, salidas, racores |
| `manguera_trenza_color` / `_normal` | 512² | Trenza negra de las mangueras |
| `cincha_refuerzo_*` | 256×512 | Parche y cincha de anclaje de los cables |

`piso_basecolor`, `cuero_basecolor` y `cuerda_basecolor` son imágenes **generadas con
IA** provistas por el autor; sus normal y roughness se derivan de ellas, igual que el cuero de las tiras
`borde_*` y `zocalo_*`, que conservan su costura original. El original queda en `fuentes/`, fuera
del paquete que se distribuye. El resto de las texturas son procedurales.

Las de cuero son **tiras, no cuadradas**: el borde mide 6,7 × 0,5 m, una textura
cuadrada desperdiciaría la mayor parte del espacio.

Las del quemador y la cincha son **en mosaico** (tileables), aplicadas con un nodo
Mapping. No están bakeadas por objeto: son piezas chicas y repetir una textura
genérica rinde mucho más que hacerle un atlas a cada tubo.

---

## 6. Los cuatro puntos críticos

### 6.1 La tela tiene que ser doble cara

`Render Face: Both` en el material `M_Envelope_Fabric`.

Si queda en `Front`, **desde adentro de la canasta vas a ver el cielo a través del
globo**. El GLB ya trae `doubleSided: true`, pero conviene confirmarlo en Unity.

### 6.2 Emisivo activado

- **Tela del globo**: emisivo al 22% del color del panel. Es lo que hace que los
  paneles se vean luminosos desde adentro, como en un globo real (el sol atraviesa
  el nylon). Desde afuera a pleno sol es imperceptible.
- **Llama**: usa `KHR_materials_emissive_strength` con valor 26. Con Bloom activado
  queda bien; sin Bloom se ve plana.

### 6.3 Color space

Proyecto en **Linear** (es el default en URP). Coincide con Blender.

### 6.4 La trama de la tela va como Detail Map (no viene en el GLB)

El `globo_normal` del GLB trae el relieve **macro**: el abombado entre gajos, los
pliegues y las costuras. La **trama del ripstop no puede viajar en el GLB** — glTF
admite un solo normal map por material y la trama necesita repetirse cientos de
veces.

Se aplica a mano en el material `M_Envelope_Fabric`, en **Detail Inputs**:

| Slot | Archivo | Tiling |
|---|---|---|
| Detail Normal Map | `tela_ripstop_normal.png` | **226 × 110** |
| Detail Albedo | `tela_ripstop_detail_albedo.png` | **226 × 110** |

Ese tiling no es arbitrario: el parche representa 25 cm de tela, y el globo mide
56,55 m de circunferencia por 27,58 m de arco → 226 y 110 repeticiones.
Si cambiás el tamaño del globo, recalculá con esa división.

El detail albedo es gris 0,5 neutro con la grilla apenas más clara, así que en modo
overlay solo aporta los hilos sin alterar el color del panel.

**Por qué no está bakeada:** a 2048² cada texel cubre 1,4 × 2,8 cm y los hilos miden
0,4 mm. Bakearla no la mostraría, solo produciría moiré.

---

## 7. Cómo está armada la unión de los cables

La cadena completa, de arriba hacia abajo:

1. **Cinta de carga** pintada en la textura de la tela, sobre cada una de las 20
   costuras de gajo
2. **Parche de cincha** (`Rigging_TapePatch_*`) cosido a la tela con pespunte en
   **caja con cruz** — el patrón estándar para cinchas que cargan peso
3. **Cincha** (`Rigging_TapeStrap_*`) que baja 26 cm de la boca
4. **Anillo de acero** (`Rigging_Ring_*`) en su extremo
5. **Cable** (`Rigging_Cable_*`) del anillo al marco del quemador

Son **20 cables, uno por gajo**, alineados con las costuras. Si cambiás el número de
gajos en la textura, hay que cambiar este número también o dejan de coincidir.

---

## 8. Si vas a editar el .blend

Hay **dos capas de trabajo** sobre las texturas del globo y es fácil pisarlas:

1. Lo que genera el **shader procedural** (paleta, costuras, abombado)
2. Lo que se **compone con numpy** encima (arrugas, tono de los pliegues, pespunte)

**Rebakear borra la capa 2.** Si tocás el shader, después hay que recomponer.
Los composites son determinísticos (semillas fijas), así que se recalculan idénticos
y hasta se pueden **restar** para bajar la intensidad sin rebakear — es lo que se
hizo para ajustar el arrugado.

### Ciclo completo de un rebake

1. Motor **Cycles**, `samples = 1`, margin 8–16
2. Bake `DIFFUSE` con *Direct* e *Indirect* apagados y *Color* prendido
3. Bake `NORMAL` (y `ROUGHNESS` en el caso del tanque)
4. **Reconstruir el material apuntando a las imágenes** ← se olvida fácil
5. Recomponer las capas de numpy
6. Volver a **EEVEE** y reexportar

### Capas UV

| Objeto | Capas | Notas |
|---|---|---|
| `Envelope_Fabric` | `UVMap` | u = ángulo, v = **longitud de arco** (sin estiramiento en los polos) |
| `Basket_Weave` | `UVMap` (metros) | El tejido se repite por metro real: un nodo Mapping con escala 1/0,75 |
| `Basket_RimTop`, `Basket_TrimBase` | `UVMap` (metros) + `UVNorm` (0–1) | Igual criterio |
| `Basket_CornerGuard_*`, `Basket_UprightPad_*` | `UVMap` | Mapeadas dentro de la textura del borde |
| `Basket_Floor` | `UVMap` | Proyección planar XY, 1:1 con el contorno del piso |
| `Basket_Runner_*` | `UVMap` | Proyección de caja, misma densidad que el piso |
| `Tank_Body_*` | `UVMap` | Cilíndrica |
| `Tank_Hose_*` | `UVMap` | Smart project (se armaron con bmesh, sin UV) |

La capa marcada `active_render` es la que corresponde a la textura. No cambiarla.

---

## 9. Trampas encontradas durante la construcción

Anotadas porque son fáciles de repetir:

- **Bakear el pase difuso sobre un material metálico da negro.** Los metales no
  tienen componente difusa. Hay que bajar `Metallic` a 0 solo durante ese bake y
  restaurarlo después. Pasó con los tanques.

- **Encadenar un Bump después de un Normal Map rompe el export a glTF.** glTF
  admite un solo normal map por material, así que el exportador tomó lo último que
  alimentaba el input Normal (la trama tileada, un height map en escala de grises)
  y **descartó el normal bakeado**. El bakeado tiene que ir **directo al BSDF**.

- **Las primitivas con tapas n-gon no generan tangentes.** Los cilindros y conos
  creados con `bpy.ops.mesh.primitive_*` tienen tapas de n lados, y Blender no puede
  calcular tangentes ahí — el exportador avisa con "Could not calculate tangents" y
  la malla sale **sin TANGENT**, así que su normal map se ve mal en Unity. Se
  resuelve con un modificador **Triangulate** en todo objeto que use normal map.

- **Los objetos Curve rompen FBX y OBJ de formas distintas y silenciosas.** Los 20
  cables y las 2 serpentinas del quemador eran curvas con bevel. El exportador FBX
  las **omitió por completo** (`object_types` sin `'CURVE'`: salieron 139 de 161
  objetos, sin un solo warning) y el de OBJ las escribió **dos veces**, una
  trianguladas y otra con los quads originales. Solo el GLB estaba bien. Se
  arreglaron convirtiéndolas a malla (`object.convert(target='MESH')`), que conserva
  UV, material y padre. **Verificar siempre el conteo de objetos del archivo
  exportado, no el de la escena.**

- **Un normal map no se ve con luz ambiente uniforme.** Con un cielo parejo muy
  brillante, inclinar la normal casi no cambia la luz que recibe la superficie, así
  que los pliegues desaparecen. Si la tela se ve plana, mirá la iluminación antes de
  tocar la textura.

- **Para pliegues usar ruido "ridged" (`1 - |2n-1|`), no ruido común.** El ruido
  normal da manchas suaves que se leen como ondulación; el ridged da crestas
  afiladas, que es lo que parece un pliegue de tela.

- **En las texturas bakeadas la fila 0 es la CORONA, no la boca.** Blender guarda
  las imágenes de abajo hacia arriba y PIL las lee al revés, así que al componer
  algo con numpy sobre un mapa bakeado el eje V queda invertido. Verificar siempre
  con un rasgo conocido (acá, la garganta teal) antes de componer.

- **`matrix_world` está cacheado.** Leer vértices sin aplicarlo da coordenadas
  locales — así quedaron las lengüetas 7 cm flotando. Y después de mover un objeto
  hay que llamar a `view_layer.update()` o se sigue leyendo el valor viejo.

- **El punteado del pespunte aliasa a distancia; usar línea continua.** A 6 m cada
  puntada cae en 2-3 píxeles y el mipmap la promedia inconsistentemente, dejando una
  franja difusa peor que no tener nada.

- **Lo que se ancla a otra geometría conviene leerlo del mesh, no copiarlo.** Los
  cables quedaron colgando en el aire cuando cambió el perfil del globo. Ahora leen
  el radio de la boca directamente del mesh y se reanclan solos.

- **Una textura de valor constante es un desperdicio.** La rugosidad de la trenza
  era un gris plano ocupando 453 KB; va como escalar en el material.

- **`path_mode='COPY'` al exportar duplica todo el set de texturas.** El OBJ dejó 25
  PNG sueltos en la raíz y el FBX otros 25 en un `.fbm/` — 38 MB de copias idénticas
  a `texturas/`. Con `'RELATIVE'` los dos apuntan a la carpeta que ya existe.
