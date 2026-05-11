---
name: paginadevendas-gui-highend
description: Cria sites e páginas premium para negócios de serviço, produto físico e presença digital — imobiliárias, aluguel de carros, restaurantes, clínicas, academias, agências, portfólios, qualquer coisa que NÃO seja um infoproduto/curso. Use quando pedirem site para negócio físico, serviço, empresa ou marca. Design de agência $150k — double-bezel, pill nav flutuante, Z-axis cascade, editorial luxury. Sempre pergunta sobre a hero antes de codar: gera prompt de imagem (Nano Banana Pro) e pergunta se vai animar no Seedance.
---

# Site Premium — Serviços e Produtos Físicos

Skill para criar sites de alto padrão para negócios que **não são infoprodutos**.
Exemplos: imobiliária, aluguel de carros de luxo, restaurante, clínica, academia, agência, portfólio.
Entrega `index.html` standalone. Design sempre no nível de agência $150k.

---

## 🛑 GATE — ANTES DE QUALQUER CÓDIGO

**Faça estas três perguntas antes de escrever uma linha de HTML:**

**1. Paleta de cores**
Apresente as opções abaixo e pergunte qual se encaixa melhor:

> "Qual o estilo visual da página? Escolhe uma das opções:
>
> **A — Escuro premium** → fundo preto/espresso, tipografia clara, acento personalizável (dourado, roxo, azul, verde...)
> **B — Tech / SaaS** → OLED preto `#050505`, orbs de luz colorida no fundo, glassmorphism
> **C — Editorial clean** → fundo branco ou creme, tipografia serif grande, minimalismo de revista
> **D — Outra ideia** → me fala a paleta que você quer: cor de fundo, cor de destaque e clima geral"

Se a pessoa escolher A, B ou C mas **não especificar a cor de acento** → pergunte: *"Qual cor de destaque? (ex: dourado, roxo, azul cobalto, verde esmeralda, laranja...)"*
Se escolher D → aguarde a descrição e adapte o design system inteiro antes de codar.

**Nunca assuma dourado como padrão.** A cor de acento deve sempre vir da escolha da pessoa.

---

**2. Hero**
> "Qual é a ideia da hero? Me conta o tema, o clima que quer passar e se já tem alguma imagem ou vídeo pronto — ou se quer que eu sugira."

Com base na resposta:
- Gere o prompt de imagem para **Nano Banana Pro** (ver template abaixo) usando a paleta escolhida
- Entregue o prompt e pergunte: *"Quer transformar essa imagem em vídeo no Seedance para a hero ficar animada? Se sim: quantos segundos? Um único shot ou várias cenas? Tem algum movimento específico em mente?"*
- Se sim → gere o prompt Seedance (ver template abaixo)
- Se já tiver vídeo pronto → peça o caminho do arquivo

---

**3. Conteúdo mínimo do site**
> "Me conta o que o site precisa ter: nome do negócio, serviços/produtos principais, CTA (reserva? contato? WhatsApp?), e se tem depoimentos ou preços pra mostrar."

Só depois de ter os três blocos respondidos, escreva o código.

---

### Template — Prompt de imagem (Nano Banana Pro)

```
[Descrição visual da cena principal], cinematic composition, [paleta escura coerente com o negócio],
dramatic ambient lighting, ultra-sharp, 4K, hyper-realistic, no text, no logos,
professional [tipo de fotografia], wide angle.
```

Exemplos:
- **Imobiliária:** `luxury penthouse interior at night, floor-to-ceiling windows, city skyline, warm amber lighting, ultra-sharp 4K, no people`
- **Carros de luxo:** `McLaren 720S Papaya Orange parked on dark wet street, dramatic side lighting, fog, cinematic 4K`
- **Restaurante:** `high-end restaurant interior, candlelight on dark marble table, bokeh background, editorial food photography`
- **Clínica/spa:** `minimalist treatment room, soft warm light, white linen, japanese zen aesthetic, ultra-clean`

---

### Template — Prompt Seedance 2.0

```
[0–Xs]: [movimento inicial — câmera, luz, elementos da cena]
[Xs–Ys]: [continuação ou segundo shot]
[Ys–fim]: [encerramento estático para loop seamless]

Camera: [locked / slow push-in / orbit / drift]
Style: cinematic, [paleta], ambient [adjetivo], photorealistic
```

O último segundo deve ter movimento mínimo para o loop boomerang funcionar.

---

## 1. ABSOLUTE ZERO — ANTI-PATTERNS (falha imediata se presente)

- **Fontes banidas:** Inter, Roboto, Arial, Open Sans, Helvetica
- **Ícones banidos:** Lucide padrão, FontAwesome, Material Icons — usar só Phosphor Light ou Remix Line
- **Bordas/sombras banidas:** `1px solid gray` genérico, `box-shadow rgba(0,0,0,0.3)` duro
- **Layouts banidos:** navbar edge-to-edge colada no topo, grid 3-colunas simétricas Bootstrap
- **Motion banido:** `linear`, `ease-in-out`, mudanças de estado sem interpolação

