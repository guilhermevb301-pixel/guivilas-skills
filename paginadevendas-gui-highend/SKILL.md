---
name: paginadevendas-gui-highend
description: Cria páginas de vendas HTML standalone de alto padrão para infoprodutos do Gui (cursos, mentorias, agentes de IA). Use SEMPRE que o Gui pedir "página de vendas", "landing page", "cria uma página pra mim", "faz uma página de [produto]". Faz perguntas obrigatórias antes de escrever qualquer código. Entrega index.html autocontido, responsivo, com design premium diferenciado — hero video ambient, tipografia Clash Display + Inter, glassmorphism, scroll reveals, micro-animações.
---

# Página de Vendas Highend — Infoprodutos do Gui

Skill para criar landing pages de conversão premium para cursos, mentorias e produtos digitais.
Resultado: `index.html` standalone, sem dependências externas além de Google Fonts + Fontshare.

---

## PASSO 0 — Intake obrigatório (SEMPRE perguntar antes de codar)

Antes de escrever uma linha de código, faça TODAS essas perguntas. Organize em blocos:

### Bloco 1 — Identidade do produto
- Qual o nome do produto e o nome da marca?
- Qual o público-alvo (quem compra, qual dor resolve)?
- Qual o preço e formato (parcelamento)?
- Tem garantia? Quantos dias?
- Qual o link de compra / CTA principal?

### Bloco 2 — Visual
- **Paleta de cores:** tem alguma cor definida ou quer sugestão?
- **Estilo:** luxuoso/editorial, moderno/tech, profissional/corporativo ou vibrante/jovem?
- **Fontes:** quer seguir o padrão da skill (Clash Display + Inter) ou tem preferência?

### Bloco 3 — Conteúdo do produto (infoproduto)
- Quantos módulos tem o treinamento? Quais os nomes?
- Quais as principais aulas ou entregas de cada módulo?
- Tem bônus? Quais?
- Tem depoimentos? Me manda os textos/nomes.
- Tem foto ou vídeo do mentor/criador?

### Bloco 4 — Hero Section
- **Mídia da hero:** vai ter vídeo de fundo (ambient video) ou imagem estática?
  - Se vídeo: tem um vídeo pronto? Ou quer sugestão de prompt para gerar no Higgsfield/Seedance?
  - Se imagem: tem start frame + end frame (para animação de transição) ou só start frame?
- **Ideia da hero:** como quer que o visitante se sinta ao chegar? (ex: poder, transformação, exclusividade, urgência)
- **Headline:** tem alguma ideia ou quer que eu proponha?

### Bloco 5 — Integrações
- Quer conectar com MCP do Higgsfield para gerar imagens/vídeos direto na skill?
- Ou prefere só os prompts prontos para você gerar manualmente?

---

## PASSO 1 — Sugestões de animação da Hero (sempre apresentar 2 opções)

Com base no tema e estilo informados, proponha 2 direções criativas para a hero antes de codar:

**Exemplo para tema "IA + tecnologia":**
> **Opção A — Ambient Video:** vídeo de fundo gerado no Seedance/Higgsfield com cena estática e elementos flutuando (ícones de IA, hologrmas, código). Opacidade 0.55–0.65. Overlay gradient escuro. Texto branco em destaque total.
>
> **Opção B — Split Screen com Start Frame:** foto/imagem do mentor à direita (fade para o fundo), headline grande à esquerda. Sem vídeo. Mais clean, mais credibilidade pessoal.

Espere o Gui escolher antes de codificar.

---

## PASSO 2 — Design System

