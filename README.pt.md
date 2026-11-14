# Tlender

[English](README.md) · **Português** · [Español](README.es.md)

**Tlender é um programa de 3D para modelar, animar e renderizar personagens e cenas**, feito do zero em C e Vulkan para
ser rápido. Ele usa os mesmos atalhos, menus e conceitos do Blender, então quem já usa o Blender se sente em casa, e abre
e salva arquivos `.blend`.

**Versão atual: 0.28** (14/11/2026) · Windows 10/11 64 bits · Português, English, Español ·
[Tlender Mobile para Android](https://github.com/NathanLourencoPeixoto/tlender-mobile-releases)

## O que você está baixando

Na [release mais recente](https://github.com/NathanLourencoPeixoto/tlender-releases/releases/latest) há três arquivos:

| Arquivo | O que é |
|---|---|
| `Tlender-<versão>-win64.zip` | **O programa.** Extraia a pasta onde quiser e abra o `tlender.exe` (não precisa instalar nada). |
| `Tlender-<versão>-win64.zip.sha256` | O código para conferir se o download chegou inteiro. |
| `Tlender-<versão>-win64.zip.sig` | A assinatura que o atualizador do Tlender confere antes de instalar uma versão nova. |

Dentro do zip vêm o `tlender.exe`, o instalador de atualizações (`tlender_updater.exe`), o denoiser (Intel OIDN), o
NVIDIA DLSS, o runtime do Visual C++ e um `LEIA-ME.txt`. Nada é instalado no sistema; as preferências ficam em
`%APPDATA%\Tlender`.

**Requisitos**: uma placa de vídeo com Vulkan 1.2. Para renderizar na GPU, ray tracing por hardware (NVIDIA RTX, AMD RX
6000 ou mais nova, Intel Arc); sem isso o render usa a CPU.

**Aviso do Windows**: o executável ainda não tem um certificado de assinatura de código, então o SmartScreen ou o
antivírus podem alertar na primeira vez. Clique em *Mais informações → Executar assim mesmo*. Cada pacote é assinado
pelo autor (o arquivo `.sig`), e o atualizador só instala versões com essa assinatura.

## Atualizações

O Tlender procura uma versão nova ao abrir e baixa **só os arquivos que mudaram**. A versão nova é instalada quando você
fecha o programa. Marcando *Usar a versão Beta do Tlender* nas Preferências você entra no **canal Beta** e recebe as versões de teste antes (elas
terminam em `_b`). Tudo o que mudou em cada versão está nas [releases](https://github.com/NathanLourencoPeixoto/tlender-releases/releases)
e no próprio programa (*Ajuda > Notas da versão*).

### Novidades da 0.28

- **Sem esperar os kernels da GPU**: o F12 e a vista Renderizada mostram a imagem quase na hora (34,8 s -> 0,6 s na cena
  de teste) enquanto o kernel completo termina em segundo plano, e trocam para ele sem tela preta.
- **Kernels guardados um por um**: a segunda abertura deixa tudo pronto em 0,3 s; depois de uma atualização só o que
  mudou recompila; barra de progresso de verdade, dizendo o que falta.
- **Tempo real compila mais rápido** (só os grupos de nodes que a cena usa: 128 s -> 56 s).
- Os portais entre cenas foram retirados; as várias cenas, as View Layers e a cena dentro de cena continuam.

## Capturas

![A vista Renderizada com o Ray Tracing: tijolo, vidro, cromo e lava](img/rendered-view.jpg)

![O Modo Edição com as ferramentas de modelagem em colunas](img/modeling-columns.jpg)

## Mais rápido que o Blender

Medido na mesma máquina, com o mesmo arquivo nos dois programas (Blender 5.1):

![Quantas vezes o Tlender é mais rápido que o Blender](img/speed-vs-blender-pt.svg)

![Tempo de render: Tlender contra Cycles](img/render-vs-cycles-pt.svg)

## Fiel ao Blender

A meta é o mesmo resultado que o Blender dá, com o mesmo arquivo:

| O que foi comparado | Resultado |
|---|---|
| Luzes (sol, spot e área) contra o Cycles | sol e spot iguais; luz de área a menos de 0,1% |
| Arquivos glTF exportados, abertos em 6 versões do Blender (4.0 a 5.3) | 66 de 66 corretos |
| Arquivos FBX exportados, abertos nas mesmas 6 versões | 54 de 54 corretos (vértices com pele a 0,000005) |
| Drivers de uma rig de produção importada do `.blend` | 370 de 370 iguais |
| `.blend` | abre do Blender 2.7x ao 5.3 e salva para 4.0, 4.2, 4.5, 5.0, 5.1 ou 5.3 |

## O que o Tlender tem que o Blender não tem

- **Três renderizadores**: *Ray Tracing* (path tracer como o Cycles), *Render X* (mais rápido em luz indireta) e *Tempo
  real*, com **DLSS** e Ray Reconstruction nos três.
- **Pose por arrasto em qualquer rig**: reconhece Auto-Rig Pro, Rigify, AdvancedSkeleton, Mixamo, MetaHuman, VRoid,
  Character Creator, Daz e outros, e posa pelos controles da própria rig.
- **Ferramentas de animador**: etapas Bloquear/Spline/Polir, espaços temporários, travar no mundo, desenho 2D por
  quadro, fantasmas, arcos, gráfico de espaçamento e ajuda de física (centro de massa e parábola).
- **Lip sync em português**, rotoscopia com IA (SAM 2), multidões e captura de movimento ao vivo.
- **Física**: líquidos e gases em voxels, fogo que ilumina a cena, tecidos, cordas e correntes, corpos rígidos,
  destruição, chuva que molha e escorre, hair com física.
- **Texture Graph** ao vivo nos materiais, em 16 bits, animável e calculado na GPU.
- **Modo Maya**: atalhos, ícones, Hotbox e Attribute Editor para quem vem do Maya.
- **Exporta para a Real Engine**, a game engine do mesmo autor.
- **Tlender Mobile**: o mesmo programa em celulares e tablets Android, com interface para toque e caneta.

## Reportar um problema

No programa: *Ajuda > Reportar um bug* (ou o besouro na barra de status) ou *Enviar sugestão*. O texto, as imagens e
o relatório de travamento são enviados direto, sem precisar de conta no GitHub.