---

## 2. CREATIVE VARIANCE ENGINE

Antes de escrever código, escolha silenciosamente **1 Vibe + 1 Layout**:

### Vibes
1. **Ethereal Glass** (Tech / SaaS / IA) — fundo OLED `#050505`, mesh gradients com orbs glowing, backdrop-blur-2xl, tipografia Grotesk larga
2. **Editorial Luxury** (Lifestyle / Imobiliária / Carros / Agência) — espresso `#0a0806` ou creme `#FDFBF7`, Variable Serif (DM Serif Display) para headlines, noise/grain, acento dourado
3. **Soft Structuralism** (Saúde / Portfólio / Consumer) — fundo branco ou cinza-prata, Grotesk bold massivo, sombras ambientes suaves e difusas

### Layouts
1. **Asymmetrical Bento** — CSS Grid com cards de tamanhos variados (`1.5fr 1fr 1fr`), nunca 3 iguais em linha. Mobile: `grid-cols-1`, gap generoso.
2. **Z-Axis Cascade** — cards fisicamente empilhados com rotações (`-2deg`, `3deg`, `2.5deg`) para profundidade real. Mobile: remover rotações abaixo de 768px.
3. **Editorial Split** — tipografia massiva na esquerda (55%), conteúdo interativo na direita (45%). Mobile: stack vertical completo.

**Universal Mobile Override:** abaixo de 768px → `w-full`, `px-4`, `py-8`. Nunca `h-screen` — sempre `min-h-[100dvh]`.

---

## 3. HAPTIC MICRO-AESTHETICS

### Double-Bezel (Doppelrand) — obrigatório em todos os cards
Nunca colocar card direto no fundo. Sempre dois níveis aninhados:

```css
.db  {
  background: var(--s1);
  border-radius: 2rem;
  padding: 6px;
  border: 1px solid rgba(255,255,255,0.06);
}
.dbi {
  background: var(--s2);
  border-radius: calc(2rem - 6px);
  padding: 24px;
  box-shadow: inset 0 1px 1px rgba(255,255,255,0.08),
              inset 0 -1px 0 rgba(0,0,0,0.3);
}
```

### Button-in-Button — obrigatório no CTA principal
O ícone/seta nunca fica solto ao lado do texto. Deve estar dentro de um círculo aninhado:

```html
<a class="btn-pill" href="#">
  Texto do botão
  <span class="bi">→</span>
</a>
```
```css
.btn-pill { display: inline-flex; align-items: center; gap: 10px; padding: 10px 10px 10px 20px; border-radius: 100px; }
.bi { width: 28px; height: 28px; border-radius: 50%; background: rgba(0,0,0,0.18); display: flex; align-items: center; justify-content: center; transition: transform 0.55s cubic-bezier(0.32,0.72,0,1); }
.btn-pill:hover .bi { transform: translateX(2px) translateY(-1px) scale(1.1); }
```

### Floating Pill Nav — obrigatório
```css
.nav {
  position: fixed; top: 20px; left: 50%; transform: translateX(-50%);
  z-index: 200;
  padding: 10px 10px 10px 28px;
  background: rgba(10,8,6,0.9);
  backdrop-filter: blur(24px);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 100px;
  white-space: nowrap;
}
```

### Eyebrow Tags
```html
<span class="eyebrow">Categoria · Contexto</span>
```
```css
.eyebrow { font-size: .6rem; letter-spacing: .2em; text-transform: uppercase; border-radius: 100px; padding: 5px 14px; border: 1px solid; display: inline-block; margin-bottom: 20px; }
```

### Whitespace
Padding de seção mínimo: `py-24` a `py-40`. O layout precisa respirar pesado.

---

## 4. MOTION CHOREOGRAPHY

### Transição padrão — nunca `ease`
```css
--ease: cubic-bezier(0.32, 0.72, 0, 1);
```

### Scroll reveal com blur (obrigatório)
```css
.sr {
  opacity: 0;
  transform: translateY(56px);
  filter: blur(12px);
  transition: opacity .85s var(--ease), transform .85s var(--ease), filter .65s var(--ease);
}
.sr.in { opacity: 1; transform: translateY(0); filter: blur(0); }
```
```javascript
(function() {
  var els = document.querySelectorAll('.sr');
  var fb = setTimeout(function(){ els.forEach(function(el){ el.classList.add('in'); }); }, 1500);
  if (!('IntersectionObserver' in window)) { els.forEach(function(el){ el.classList.add('in'); }); clearTimeout(fb); return; }
  var io = new IntersectionObserver(function(entries) {
    entries.forEach(function(e) { if (e.isIntersecting) { e.target.classList.add('in'); io.unobserve(e.target); } });
  }, { threshold: 0.05, rootMargin: '0px 0px 80px 0px' });
  els.forEach(function(el){ io.observe(el); });
})();
```