### Paleta padrão para infoprodutos tech/IA
```css
--bg:           #08080a;   /* fundo principal */
--surface:      #111114;   /* cards, seções alternadas */
--surface-2:    #18181c;   /* hover states */
--border:       #1c1c20;   /* bordas sutis */
--border-strong:#2a2a30;   /* bordas visíveis */
--text:         #f8f8fa;   /* texto principal */
--text-muted:   #8b8b9a;   /* texto secundário */
--text-faint:   #4a4a56;   /* labels, captions */
--accent:       #7C3AED;   /* roxo — padrão Gênios da IA */
--accent-light: #A78BFA;
--accent-dark:  #5B21B6;
--accent-2:     #3B82F6;   /* azul complementar */
--grad:         linear-gradient(135deg, #7C3AED, #3B82F6);
```

**Para outros estilos, adapte a cor de acento mas NUNCA mude o fundo escuro.**
- Luxuoso/editorial → `--accent: #c9a84c` (dourado)
- Saúde/bem-estar → `--accent: #10b981` (verde esmeralda)
- Premium feminino → `--accent: #ec4899` (rosa)

### Tipografia (padrão obrigatório)
```html
<!-- No <head> -->
<link rel="preconnect" href="https://api.fontshare.com">
<link href="https://api.fontshare.com/v2/css?f[]=clash-display@600,700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&display=swap" rel="stylesheet">
```

```css
/* Headlines H1, H2 */
h1, h2 {
  font-family: 'Clash Display', 'Inter', sans-serif;
  font-weight: 700;
  letter-spacing: -0.02em;
  line-height: 1.1;
}

/* H1 hero */
h1 { font-size: clamp(2.8rem, 6vw, 5rem); }

/* H2 seções */
h2 { font-size: clamp(2rem, 4vw, 3rem); }

/* Body */
body { font-family: 'Inter', sans-serif; font-size: 1rem; line-height: 1.6; }

/* Lead text */
.lead { font-size: clamp(1.1rem, 1.8vw, 1.3rem); color: var(--text-muted); line-height: 1.65; }

/* Números/métricas */
.stat-num, .price { font-family: 'Inter', sans-serif; font-weight: 900; letter-spacing: -0.03em; }
```

**Proibido:** Roboto, Inter puro para headlines, qualquer fonte serifada genérica.

### Grid e Espaçamento (base 8px)
```
4px  — micro gap
8px  — xs
16px — sm (padding interno de card)
24px — md
32px — lg (gap entre cards)
48px — xl
64px — 2xl (padding seção mobile)
96px — 3xl (padding seção desktop)
128px — hero padding
```

---

## PASSO 3 — Hero Section com Ambient Video (padrão obrigatório para infoprodutos)

### Estrutura HTML do hero
```html
<section class="hero">
  <!-- Ambient video — gerado no Higgsfield ou Seedance -->
  <video id="hero-video" class="hero-video-bg" autoplay muted playsinline preload="auto">
    <source src="../public/videos/hero-video.mp4" type="video/mp4">
  </video>
  <div class="hero-video-overlay"></div>
  <div class="hero-grid"></div> <!-- grid sutil de fundo -->

  <div class="container hero-content">
    <span class="eyebrow reveal">Categoria · Nome do Produto</span>
    <h1 class="reveal">Headline <span class="text-gradient">impactante</span><br>aqui</h1>
    <p class="lead reveal">Subheadline curta. Máximo 2 linhas. Foca na transformação.</p>
    <div class="reveal" style="margin-top: 40px;">
      <a href="#oferta" class="btn btn-primary btn-large">CTA Principal →</a>
      <div class="offer-trust" style="margin-top: 16px;">
        <span>Garantia X dias</span>
        <span>Acesso imediato</span>
        <span>Parcelado em 12x</span>
      </div>
    </div>
  </div>
</section>
```

