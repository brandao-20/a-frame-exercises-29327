# A-Frame Exercises (1–9)

Repositório com a resolução completa dos exercícios “A-Frame Exercises” (1 a 9), incluindo demonstrações com **A-Frame**, **aframe-gui**, **AR.js** (marker-based, image tracking/NFT e location-based) e **MindAR** (image tracking, multi-targets, multi-tracks, custom UI e events).

Este repositório é baseado no material fornecido pelo professor no PDF `IEU_2526_05.pdf` (disponível na pasta `docs/`), que descreve os exercícios de A-Frame para a unidade curricular Interação e Experiência de Utilizador. O PDF inclui introduções a A-Frame, exemplos, guias de início, exercícios específicos (como Exercise 1: base A-Frame, Exercise 2: GUI, Exercise 3: AR.js, Exercises 4-9: MindAR) e discussões sobre usabilidade em VR e AR.

> **Nota importante (iPhone)**: A funcionalidade AR (câmara) requer **HTTPS**. Para testar no iPhone, utilizei **GitHub Pages**.

---

## Conteúdo do projeto

- `exercise1/` — Cena A-Frame base (introdução / primeiros objetos).
- `exercise2-gui/` — GUI com **aframe-gui** (botões funcionais) + **patch de compatibilidade** com versões recentes de A-Frame/Three.js.
- `exercise3-arjs/`
  - `marker-based/` — AR.js marker-based com **Hiro marker** + botão para abrir o `marker.html`.
  - `image-tracking/` — AR.js **NFT (image tracking)** com imagem alvo e descritores (`.fset/.fset3/.iset`) e correção de paths.
  - `location-based/` — AR.js location-based com UI e **bússola/agulha** para orientar a direção.
- `exercise4-mindar-minimal/` — MindAR minimal (primeiro target `.mind`).
- `exercise5-mindar-basic/` — MindAR basic com modelo GLB e interação (toggle/anim).
- `exercise6-mindar-multi-targets/` — MindAR com **2 targets** e conteúdos diferentes.
- `exercise7-mindar-multi-tracks/` — MindAR com **maxTrack: 2** (2 targets visíveis ao mesmo tempo).
- `exercise8-mindar-custom-ui/` — MindAR com **UI personalizada** (loading/scanning/error overlays).
- `exercise9-mindar-events/` — MindAR com **eventos + controlos** (start/pause/unpause/stop) e log de estado.

---

## Requisitos

- Browser moderno (Chrome recomendado).
- Python 3 (para servidor local simples).
- Câmara (webcam no PC ou câmara do telemóvel).
- Para iPhone: servir via **HTTPS** (ex.: GitHub Pages).

---

## Como executar localmente (PC)

Na raiz do repositório, abre uma terminal/prompt e executa (segundo o teu sistema operativo):

**Linux / macOS**  
`python3 -m http.server 8000`

**Windows**  
`py -3 -m http.server 8000`

Depois abre no browser:  
http://localhost:8000/

Navega para o exercício que quiseres, por exemplo:

- http://localhost:8000/exercise2-gui/
- http://localhost:8000/exercise3-arjs/marker-based/
- http://localhost:8000/exercise4-mindar-minimal/

**Dica**: Vários exercícios têm um botão para abrir o `target.html` ou `marker.html` (útil para mostrar o marcador/target noutro ecrã ou imprimir).

---

## Como testar no iPhone (HTTPS)

1. Ativa o GitHub Pages no repositório:
   - Settings → Pages → Source → Deploy from branch → **main** → **/root**
2. Abre o URL que o GitHub te dá: https://<username>.github.io/<repo>/
3. Dá permissões de **Câmara** (e **Localização** nos exercícios location-based).

---

## Exercícios – Explicação detalhada

### Exercise 1 — A-Frame base
Cena inicial com geometrias simples e estrutura base para os exercícios seguintes.

### Exercise 2 — GUI (aframe-gui)
**Objetivo**: Criar um painel GUI com botões clicáveis.

