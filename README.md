# GTR2N — GT Racing 2 PC

Port nativo para **Windows x64** de *GT Racing 2: The Real Car Experience* (Android, versão **1.6.1c**), com launcher próprio, melhorias gráficas e suporte a teclado e gamepad.

> **Aviso:** este é um projeto de preservação e estudo, sem fins lucrativos e sem afiliação com a Gameloft. Este repositório e os releases **não contêm** nenhum arquivo do jogo (APK, `libGT2.so`, OBBs ou assets). Você precisa fornecer os seus próprios arquivos, obtidos de uma cópia que você possui legitimamente.

Página do projeto: ative o GitHub Pages em *Settings → Pages* (branch `main`, pasta `/docs`).

---

## Como funciona

O projeto não recompila o jogo para x64. Ele traz um **runtime nativo para Windows** (base AndroidRecomp + Dynarmic + SDL2 + OpenGL) que carrega a biblioteca original `libGT2.so` (ARMv7) e emula a CPU dela. O runtime também implementa as partes de Android de que o jogo depende (JNI, OpenGL ES, OpenSL ES) e lê os OBBs originais diretamente, sem precisar extraí-los.

Os patches de compatibilidade e de melhoria gráfica são aplicados em memória, no momento da execução. O `libGT2.so` original nunca é alterado em disco.

## Requisitos

- Windows 10 ou 11 (64 bits)
- GPU com OpenGL 3.3 ou superior
- Os arquivos da versão exata **1.6.1c**:
  - `com.gameloft.android.ANMP.GloftRAHM-1.6.1c.apk`
  - `main.15927.com.gameloft.android.ANMP.GloftRAHM.obb`
  - `patch.16122.com.gameloft.android.ANMP.GloftRAHM.obb`

Outras versões **não funcionam**, porque os patches usam offsets fixos dentro do `libGT2.so`.

## Instalação

1. Baixe o `.zip` mais recente na página de [Releases](../../releases) e extraia em uma pasta de sua escolha.
2. Coloque, ou aponte no launcher, o APK e os dois OBBs.
3. Abra o launcher, ajuste as opções e clique em **Iniciar**.

## Recursos

### Melhorias gráficas

| Opção | Descrição |
|---|---|
| Taxa de quadros | Limite interno de 30 FPS removido. Escolha 30, 60, 120, 144, 240 ou ilimitado. |
| MSAA | Anti-aliasing por hardware: desativado, 2x, 4x ou 8x. |
| Filtragem anisotrópica | De 1x até 16x. |
| Campo de visão (FOV) | Multiplicador do FOV 3D, sem distorcer a interface 2D. O valor 1.25 é indicado para ultrawide. |
| Perfil gráfico | Perfil de GPU forçado para `GPU_HIGH`. |
| Reflexos | Texturas de reflexo em tempo real a 1024×1024. |
| Profundidade | Buffer de 24 bits para reduzir o z-fighting. |
| Resolução e tela | Resolução fixa, nativa do monitor ou automática. Tela cheia sem bordas (**F11** alterna a qualquer momento). |

### Controles

| Ação | Teclado | Gamepad (Xbox / PlayStation) |
|---|---|---|
| Acelerar | `W` / `↑` | Gatilho direito (RT / R2) |
| Frear / ré | `S` / `↓` | Gatilho esquerdo (LT / L2) |
| Direção | `A` `D` / `←` `→` | Analógico esquerdo ou direcional |
| Câmera | `C` | Y / Triângulo |
| Pausar | `P` / `Tab` / `Esc` | Start |
| Menus | Mouse, `Enter` / `Esc` | Direcional, A (confirmar), B (voltar) |

### Launcher

- Configuração de vídeo e gráficos, gravada no `config.ini`.
- Gerenciador de saves: backup, restauração, importação, exportação e reset (com backup preventivo).
- Perfis de configuração.

## Configuração manual

O runtime lê o arquivo `config.ini` que fica ao lado do executável:

```ini
[video]
mode = auto          ; auto | native (usado quando width/height = 0)
width = 1920
height = 1080
fullscreen = 0
fps_limit = 120      ; 0 = ilimitado

[graphics]
msaa = 4             ; 0, 2, 4 ou 8
anisotropy = 16      ; 1, 2, 4, 8 ou 16
fov_multiplier = 1.15

[log]
verbose = 0
```

## Roadmap

- [ ] Launcher que detecta o APK e os OBBs, valida a versão (nome e SHA-256 do `libGT2.so`) e monta sozinho a pasta do jogo.
- [ ] Caminhos relativos no `config.ini`, para a pasta poder ser movida.
- [ ] Remapeamento real de teclas e botões (hoje os atalhos são fixos no runtime).
- [ ] Perfis com saves separados.

## Problemas conhecidos

- O jogo foi testado em um conjunto limitado de configurações, e podem ocorrer travamentos em algumas GPUs.
- Recursos online (Google Play Services, loja, anúncios) não funcionam e foram desativados.

Encontrou um bug? Abra uma [issue](../../issues) com o seu modelo de GPU, a versão do Windows e o arquivo de log.

## Créditos

- **Gameloft**: jogo original *GT Racing 2: The Real Car Experience*. Todos os direitos pertencem aos seus donos.
- **AndroidRecomp**: base do runtime.
- **Dynarmic**: emulação de ARMv7.
- **SDL2**, **glad** e **stb**: janela, entrada e OpenGL.

Cada componente de terceiros segue a sua própria licença.

## Licença

O código original deste projeto (launcher e patches) é distribuído sob a licença escolhida pelo autor. Veja o arquivo `LICENSE`. O jogo, a marca e os assets não estão incluídos e não são licenciados por este projeto.