### CSS do hero video (copiar sempre)
```css
.hero {
  position: relative;
  min-height: 100dvh;
  display: flex;
  align-items: center;
  overflow: hidden;
}

/* Ambient video — opacidade baixa para não competir com o texto */
.hero-video-bg {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 12%;
  z-index: -1;
  opacity: 0.62; /* ajustar entre 0.5 e 0.7 conforme o vídeo */
}

/* Overlay gradient para legibilidade do texto */
.hero-video-overlay {
  position: absolute;
  inset: 0;
  background:
    linear-gradient(to bottom,
      rgba(8,8,10,0.35) 0%,
      rgba(8,8,10,0.08) 35%,
      rgba(8,8,10,0.08) 60%,
      rgba(8,8,10,0.90) 100%
    ),
    linear-gradient(to right,
      rgba(8,8,10,0.38) 0%,
      transparent 25%,
      transparent 75%,
      rgba(8,8,10,0.38) 100%
    );
  z-index: 0;
  pointer-events: none;
}

/* Grid sutil de fundo */
.hero-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);
  background-size: 48px 48px;
  z-index: 0;
  pointer-events: none;
}

/* Conteúdo fica acima de tudo */
.hero-content {
  position: relative;
  z-index: 1;
  text-align: center;
  padding: 128px 24px 80px;
}

/* Texto branco obrigatório na hero */
.hero h1, .hero .lead { color: #ffffff !important; }
.hero .lead { font-weight: 700 !important; }
```

### Loop de vídeo seamless (boomerang a partir de um ponto)
Quando o vídeo tem uma cena parada nos últimos segundos, criar boomerang com ffmpeg e usar JS para loopear o trecho:

```bash
# Criar boomerang dos últimos 2 segundos (ex: seg 8-10 de vídeo de 10s)
ffmpeg -i input.mp4 \
  -filter_complex "
    [0:v]scale=1280:-2[scaled];
    [scaled]split[full][tmp];
    [tmp]trim=start=8:end=10,setpts=PTS-STARTPTS,reverse[boom];
    [full][boom]concat=n=2:v=1[out]
  " \
  -map "[out]" -c:v libx264 -crf 22 -preset fast -an output.mp4
```

```javascript
// JS: intro completo → boomerang do segundo 8 em loop eterno
(function() {
  var v = document.getElementById('hero-video');
  if (!v) return;
  var LOOP_START = 8;
  var LOOP_END   = 11.95; // duração total - 0.1s
  function jumpBack() { v.currentTime = LOOP_START; v.play(); }
  v.addEventListener('timeupdate', function() {
    if (v.currentTime >= LOOP_END) jumpBack();
  });
  v.addEventListener('ended', jumpBack);
})();
```

### Mobile: hero video em telas pequenas
```css
@media (max-width: 640px) {
  /* Opções: contain (mostra cena inteira) ou manter cover com posição ajustada */
  .hero-video-bg {
    object-fit: contain;
    object-position: center 15%;
    opacity: 0.75;
  }
  /* Botão full width no mobile */
  .hero-content .btn {
    width: 100%;
    white-space: normal;
    padding: 18px 20px;
  }
}
```

---

## PASSO 4 — Estrutura de Seções (infoprodutos)

Ordem padrão para cursos/mentorias:

1. **TOPBAR** — faixa de urgência com countdown
2. **HERO** — video ambient + headline + CTA
3. **STATS** — 4 números de prova social (DM Mono, gradient text)
4. **PROBLEMA** — 4 cards de dores do avatar
5. **MECANISMO** — diferencial único do produto (criar/vender/reter)
6. **PARA QUEM É** — split screen ou lista
7. **COMO FUNCIONA** — 5 passos em linha horizontal
8. **CURRÍCULO** — carrossel horizontal de módulos
9. **DEPOIMENTOS** — grid 3D ou wall de depoimentos
10. **OFERTA** — preço + parcelamento + bônus + garantia
11. **FAQ** — accordion, mín. 7 perguntas
12. **CTA FINAL** — urgência + botão

---

## PASSO 5 — Efeitos Obrigatórios