**Implementação**:
- Mantida versão A-Frame 1.5.0.
- Adicionado patch de compatibilidade para geometrias antigas (`PlaneBufferGeometry`, etc.) usadas pela biblioteca aframe-gui.
- Painel com botões funcionais para:
  - Mudar cor do objeto
  - Rodar 360º
  - Reset

### Exercise 3A — AR.js (marker-based)
**Objetivo**: Usar o marcador Hiro para exibir conteúdo em AR.

**Implementação**:
- Página principal com indicação de estado.
- Botão “Abrir marker.html” para visualizar/imprimir o marcador.
- Detecção em tempo real do marcador Hiro.

**Teste no PC**: Abre `marker.html` noutro ecrã ou telemóvel e aponta a webcam.

### Exercise 3B — AR.js (image tracking / NFT)
**Objetivo**: Tracking por imagem natural (NFT).

**Implementação**:
- Imagem alvo com bom contraste/detalhes.
- Descritores NFT gerados (`.fset`, `.fset3`, `.iset`).
- Correção de caminhos para carregamento correto.
- Botões para abrir `target.html` e visualizar a imagem alvo.

**Notas**: A primeira carga pode demorar. Evita reflexos/brilho na imagem alvo.

### Exercise 3C — AR.js (location-based)
**Objetivo**: Conteúdo baseado em localização GPS e direção.

**Implementação**:
- UI com botões para iniciar permissões e posicionar alvos a diferentes distâncias.
- Exibição de coordenadas GPS e precisão.
- Bússola visual:
  - Agulha azul: heading atual
  - Agulha vermelha: direção para o alvo
  - Instruções textuais (“vira Xº à direita/esquerda” ou “alinhado ✅”)

**Notas**: Melhor precisão ao ar livre. Em interiores a accuracy pode ser baixa (30–50 m).

### Exercise 4 — MindAR (minimal)
**Objetivo**: Primeiro exemplo funcional de tracking com MindAR.

**Implementação**:
- Estrutura simples com `mindar-image` e ficheiro `.mind`.
- `target.html` para mostrar a imagem alvo.
- Conteúdo básico (plano + texto) ao detectar o target.

### Exercise 5 — MindAR (basic)
**Objetivo**: Tracking + modelo 3D + interação.

**Implementação**:
- Modelo GLB leve (Duck) com rotação contínua.
- Clique no plano para esconder/mostrar o modelo (toggle).

### Exercise 6 — MindAR (multi-targets)
**Objetivo**: Múltiplos targets no mesmo ficheiro `.mind` com conteúdos diferentes.

**Implementação**:
- Dois `<a-entity mindar-image-target>` com `targetIndex: 0` e `targetIndex: 1`.
- Conteúdos distintos (ex.: box vs sphere).

### Exercise 7 — MindAR (multi-tracks)
**Objetivo**: Tracking simultâneo de múltiplos targets.

**Implementação**:
- `maxTrack: 2` no componente `mindar-image`.
- Dois targets visíveis ao mesmo tempo quando ambos estão no campo de visão.

### Exercise 8 — MindAR (custom UI)
**Objetivo**: UI personalizada para estados de loading/scanning/error.

**Implementação**:
- Overlays HTML próprios.
- Ligação via atributos:
  - `uiLoading: #loadOverlay`
  - `uiScanning: #scanOverlay`
  - `uiError: #errorOverlay`
- Imagem “ghost” para facilitar alinhamento.

**Nota**: Em alguns PCs pode aparecer “WebGL not supported”. Funciona melhor em dispositivos móveis via HTTPS.

### Exercise 9 — MindAR (events)
**Objetivo**: Controlo manual do ciclo AR e reação a eventos.

**Implementação**:
- `autoStart: false` para controlo manual.
- Botões: Start / Pause / Unpause / Stop.
- Log de eventos:
  - `arReady`, `arError`
  - `targetFound`, `targetLost`
  - Clique no plano (A-Frame)

---

## Demonstração em Vídeo

Ficheiro no repositório: `video/Exercises_Full_Demo.mp4`

---

## Autor

**Nome**: Gabriel da Silva Brandão  
**Nº aluno**: 29327  
**UC**: Interação e Experiência de Utilizador  
**Data**: 14/12/2025