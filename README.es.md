# Tlender

[English](README.md) · [Português](README.pt.md) · **Español**

**Tlender es un programa 3D para modelar, animar y renderizar personajes y escenas**, escrito desde cero en C y Vulkan
para ser rápido. Usa los mismos atajos, menús y conceptos que Blender, así que quien ya usa Blender se siente en casa, y
abre y guarda archivos `.blend`.

**Versión actual: 0.48** (25/11/2026) · Windows 10/11 64 bits · Español, English, Português ·
[Tlender Mobile para Android](https://github.com/NathanLourencoPeixoto/tlender-mobile-releases)

## Qué estás descargando

La [release más reciente](https://github.com/NathanLourencoPeixoto/tlender-releases/releases/latest) tiene tres archivos:

| Archivo | Qué es |
|---|---|
| `Tlender-<versión>-win64.zip` | **El programa.** Extrae la carpeta donde quieras y abre `tlender.exe` (no hay que instalar nada). |
| `Tlender-<versión>-win64.zip.sha256` | El código para comprobar que la descarga llegó completa. |
| `Tlender-<versión>-win64.zip.sig` | La firma que el actualizador de Tlender comprueba antes de instalar una versión nueva. |

Dentro del zip vienen `tlender.exe`, el instalador de actualizaciones (`tlender_updater.exe`), el denoiser (Intel OIDN),
NVIDIA DLSS, el runtime de Visual C++ y un `LEIA-ME.txt` (léeme). No se instala nada en el sistema; las preferencias se
guardan en `%APPDATA%\Tlender`. El idioma de la interfaz se cambia en *Editar > Preferencias > Interfaz > Traducción*.

**Requisitos**: una tarjeta gráfica con Vulkan 1.2. Para renderizar en la GPU hace falta ray tracing por hardware (NVIDIA
RTX, AMD RX 6000 o más nueva, Intel Arc); sin eso el render usa la CPU.

**Aviso de Windows**: el ejecutable todavía no tiene un certificado de firma de código, así que SmartScreen o el
antivirus pueden avisar la primera vez. Haz clic en *Más información → Ejecutar de todas formas*. Cada paquete está
firmado por el autor (el archivo `.sig`), y el actualizador solo instala versiones con esa firma.

## Actualizaciones

Tlender busca una versión nueva al abrirse y descarga **solo los archivos que cambiaron**. La versión nueva se instala
cuando cierras el programa. Marcando *Usar la versión Beta de Tlender* en las Preferencias entras en el **canal Beta** y
recibes antes las versiones de prueba (terminan en `_b`). Todo lo que cambió en cada versión está en las
[releases](https://github.com/NathanLourencoPeixoto/tlender-releases/releases) y en el propio programa (*Ayuda > Notas
de la versión*).

### En la beta 0.49_b (canal Beta)
- **Rotoscopia guiada y más rápida**: pestaña Recortar con cinco pasos, pins que responden en ~0,1 s, vista previa
  del video en un hilo con Cancelar, calidad Rápida/Buena/Máxima y exportación en PNG de 16 bits sin congelar la
  pantalla.

### Novedades de la 0.48 y de Mobile 0.29

- **Recorte inteligente con pines, sin pantalla verde**: círculos en lo que se queda y en lo que sale; SAM 2.1 hace la
  máscara y sigue el objeto, y ViTMatte refina borde y pelo (error en el pelo de 14,9 a 2,5 en una prueba). Sale en PNG de 16 bits o EXR.
- **El recorte en la escena 3D**: se vuelve un plano físico delante de la cámara del tracking, con la luz y las sombras
  del 3D, y las áreas fijadas en la escena (como el suelo) también quedan visibles.
- **Mapas PBR del recorte**: Albedo, Normal, Roughness y Metal y un material listo (MoGe-2 y Marigold en el PC).
- **Tracking como el de RealScan**: rolling shutter y lente completa en el solve, unas 100× más rápido (pasillo 4K de
  81 min a 50 s), modo denso, gráfico del error por fotograma y aviso de trípode.
- **Tomas con ARCore** en Tlender Mobile, enviadas al PC por Wi-Fi con cámara, suelo, malla y luz.

### Novedades de la 0.47

- **Código abierto**: el código de Tlender ahora es público en [tlender-source](https://github.com/Nathan3DAnimator/tlender-source), bajo la GPL-3.0-or-later
  (la misma familia que Blender). El SDK de DLSS se descarga de NVIDIA con un script al compilar.
- **Editor de episodios** empieza sin carpeta elegida (antes apuntaba a una carpeta que solo existía en el ordenador del autor).

### Novedades de la 0.46 y de Mobile 0.28

- **Límites que detienen G, R, S y el manipulador**: con *Afectar transformación* (activada por defecto) el valor de un
  hueso u objeto con Limit se detiene en el límite, y volver responde al instante (antes pasaba y había que arrastrarlo todo de vuelta).
- **Huesos seleccionados bien visibles**: alambres más gruesos (también en las formas de control) y color más claro en el seleccionado.
- **Cadenas de física que no saltan al chocar**: un cable en Heavy Chain apoyado en el cuerpo ya no rebota ni gira sin
  motivo; en un personaje de prueba, los eslabones que giraban más de 60° en un cuadro pasaron de 420 a 0, con el mismo costo.
- **Pelaje que sigue las manos** en mallas con Subdivision antes del Armature.
- **Exportar a Real Engine**: las piezas emparentadas a huesos salen unidas a ellos.

### Novedades de la 0.45 y de Mobile 0.27

- **Denoise temporal en el render de animación** (Render > Denoise temporal en la animación, activado por defecto): cada
  cuadro del Ctrl+F12 continúa el denoise del anterior, llevado por el movimiento, y el ruido que queda ya no parpadea. En
  los tres motores; el parpadeo bajó a menos de la mitad, sin estela en lo que se mueve.
- **Drivers de encendido/apagado iguales a Blender**: los huesos que encienden ojos, muestran accesorios o cambian IK/FK
  en el límite ahora cambian como en Blender (comprobado en los rigs FNAF 2 de NovaBandit).
- **Pelaje con el color del material en la vista**: en Material Preview y en Sólido > Textura, la textura del material en
  cada pelo.
- **Tiempo real nítido sin DLSS**: quieta, la vista vuelve a la resolución completa.
- **Huesos con Visible y Seleccionable**, en el panel del hueso y en el Outliner (ojo y flecha).

### Novedades de la 0.44 y de Mobile 0.26

- **G y R en huesos con Child Of** ya no hacen saltar el hueso lejos del ratón (la cabeza de un rig con cambio de espacio).
- **Las cadenas de la simulación de huesos se asientan**: muchos huesos cortos con Dynamic Chain y Heavy Chain (cables) ya
  no giran sin parar; caen, se detienen y hacen el látigo al balancearse.
- **Editor de drivers**: el menú Añadir variable ya no cierra el programa.

### Novedades de la 0.43 y de Mobile 0.25

- **Cámara virtual desde el celular**: con Tlender Mobile, girar y caminar con el celular mueve la cámara que filma
  la escena del PC (siguiendo los cortes del Ctrl+B), con la imagen de la cámara en la pantalla del celular y keys grabadas al reproducir.
- **Render del Tiempo real en la mejor calidad**: F12 y Ctrl+F12 usan siempre la malla entera, las imágenes enteras y
  todos los fotogramas, sin límite de tiempo; la malla de los personajes ya no parpadea en las animaciones.
- **Playblast por el Tiempo real**: con la vista en Renderizado, el Playblast graba la imagen del Tiempo real, con luces,
  sombras y desenfoque de movimiento.
- **Personajes pesados a más de 300 fotogramas por segundo en vez de 36**, sin tirones (normales en todos los núcleos,
  videos sin uso fuera de la reproducción).
- **Sync to Audio al ritmo de la escena** aunque el programa vaya lento, y la **vista de cámara** ya no cambia de cámara
  al añadir o mover objetos (Ctrl+Numpad 0 elige la cámara de la escena).

### Novedades de la 0.42 y de Mobile 0.24

- **Archivos dentro del .tlend**: *Archivo > Datos externos > Empaquetar recursos* guarda texturas, sonidos, videos,
  volúmenes y fuentes dentro del archivo, que se abre en otra computadora sin las carpetas; desempaquetar con las opciones
  de Blender.
- **Rutas relativas (`//`)**: lo que está dentro de la carpeta del proyecto se guarda como `//carpeta/archivo`, así se
  puede mover o enviar la carpeta entera.
- **Búsqueda inteligente de archivos que faltan**: cuando las texturas, sonidos o videos de una escena no están en la
  computadora, Tlender los busca solo: por el contenido (aunque estén renombrados), por las carpetas del proyecto, por el
  nombre, por otra extensión y por nombres parecidos, y los cambia todos con un clic.
- **Aviso de "Guardado"** después de Ctrl+S y **archivos de Blender 2.79** (capas, grupos y materiales de Blender Internal).

### Novedades de la 0.41 y de Mobile 0.23

- **Los personajes llenos de modificadores se reproducen mucho más rápido**: con Mirror, Armature, Delta Mush, Subdivisión,
  Solidify y Displace sobre el esqueleto, un cuadro de la animación bajó de 134 ms a 9 ms (de 7 a más de 100 cuadros por
  segundo); los deformadores solo mueven los vértices, sin copiar toda la malla, y el resultado es el mismo.
- **Escenas con miles de objetos separados**: 10 mil objetos se reproducen a 37 cuadros por segundo (antes 4); el viewport
  ya no dibuja lo que está fuera del encuadre y el Outliner bajó de 60 ms a menos de 1 ms por cuadro.

### Novedades de la 0.40 y de Mobile 0.22

- **Rigs de terceros iguales que en Blender**: 14 de los 15 animatrónicos del FNAF 2 de NovaBandit ahora se mueven
  exactamente como en Blender (antes 4): piezas en los pistones, cables, ojos con driver por curva, dos IK en el mismo
  brazo; las asas Bezier siguen la regla de Blender actual en toda curva de animación.
- **Cables que se arrastran al reproducir**: en los rigs con "física" de cables, el cable se queda atrás de la mano al
  reproducir y se asienta al detenerse.
- **El Retarget reconoce muchos más personajes**: agentes de Valorant, FNAF 1 y humanos del FNAF 2, Mario, Woody, Kissy
  Missy, Huggy, BoxyBoo y más (56 de 254 rigs probados mejoraron); cinco rigs que cerraban el programa al abrirlos ahora
  se abren.

### Novedades de la 0.39 y de Mobile 0.21

- **Escenas pesadas rápidas**: un personaje lleno de modificadores con mocap grabado cuadro a cuadro se reproducía a 8
  cuadros por segundo y ahora a 33; guardar una escena de 1 millón de keys pasó de 3,3 s a 0,45 s y el autoguardado espera a
  que dejes de mover; el deshacer ya no copia todas las keys en cada paso.
- **G y R por la cámara y X/Y en el Graph Editor**, como en Blender: G mueve y R gira la cámara mirando por ella; G X / G Y
  y S X / S Y en el Graph Editor.
- **Mocap más limpio**: pies que no se deslizan en el Retarget (de 30–50 cm a unos 2 cm por paso), dedos correctos en rigs
  cuyas falanges copian un control, y la pelvis sin tirones (PC).

### Novedades de la 0.38 y de Mobile 0.20

- **Cara en personajes con partes**: un personaje con solo mandíbula, ojos y párpados en huesos (sin labios ni shape
  keys) recibe la cara del mocap en lo que tiene: la boca por la mandíbula, la mirada a los lados y arriba y abajo, los
  párpados parpadeando. Shape keys de expresión con ojos en huesos también.
- **Límites del rig en el Retarget**: Limit Rotation y Limit Location del personaje respetados en el Retarget, el
  horneado y la cara; los huesos de abajo compensan lo que el de arriba no pudo.
- **Solo cuerpo, Solo cara, Cuerpo y cara** (PC): en la pestaña Mocap, graba el cuerpo con una cámara y la cara de cerca
  con otra; el vídeo Solo cara da su cara al cuerpo del grupo, sincronizado por el sonido.

### Novedades de la 0.37 y de Mobile 0.19

- **Retarget en todos los auto-rigs**: Auto-Rig Pro, Rigify (el nuevo, el legado y el FBX), Mixamo, MetaHuman, el Mannequin de Unreal, Character Creator / iClone / AccuRIG, Daz Genesis 8 y 9, VRoid / VRM, HumanIK de Maya y los nombres del Humanoid de Unity, y rigs propios de estudio (los accesorios nunca son
  miembro). Manos y pies en **IK o FK**, cada miembro a su manera; un rig solo con IK va por el IK; **Configurar rig**
  para un rig propio, guardado en el perfil.
- **Cara modular**: expresiones propias (cara no humana), muchos a muchos, shape keys en portugués y la cara por un
  panel de sliders junto a la cabeza.
- **Física de los huesos** en la malla al reproducir (antes solo después del horneado), hueso con física animable en
  Modo Pose y el horneado en la acción de la línea de tiempo.
- Los vídeos fuera de la vista no se decodifican al reproducir (sin lag); el vídeo del mocap en el Image Editor.

### Corrección de la 0.36 y de Mobile 0.18

- La 0.35 se cerraba al abrir cuando la interfaz guardada tenía un editor Retarget. **Si su 0.35 se cierra al abrir**,
  descargue `Tlender-0.36-win64.zip` en la [release](https://github.com/NathanLourencoPeixoto/tlender-releases/releases/latest) y extráigalo encima de la carpeta de Tlender. Desde la
  0.36, una apertura que se cierra hace que la siguiente abra con las pestañas de fábrica y busque una actualización enseguida.

### Novedades de la 0.35 y de Mobile 0.17

- **La interfaz guardada, como en Blender** (PC y Mobile): cambiar pestañas y áreas ya no guarda solo; Guardar
  preferencias guarda la interfaz, y vuelve al abrir Tlender y en Archivo > Nuevo.
- **La pestaña Mocap sigue al archivo**: Archivo > Nuevo deja la pestaña vacía, cada .tlend tiene su lista de vídeos y
  cada vídeo tiene una papelera para quitarlo de la lista (y "Vaciar la lista").
- **Limpiar mapa en el Retarget** (PC y Mobile): quita el hueso de todos los papeles de un lado (Ctrl+Z lo deshace), y
  Limpiar todo en la cara; y el IK del personaje apagado por defecto (los miembros van en FK; "Usar el IK del rig" lo enciende).

### Novedades de la 0.34 y de Mobile 0.16

- **Mocap rehecho sobre RGB MoCap**, dentro de Tlender (usa los runtimes y modelos de su instalación de RGB MoCap): ExMR,
  FlowHMR o GVHMR, **varios vídeos** (persona nueva u otro ángulo, sincronizados solos), girar el vídeo, encontrar
  personas, barra con el tiempo restante, corrección de contactos editable, cara, exportar FBX/BVH, **muñeco 3D** y
  **root motion** (andando o en el sitio). En una toma de webcam + celular, el error del cuerpo en el mundo bajó de
  13,5 cm (RGB MoCap) a 9 cm con la webcam y 7,1 cm con los dos ángulos. PC con NVIDIA.
- **Retarget a cualquier personaje** (PC y Mobile), ahora un editor: siluetas de las partes del cuerpo, vista previa
  igual al horneado, "En el sitio", ajuste por hueso, la **cara** en shape keys o huesos/controles (cada expresión ligada
  a un objetivo) y **perfiles** guardados por rig. El cálculo es el de RGB MoCap: 1,4 cm de su resultado (antes 13 cm), y
  los rigs reales funcionan (Auto-Rig Pro, rigs de juego, piernas en IK con polo, rigs que estiran).
- **Importar el FBX de RGB MoCap**, con la cara ARKit/Live Link.

### Novedades de la 0.31

- **Mocap en tus personajes**: Aplicar prepara cualquier rig humano por sí solo (Auto-Rig Pro también), el personaje
  queda firme (sin temblar ni caminar por el mundo), la cara de rigs Auto-Rig Pro va por los controles, se detecta la
  lengua y el polish gana una capa propia sobre la capa del mocap, editable y con menos claves.
- **Sin giros del cuerpo** con una cámara, y los brazos ya no saltan entre cuadros; una pierna que aparece en medio de
  la imagen ahora se sigue.
- **Rastreo 3 veces más rápido** (video de 35 s: ~90 s -> ~30 s); los videos 4K se leen más de dos veces más rápido.
- **Verificar con Claude** (opcional, con tu clave de la API de Claude): cuadros clave verificados para saber hacia
  dónde mira el actor y qué aparece en el cuadro.
- **Webcam + celular**: los videos de celular en vertical entran en la posición correcta, dos cámaras sin sonido se
  sincronizan por el movimiento y la calibración funciona aunque una cámara no muestre los pies.
- **Pies en el piso sin saltitos**: la limpieza del mocap usa las ideas de contacto de RGBMocap, cada una medida antes:
  la altura de la cadera sigue una curva suave que deja los pies quietos en el piso (cadera que andaba 4,4 m parado de
  pie -> 2,8 m), los pies trabados entran y salen sin tirón y los saltos de verdad siguen siendo saltos.
- **Piernas fuera del cuadro ya no tiran**: con una cámara, la estimación 3D de un hueso solo cuenta cuando la red lo
  ve de verdad.
- **Cuerpo por FlowHMR (externo, PC con NVIDIA)**: el paso Rastrear puede usar FlowHMR, un modelo temporal de cuerpo
  entero que tiembla mucho menos que las redes cuadro a cuadro, en un entorno Python tuyo (`tools/flowhmr_setup.ps1`).

### También nuevo desde la 0.29 (primero en la beta 0.30_b)

- **Mocap con vídeos de verdad**: lo que no aparece en el vídeo (las piernas en una webcam, un brazo que sale del cuadro)
  se queda quieto en lugar de agitarse: pose T si nunca aparece, la última pose vista hasta 2 s, y una vuelta suave. Los
  vídeos de torso y brazos ahora rastrean el cuerpo y la cara.
- **Vista previa 3D de la cara** en el paso Rastrear: una cabeza con las 52 expresiones ARKit movida por el rastreo, y la
  malla de la cara (ojos, iris, labios, contorno) dibujada sobre el vídeo.

### Novedades de la 0.29

- **Mocap por video**: la pestaña Mocap lleva del video a la animación en 6 pasos (Fuentes, Sincronizar, Calibrar,
  Rastrear, Limpiar, Aplicar). Cuerpo, manos y cara, juntos o por separado, por videos, webcam, celular (se vuelve cámara
  por Wi-Fi con un código QR) o varias cámaras y un dron a la vez, sincronizados y calibrados solos.
- **En cualquier personaje**: el esqueleto listo "Mocap Tlender" o el rig de su personaje (Mixamo, Unreal, CC, auto-rig,
  Rigify); la cara en shape keys, huesos reales, rigs mixtos o rigs con controles.
- **Exportar al Real Engine (.tlend)** con las mallas evaluadas y los nodos horneados en imágenes.
- Selección por caja como en Blender (cualquier parte visible del objeto), texturas que se actualizan solas cuando el
  archivo cambia y apertura más rápida (~7 s -> 2,4 s).

### Novedades de la 0.28

- **Sin esperar los kernels de la GPU**: F12 y la vista Renderizada muestran la imagen casi al instante (34,8 s -> 0,6 s
  en la escena de prueba) mientras el kernel completo termina en segundo plano, y cambian a él sin pantalla negra.
- **Kernels guardados uno a uno**: la segunda apertura tiene todo listo en 0,3 s; después de una actualización solo se
  recompila lo que cambió; una barra de progreso real que dice lo que falta.
- **Tiempo real compila más rápido** (solo los grupos de nodos que usa la escena: 128 s -> 56 s).
- Se retiraron los portales entre escenas; las varias escenas, las View Layers y la escena dentro de escena se
  mantienen.

## Capturas

![La vista Renderizada con Ray Tracing: ladrillo, vidrio, cromo y lava](img/rendered-view.jpg)

![El Modo Edición con las herramientas de modelado en columnas](img/modeling-columns.jpg)

## Más rápido que Blender

Medido en la misma máquina, con el mismo archivo en los dos programas (Blender 5.1):

![Cuántas veces Tlender es más rápido que Blender](img/speed-vs-blender-es.svg)

![Tiempo de render: Tlender frente a Cycles](img/render-vs-cycles-es.svg)

## Fiel a Blender

El objetivo es el mismo resultado que da Blender, con el mismo archivo:

| Qué se comparó | Resultado |
|---|---|
| Luces (sol, foco y área) frente a Cycles | sol y foco idénticos; luz de área a menos del 0,1% |
| Archivos glTF exportados, abiertos en 6 versiones de Blender (4.0 a 5.3) | 66 de 66 correctos |
| Archivos FBX exportados, abiertos en las mismas 6 versiones | 54 de 54 correctos (vértices con piel a 0,000005) |
| Drivers de un rig de producción importado desde `.blend` | 370 de 370 iguales |
| `.blend` | abre de Blender 2.7x a 5.3 y guarda para 4.0, 4.2, 4.5, 5.0, 5.1 o 5.3 |

## Lo que Tlender tiene y Blender no

- **Tres renderizadores**: *Ray Tracing* (path tracer como Cycles), *Render X* (más rápido con luz indirecta) y *Tiempo
  real*, con **DLSS** y Ray Reconstruction en los tres.
- **Posar arrastrando en cualquier rig**: reconoce Auto-Rig Pro, Rigify, AdvancedSkeleton, Mixamo, MetaHuman, VRoid,
  Character Creator, Daz y otros, y posa con los controles del propio rig.
- **Herramientas de animador**: etapas Bloquear/Spline/Pulir, espacios temporales, fijar en el mundo, dibujo 2D por
  fotograma, fantasmas, arcos, gráfico de espaciado y ayuda de física (centro de masa y trayectoria).
- **Lip sync en portugués**, recorte con pines sin pantalla verde (SAM 2.1 + ViTMatte) con mapas PBR y plano físico ante la cámara, multitudes y captura de movimiento en vivo.
- **Física**: líquidos y gases en vóxeles, fuego que ilumina la escena, telas, cuerdas y cadenas, cuerpos rígidos,
  destrucción, lluvia que moja y escurre, pelo con física.
- **Texture Graph** en vivo en los materiales, en 16 bits, animable y calculado en la GPU.
- **Modo Maya**: atajos, iconos, Hotbox y Attribute Editor para quien viene de Maya.
- **Denoise temporal en la animación**, también en el path tracer: el ruido que queda no parpadea de un cuadro a otro.
- **Busca archivos que faltan por su contenido**: la textura renombrada o la carpeta del proyecto movida a otro disco.
- **Exporta a Real Engine**, el motor de juegos del mismo autor.
- **Tlender Mobile**: el mismo programa en móviles y tabletas Android, con interfaz para tacto y lápiz.

## Reportar un problema

En el programa: *Ayuda > Reportar un error* (o el escarabajo de la barra de estado) o *Enviar sugerencia*. El texto, las
imágenes y el informe de fallo se envían directamente, sin necesidad de cuenta en GitHub.