### Scroll Reveal (IntersectionObserver)
```css
.reveal {
  opacity: 0;
  transform: translateY(22px);
  transition: opacity 0.6s cubic-bezier(0.16,1,0.3,1),
              transform 0.6s cubic-bezier(0.16,1,0.3,1);
}
.reveal.visible { opacity: 1; transform: translateY(0); }
```
```javascript
// Sempre incluir no <script> no fim do body
(function() {
  var els = document.querySelectorAll('.reveal');
  var failsafe = setTimeout(function() {
    els.forEach(function(el) { el.classList.add('visible'); });
  }, 1500);
  if (!('IntersectionObserver' in window)) {
    els.forEach(function(el) { el.classList.add('visible'); });
    clearTimeout(failsafe); return;
  }
  var io = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
        io.unobserve(entry.target);
      }
    });
  }, { threshold: 0.05, rootMargin: '0px 0px 80px 0px' });
  els.forEach(function(el) { io.observe(el); });
})();
```

### Gradient Text (headline principal)
```css
.text-gradient {
  background: var(--grad);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

### Glow no hover de cards
```css
.card-hover {
  transition: transform 0.22s cubic-bezier(0.16,1,0.3,1),
              box-shadow 0.22s ease,
              border-color 0.22s ease;
}
.card-hover:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 40px rgba(0,0,0,0.45), 0 0 28px rgba(124,58,237,0.15);
  border-color: rgba(124,58,237,0.3);
}
```

### Cursor glow na hero
```css
.hero::after {
  content: '';
  position: absolute; inset: 0;
  background: radial-gradient(
    500px circle at var(--mx, 50%) var(--my, 50%),
    rgba(124,58,237,0.14) 0%, transparent 60%
  );
  pointer-events: none; z-index: 0; opacity: 0;
  transition: opacity 0.4s;
}
.hero.cursor-active::after { opacity: 1; }
```
```javascript
var hero = document.querySelector('.hero');
if (hero) {
  hero.addEventListener('mousemove', function(e) {
    var r = hero.getBoundingClientRect();
    hero.style.setProperty('--mx', (e.clientX - r.left) + 'px');
    hero.style.setProperty('--my', (e.clientY - r.top) + 'px');
    hero.classList.add('cursor-active');
  });
  hero.addEventListener('mouseleave', function() {
    hero.classList.remove('cursor-active');
  });
}
```

### Noise texture no body (sempre)
```css
body::before {
  content: '';
  position: fixed; inset: 0; z-index: 9999;
  pointer-events: none; opacity: 0.025;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
}
```

### Countdown de urgência (topbar)
```javascript
// Incluir no <script> — persiste 24h no localStorage
function initCountdown() {
  var target = document.querySelector('[data-countdown]');
  if (!target) return;
  var key = 'countdown_' + (target.dataset.countdown || 'default');
  var TTL = 24 * 60 * 60 * 1000;
  var endTime = Number(localStorage.getItem(key));
  if (!endTime || endTime < Date.now()) {
    endTime = Date.now() + TTL;
    localStorage.setItem(key, String(endTime));
  }
  var hEl = target.querySelector('[data-h]');
  var mEl = target.querySelector('[data-m]');
  var sEl = target.querySelector('[data-s]');
  function pad(n) { return String(n).padStart(2, '0'); }
  function tick() {
    var diff = Math.max(0, endTime - Date.now());
    if (hEl) hEl.textContent = pad(Math.floor(diff / 3600000));
    if (mEl) mEl.textContent = pad(Math.floor((diff % 3600000) / 60000));
    if (sEl) sEl.textContent = pad(Math.floor((diff % 60000) / 1000));
  }
  tick(); setInterval(tick, 1000);
}
```

---

## PASSO 6 — Carrossel de Módulos/Aulas (com imagens geradas por IA)

### Fluxo completo para gerar as imagens dos módulos

Quando o Gui informar os módulos/aulas no intake:

1. **Perguntar:** "Quer que eu gere os prompts para as imagens de cada módulo no Nano Banana Pro / Higgsfield?"
2. Se sim: gerar um prompt de imagem para cada módulo (estilo thumbnail de curso — dark background, ícone ou cena representativa, título do módulo em destaque)
3. Salvar imagens em `paginas-vendas/public/images/modulos/01-nome.png`, `02-nome.png`, etc.
4. Usar no carrossel abaixo

### Prompt padrão para imagens de módulo (Nano Banana Pro)

Para cada módulo, adaptar este template:
```
Dark cinematic course thumbnail, [tema do módulo], minimalist tech aesthetic.
Deep dark background #08080a, subtle purple glow accent (#7C3AED).
[Elemento visual principal do módulo — ex: laptop com código, ícone de robô, gráfico de vendas].
Clean bold white text at bottom: "[NÚMERO. NOME DO MÓDULO]".
16:9 ratio, ultra-sharp, 4K, no noise, professional course design.
```

Exemplos por tipo de módulo:
- **Ferramentas/Setup:** `laptop with purple glow on screen showing terminal code, dark desk`
- **Agente de IA:** `holographic AI robot floating, blue-purple glow, dark background`
- **Vendas/Prospecção:** `smartphone with WhatsApp chat interface, floating money icons, dark`
- **CRM/Sistema:** `clean dashboard UI floating in dark space, data visualization`
- **Claude Code:** `code editor open with Claude interface, purple ambient lighting`
- **Mentoria/Comunidade:** `group of abstract human silhouettes glowing, connected by light threads`

### CSS do Carrossel de Módulos (copiar completo)

```css
/* Carrossel horizontal com fade nas bordas */
.curriculum-outer {
  position: relative;
  overflow: hidden;
}
.curriculum-outer::before,
.curriculum-outer::after {
  content: '';
  position: absolute;
  top: 0; bottom: 24px;
  width: 48px;
  z-index: 2;
  pointer-events: none;
}
.curriculum-outer::before {
  left: 0;
  background: linear-gradient(to right, var(--bg) 0%, transparent 100%);
}
.curriculum-outer::after {
  right: 0;
  background: linear-gradient(to left, var(--bg) 0%, transparent 100%);
}
.curriculum-track {
  display: flex;
  gap: 20px;
  overflow-x: auto;
  scroll-behavior: smooth;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  padding: 8px 32px 16px;
  scrollbar-width: none;
}
.curriculum-track::-webkit-scrollbar { display: none; }