### Hamburger → X morph (mobile menu)
As 2–3 linhas do hamburger devem girar fluidamente para formar um X com `rotate-45` / `-rotate-45`.
O menu abre como overlay com `backdrop-blur(32px)`. Links aparecem com stagger (`delay-100`, `delay-150`, `delay-200`).

### Magnetic buttons
```javascript
document.querySelectorAll('.btn-pill').forEach(function(btn) {
  btn.addEventListener('mousemove', function(e) {
    var r = btn.getBoundingClientRect();
    var x = (e.clientX - r.left - r.width/2) * 0.15;
    var y = (e.clientY - r.top - r.height/2) * 0.15;
    btn.style.transform = 'translate('+x+'px,'+y+'px)';
    btn.style.transition = 'transform 0.1s linear';
  });
  btn.addEventListener('mouseleave', function() {
    btn.style.transform = 'translate(0,0)';
    btn.style.transition = 'transform 0.55s cubic-bezier(0.32,0.72,0,1)';
  });
});
```

---

## 5. PERFORMANCE

- Nunca animar `top`, `left`, `width`, `height` — só `transform` e `opacity`
- `backdrop-blur` apenas em elementos fixed/sticky (nav, overlays) — nunca em containers scrolláveis
- Grain/noise em `position: fixed; inset: 0; pointer-events: none` — nunca em containers que scrollam
- `will-change: transform` apenas em elementos ativamente animando

---

## 6. HERO VIDEO (quando houver vídeo)

```html
<section class="hero">
  <video id="heroVid" class="hvid" autoplay muted playsinline preload="auto">
    <source src="[caminho do vídeo]" type="video/mp4">
  </video>
  <div class="hovl"></div>
  <div class="hgrid"></div>
  <div class="hero-content sr">
    <span class="eyebrow">Categoria · Marca</span>
    <h1>Headline <em>impactante</em><br>aqui</h1>
    <p class="lead">Subheadline curta. Foca na transformação.</p>
    <a href="#contato" class="btn-pill">Reserve agora <span class="bi">→</span></a>
  </div>
</section>
```

```css
.hero { position: relative; min-height: 100dvh; display: flex; align-items: center; overflow: hidden; }
.hvid { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover; z-index: 0; opacity: 0.62; }
.hovl {
  position: absolute; inset: 0; z-index: 1; pointer-events: none;
  background: linear-gradient(to bottom, rgba(10,8,6,.35) 0%, rgba(10,8,6,.08) 40%, rgba(10,8,6,.08) 60%, rgba(10,8,6,.92) 100%),
              linear-gradient(to right, rgba(10,8,6,.35) 0%, transparent 25%, transparent 75%, rgba(10,8,6,.35) 100%);
}
.hgrid {
  position: absolute; inset: 0; z-index: 1; pointer-events: none;
  background-image: linear-gradient(rgba(255,255,255,.02) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(255,255,255,.02) 1px, transparent 1px);
  background-size: 48px 48px;
}
.hero-content { position: relative; z-index: 2; padding: 128px 24px 80px; text-align: center; }
```

### Loop boomerang (JS)
```javascript
(function() {
  var v = document.getElementById('heroVid');
  if (!v) return;
  var LOOP_START = 8;   // ajustar conforme o vídeo
  var LOOP_END   = 11.9;
  function back() { v.currentTime = LOOP_START; v.play(); }
  v.addEventListener('timeupdate', function() { if (v.currentTime >= LOOP_END) back(); });
  v.addEventListener('ended', back);
})();
```

---

## 7. GRAIN TEXTURE (Editorial Luxury — sempre)

```css
body::after {
  content: '';
  position: fixed; inset: 0; z-index: 9998;
  pointer-events: none; opacity: 0.032;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
```

---

## 8. PRE-OUTPUT CHECKLIST

Antes de entregar, verificar:
- [ ] Nenhuma fonte/ícone/border/shadow/layout/motion do Absolute Zero
- [ ] Vibe + Layout do Variance Engine foram escolhidos e aplicados
- [ ] Todos os cards usam Double-Bezel (outer shell + inner core)
- [ ] CTA usa Button-in-Button com círculo aninhado
- [ ] Nav é floating pill — nunca edge-to-edge
- [ ] Padding de seção mínimo `py-24`
- [ ] Todas as transições usam `cubic-bezier(0.32,0.72,0,1)` — zero `ease`/`linear`
- [ ] Scroll reveals com blur presentes
- [ ] Layout colapsa para `w-full` + `px-4` abaixo de 768px
- [ ] `backdrop-blur` só em fixed/sticky
- [ ] Impressão geral: agência $150k, não template com fonte bonita