.curriculum-card {
  flex: 0 0 260px;
  scroll-snap-align: start;
  background: #111114;
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid transparent;
  transition: transform 0.25s, box-shadow 0.25s;
}
/* Variantes de cor — adaptar à paleta do produto */
.cv-purple { border-color: rgba(124, 58, 237, 0.3); }
.cv-orange { border-color: rgba(249, 115, 22, 0.3); }
.cv-blue   { border-color: rgba(59, 130, 246, 0.3); }
.cv-green  { border-color: rgba(16, 185, 129, 0.3); }

.curriculum-card:hover { transform: translateY(-6px); }
.cv-purple:hover { box-shadow: 0 16px 40px rgba(124,58,237,0.2); }
.cv-orange:hover { box-shadow: 0 16px 40px rgba(249,115,22,0.2); }
.cv-blue:hover   { box-shadow: 0 16px 40px rgba(59,130,246,0.2); }

.curriculum-card-img {
  width: 100%;
  aspect-ratio: 3/4;  /* portrait — ideal para thumbnail de aula */
  overflow: hidden;
  background: #0a0a0c;
}
.curriculum-card-img img {
  width: 100%; height: 100%;
  object-fit: cover;
  transition: transform 0.4s;
}
.curriculum-card:hover .curriculum-card-img img { transform: scale(1.04); }

.curriculum-card-body { padding: 14px 16px 18px; }
.curriculum-card-num {
  font-size: 0.68rem; font-weight: 800;
  letter-spacing: 0.12em; text-transform: uppercase;
  display: block; margin-bottom: 6px;
}
.cv-purple .curriculum-card-num { color: var(--accent-light); }
.cv-orange .curriculum-card-num { color: #F97316; }
.cv-blue   .curriculum-card-num { color: #60A5FA; }

.curriculum-card-title {
  font-size: 0.9rem; font-weight: 700;
  color: #f5f5f7; line-height: 1.3; margin-bottom: 6px;
}
.curriculum-card-desc {
  font-size: 0.75rem;
  color: rgba(255,255,255,0.42);
  line-height: 1.45;
}

/* Navegação com setas + dots */
.curriculum-nav {
  display: flex; justify-content: center;
  align-items: center; gap: 16px;
  margin-top: 12px;
}
.curriculum-arrow {
  width: 36px; height: 36px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.1rem; font-weight: 700;
  background: rgba(124,58,237,0.1);
  border: 1px solid rgba(124,58,237,0.25);
  color: var(--accent-light);
  transition: background 0.2s; cursor: pointer;
}
.curriculum-arrow:hover { background: rgba(124,58,237,0.25); }
.curriculum-dots { display: flex; gap: 6px; align-items: center; }
.curriculum-dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: rgba(255,255,255,0.18);
  transition: background 0.2s, width 0.2s;
}
.curriculum-dot.active {
  background: var(--accent-light);
  width: 18px; border-radius: 3px;
}
```

### HTML do Carrossel (template — adaptar módulos)

```html
<!-- ========== CURRÍCULO ========== -->
<section>
  <div class="container">
    <div class="section-header reveal">
      <span class="eyebrow">O que você vai aprender</span>
      <h2>Módulos do <span class="text-gradient">treinamento</span></h2>
      <p class="lead">Cada módulo é executável — você abre e segue junto.</p>
    </div>
    <div class="curriculum-outer reveal">
      <div class="curriculum-track" id="cvTrack">

        <div class="curriculum-card cv-purple">
          <div class="curriculum-card-img">
            <img src="../public/images/modulos/01-nome.png" alt="Módulo 1" loading="lazy">
          </div>
          <div class="curriculum-card-body">
            <span class="curriculum-card-num">01</span>
            <div class="curriculum-card-title">Nome do Módulo</div>
            <p class="curriculum-card-desc">Descrição curta do que o aluno aprende neste módulo.</p>
          </div>
        </div>

        <!-- Repetir para cada módulo. Alternar cv-purple / cv-orange / cv-blue -->

      </div>
    </div>

    <!-- Navegação -->
    <div class="curriculum-nav">
      <button class="curriculum-arrow" id="cvPrev">←</button>
      <div class="curriculum-dots" id="cvDots"></div>
      <button class="curriculum-arrow" id="cvNext">→</button>
    </div>
  </div>
</section>
```

### JS do Carrossel (copiar no `<script>` no fim do body)

```javascript
// Curriculum carousel
(function() {
  var track = document.getElementById('cvTrack');
  var prev  = document.getElementById('cvPrev');
  var next  = document.getElementById('cvNext');
  var dotsC = document.getElementById('cvDots');
  if (!track) return;

  var cards = track.querySelectorAll('.curriculum-card');
  var total = cards.length;
  var current = 0;

  // Gerar dots
  for (var i = 0; i < total; i++) {
    var d = document.createElement('div');
    d.className = 'curriculum-dot' + (i === 0 ? ' active' : '');
    dotsC.appendChild(d);
  }
  var dots = dotsC.querySelectorAll('.curriculum-dot');

  function updateDots() {
    var cardW = cards[0].offsetWidth + 20;
    current = Math.round(track.scrollLeft / cardW);
    dots.forEach(function(d, i) { d.classList.toggle('active', i === current); });
  }

  function step(dir) {
    var cardW = cards[0].offsetWidth + 20;
    track.scrollBy({ left: dir * cardW * 2, behavior: 'smooth' });
  }

  track.addEventListener('scroll', updateDots);
  prev.addEventListener('click', function() { step(-1); });
  next.addEventListener('click', function() { step(1); });
})();
```

---

## PASSO 7 — Depoimentos 3D Wall (padrão obrigatório)

### Quando usar
- Sempre que tiver 6+ depoimentos de texto
- Para vídeos de depoimento: usar grid de cards com vídeo vertical (9:16)

### CSS completo da 3D Wall

```css
.testimonials-3d-wrap {
  overflow: hidden;
  perspective: 1400px;
  padding: 24px 0 64px;
  margin-top: 48px;
  /* Fade nas bordas — efeito profissional */
  mask-image:
    linear-gradient(to bottom, transparent 0%, black 12%, black 88%, transparent 100%),
    linear-gradient(to right,  transparent 0%, black 8%,  black 92%, transparent 100%);
  mask-composite: intersect;
  -webkit-mask-image:
    linear-gradient(to bottom, transparent 0%, black 12%, black 88%, transparent 100%),
    linear-gradient(to right,  transparent 0%, black 8%,  black 92%, transparent 100%);
  -webkit-mask-composite: destination-in;
}

.testimonials-3d-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 14px;
  max-width: 980px;
  margin: 0 auto;
  /* Inclinação 3D — efeito tablero */
  transform: rotateX(20deg) rotateY(-5deg) scale(0.92);
  transform-origin: center 30%;
  transform-style: preserve-3d;
  padding: 0 16px;
}

.t3d-card {
  background: var(--surface);
  border: 1px solid var(--border-strong);
  border-radius: 14px;
  padding: 18px 20px;
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}
.t3d-card:hover {
  transform: translateZ(12px) translateY(-4px);
  box-shadow: 0 20px 48px rgba(0,0,0,0.55), 0 0 0 1px rgba(124,58,237,0.2);
}

.t3d-header { display: flex; align-items: center; gap: 10px; margin-bottom: 10px; }
.t3d-avatar {
  width: 36px; height: 36px; border-radius: 50%;
  background: linear-gradient(135deg, var(--accent-dark), var(--accent));
  display: flex; align-items: center; justify-content: center;
  color: #fff; font-weight: 700; font-size: 0.78rem; flex-shrink: 0;
}
.t3d-name   { font-weight: 700; font-size: 0.85rem; line-height: 1.2; }
.t3d-handle { font-size: 0.72rem; color: var(--text-muted); }
.t3d-text   { font-size: 0.84rem; line-height: 1.6; color: var(--text-muted); }
.t3d-result {
  display: inline-block; margin-top: 10px;
  font-size: 0.72rem; font-weight: 700;
  color: var(--accent-light);
  background: rgba(124,58,237,0.12);
  padding: 3px 10px; border-radius: 20px;
}

/* Mobile: sem perspectiva 3D, coluna única */
@media (max-width: 768px) {
  .testimonials-3d-wrap {
    perspective: none;
    mask-image: linear-gradient(to bottom, transparent 0%, black 5%, black 95%, transparent 100%);
    -webkit-mask-image: linear-gradient(to bottom, transparent 0%, black 5%, black 95%, transparent 100%);
  }
  .testimonials-3d-grid {
    grid-template-columns: 1fr;
    transform: none;
    max-width: 420px;
  }
}

/* Mobile: auto-scroll vertical infinito */
@media (max-width: 640px) {
  .testimonials-3d-wrap { height: 520px; overflow: hidden; }
  .testimonials-3d-grid {
    animation: t3d-scroll 28s linear infinite;
    max-width: 360px; margin: 0 auto;
  }
  .testimonials-3d-grid:hover,
  .testimonials-3d-grid:active { animation-play-state: paused; }
}
@keyframes t3d-scroll {
  from { transform: translateY(0); }
  to   { transform: translateY(-50%); }
}
```

### HTML da 3D Wall (template — substituir conteúdo)

```html
<!-- ========== DEPOIMENTOS 3D ========== -->
<section>
  <div class="container">
    <div class="section-header reveal">
      <span class="eyebrow">Depoimentos</span>
      <h2>Quem já <span class="text-gradient">transformou</span> o resultado</h2>
    </div>
    <div class="testimonials-3d-wrap">
      <div class="testimonials-3d-grid">

        <div class="t3d-card">
          <div class="t3d-header">
            <div class="t3d-avatar">AB</div>
            <div>
              <div class="t3d-name">Nome Sobrenome</div>
              <div class="t3d-handle">@instagram · Cidade</div>
            </div>
          </div>
          <p class="t3d-text">"Texto real do depoimento aqui. Quanto mais específico, mais converte."</p>
          <span class="t3d-result">✓ Resultado alcançado</span>
        </div>

        <!-- Repetir .t3d-card para cada depoimento. Mínimo 9 para o grid 3x3 ficar cheio. -->

      </div>
    </div>
  </div>
</section>
```

### JS para mobile scroll infinito (adicionar no `<script>`)

```javascript
// Depoimentos: clone para loop contínuo no mobile
(function() {
  if (window.innerWidth > 640) return;
  var grid = document.querySelector('.testimonials-3d-grid');
  if (!grid) return;
  grid.innerHTML += grid.innerHTML;
})();
```

---

## PASSO 9 — Prompts para gerar o vídeo da Hero

### Se o Gui não tem vídeo, oferecer estes prompts baseados no estilo:

**Estilo tech/IA (padrão Gênios da IA):**
> Prompt para Seedance: *"Static scene, dark room, person sitting at desk with laptop glowing with purple light, holographic AI icons (robot, gears, chat bubbles) floating slowly in mid-air. Ambient glow. Cinematic, ARRI Alexa, 50mm, locked tripod, no camera movement. 5 seconds."*

**Estilo autoridade/mentor:**
> Prompt para Higgsfield: *"Person in dark hoodie, sitting confident in modern home office, laptop open, soft purple accent lighting from left, bokeh background with bookshelves. Shallow DOF. Locked static camera. Slow subtle ambient motion only."*

**Após gerar o vídeo:**
1. Comprimir para 1280px: `ffmpeg -i input.mp4 -vf scale=1280:-2 -c:v libx264 -crf 22 -preset fast -an output.mp4`
2. Criar boomerang se necessário (ver Passo 3)
3. Salvar em `paginas-vendas/public/videos/`

---

## PASSO 10 — Checklist antes de entregar

- [ ] Perguntas de intake respondidas antes de codar
- [ ] Opções de hero apresentadas e escolha feita
- [ ] Módulos/aulas coletados → prompts de imagem gerados ou imagens recebidas
- [ ] Depoimentos coletados (mín. 9 textos para o grid 3x3 ficar cheio)
- [ ] Video ambient com opacidade 0.55–0.70
- [ ] Overlay gradient cobrindo bordas superior e inferior
- [ ] Fonts carregadas: Clash Display + Inter
- [ ] Gradient text na headline principal
- [ ] Scroll reveals com IntersectionObserver + failsafe 1500ms
- [ ] Noise texture no body (opacity 0.025)
- [ ] Cards com hover glow
- [ ] Cursor glow no hero
- [ ] Topbar com countdown de 24h
- [ ] Mobile: botão full-width, hero video contain em 640px
- [ ] CTA repetido no mínimo 3x na página (topo, meio, rodapé)
- [ ] FAQ com mínimo 7 perguntas
- [ ] Nenhuma dependência externa quebrada
- [ ] Deploy: `vercel --prod` na pasta `paginas-vendas/`

---

## Anti-padrões proibidos

- Hero centralizado sem movimento (parece site de 2018)
- Três cards idênticos em linha com mesmo tamanho
- Inter pura para headlines (sem Clash Display)
- `#000000` puro como fundo
- Gradientes neon genéricos em tudo
- Emojis no código
- Números redondos demais: usar `R$6.847` em vez de `R$7.000`
- Vídeo na hero SEM overlay (texto ilegível)
- Página sem countdown (mata urgência)
- FAQ com menos de 7 perguntas
