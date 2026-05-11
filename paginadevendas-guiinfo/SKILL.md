---
name: paginadevendas-guiinfo
description: Cria páginas de vendas HTML premium para infoprodutos e produtos digitais — cursos, mentorias, comunidades, ferramentas digitais, qualquer produto que se venda online. USE sempre que pedirem uma página de vendas de infoproduto, curso, mentoria ou produto digital, independente da marca ou nicho. Pergunta sobre paleta/estilo, módulos/aulas, hero video (start+end frame), depoimentos, preço e urgência. Orquestra geração de imagens no Higgsfield (pede aprovação por imagem), entrega HTML completo com carrossel de módulos, depoimentos 3D perspective wall, bloco de preço com "O que está incluído" e todos os efeitos premium (hero gradient, 3D tilt, magnetic buttons). Sempre entrega prompt Seedance após end frame aprovado.
---

# Página de Vendas — Infoprodutos

Skill para criar landing pages de alta conversão para cursos, mentorias e produtos digitais.
Orquestra conteúdo → visual → imagens → HTML final. Adapta paleta e tipografia a cada produto.

---

## Processo Obrigatório (seguir nesta ordem)

### FASE 1 — Coleta de informações

Faça estas perguntas **uma por vez**, espere a resposta antes de avançar:

**1. Produto**
- Nome do produto/curso
- Promessa principal (resultado em 1 frase)
- Público-alvo
- Preço (à vista e parcelado)

**0. Visual (perguntar antes de tudo)**
"Qual o estilo visual que você quer? Tem uma cor de marca? (ex: roxo, dourado, verde, azul) — ou quer sugestão baseada no nicho do produto?"
Com base na resposta, defina `--accent` e adapte o design system. Padrão sugerido se não houver preferência: roxo `#7C3AED` + azul `#3B82F6` (tech/IA) ou dourado `#c9a84c` (luxo/premium) ou verde `#10b981` (saúde/negócios).

**2. Prova social numérica**
"Quais são os números reais que você tem? Ex: faturamento, alunos, contratos fechados, resultado gerado pros clientes."
(Esses viram os `.stat` no hero)

**3. Módulos e aulas**
"Esse produto tem módulos? Se sim, quantos e quais são os nomes?"
Se sim, para cada módulo: "Quais são as aulas do módulo X? (pode ser só os títulos)"

**4. Hero video**
"Qual é a ideia do vídeo da Hero? Pensa na cena final: onde você está, o que está na sua mão, que sensação passa?"

Com base no que ele disser, sugira **3 opções de start + end frame**:
- Start frame sempre = ambiente vazio/neutro antes da pessoa entrar
- End frame = cena climática com o professor + símbolos do produto

Formato de apresentação:
```
Opção 1 — "Nome da opção"
Start: [descreve a cena vazia]
End: [descreve a cena final com o professor]

Opção 2 — ...
Opção 3 — ...
```

**5. Depoimentos**
"Você tem depoimentos dos alunos? Manda: nome, @handle, cidade e o texto de cada um. Mínimo 9 pra preencher bem o grid 3D."

**6. Urgência**
"Vai ter vagas limitadas, janela de tempo ou outra urgência?"
(ex: "50 vagas · 72h de janela · 10 módulos")

**7. O que está incluído**
"Lista o que vem no produto: módulos, bônus, contratos, templates, comunidade, suporte. Cada item em 1 linha."

**8. Quem ensina**
"Me dá uma bio curta do professor — nome, 2-3 credenciais reais e o que fez de resultado."

---

### FASE 2 — Geração de imagens no Higgsfield

Após coletar tudo, gere imagens (NÃO vídeos) no Higgsfield:

**A. Hero background**
```
dark home office setup, single desk against wall, purple and blue LED rim lighting, MacBook open with code on screen, ultra-realistic, cinematic, 8K, no person
```

**B. Thumbnail por módulo** (se tiver módulos)
Para cada módulo, gere com GPT Image 2. Prompt base:
```
[tema do módulo], dark background, glowing [cor do módulo], 3D icon, minimal, premium, 8K
```

**Para cada imagem gerada:**
- Mostre o resultado e pergunte: "Essa ficou boa pra [nome do módulo/hero]?"
- Se não aprovada: ajuste o prompt e regenere
- Só avance após aprovação

**C. End frame do hero video**
- Use GPT Image 2 com referência do rosto do Gui (media_id: `c7e28c8b-ba71-49bf-af5c-3a860f564a22`)
- Baseie no end frame escolhido na Fase 1
- Após aprovação, entregue o prompt Seedance completo (ver template abaixo)

---

### FASE 3 — Geração do HTML

Salve em `paginas-vendas/{nome-produto-slug}/index.html`.

Link para shared: `../shared/styles.css` e `../shared/scripts.js`

---

## Design System

### Tokens CSS

O fundo é sempre escuro (`#08080a`). O que muda é `--accent` e `--accent-2` conforme a cor definida na Fase 0.
Adapte também `--accent-light`, `--accent-dark`, `--accent-glow` proporcionalmente.

```css
:root {
  --bg:           #08080a;
  --surface:      #111114;
  --surface-2:    #18181c;
  --border:       #1c1c20;
  --border-strong:#2a2a32;
  --text:         #f5f5f7;
  --text-muted:   #a1a1aa;
  --text-subtle:  #52525b;
  --accent:       [cor definida na Fase 0];   /* ex: #7C3AED roxo, #c9a84c ouro, #10b981 verde */
  --accent-2:     [cor complementar];
  --accent-light: [versão clara do accent];
  --accent-dark:  [versão escura do accent];
  --accent-glow:  rgba([R,G,B do accent], 0.4);
  --radius:       12px;
  --radius-lg:    20px;
}
```

### Tipografia
- **H1, H2:** Clash Display 600/700 via `https://api.fontshare.com/v2/css?f[]=clash-display@600,700&display=swap` — `letter-spacing: -0.02em`
- **Body, UI:** Inter (Google Fonts)
- **Números/métricas:** JetBrains Mono
- Nunca: Playfair, DM Sans, Roboto

### Efeitos premium (obrigatórios)
Sempre incluir no `<style>`:
```css
h1, h2 { font-family: 'Clash Display', 'Inter', sans-serif; letter-spacing: -0.02em; }

.hero::after {
  content: ''; position: absolute; inset: 0;
  background: radial-gradient(500px circle at var(--mx,50%) var(--my,50%), rgba(124,58,237,0.14) 0%, transparent 60%);
  pointer-events: none; z-index: 0; opacity: 0; transition: opacity 0.4s;
}
.hero.cursor-active::after { opacity: 1; }

.stat, .problem-card, .step, .testimonial, .t3d-card, .curriculum-card {
  will-change: transform;
  transition: transform 0.18s ease-out;
}
.btn-primary {
  transition: transform 0.35s cubic-bezier(0.25,0.46,0.45,0.94) !important;
}
```

Sempre incluir antes de `</body>`:
```javascript
(function() {
  var isDesktop = window.matchMedia('(hover: hover) and (pointer: fine)').matches;
  var hero = document.querySelector('.hero');
  if (hero && isDesktop) {
    hero.addEventListener('mousemove', function(e) {
      var r = hero.getBoundingClientRect();
      hero.style.setProperty('--mx', ((e.clientX-r.left)/r.width*100).toFixed(1)+'%');
      hero.style.setProperty('--my', ((e.clientY-r.top)/r.height*100).toFixed(1)+'%');
      hero.classList.add('cursor-active');
    });
    hero.addEventListener('mouseleave', function(){ hero.classList.remove('cursor-active'); });
  }
  if (isDesktop) {
    document.querySelectorAll('.stat,.problem-card,.step,.t3d-card,.curriculum-card').forEach(function(el) {
      el.addEventListener('mousemove', function(e) {
        var r=el.getBoundingClientRect(),dx=(e.clientX-(r.left+r.width/2))/(r.width/2),dy=(e.clientY-(r.top+r.height/2))/(r.height/2);
        el.style.transform='perspective(600px) rotateX('+(-dy*7)+'deg) rotateY('+(dx*7)+'deg) scale(1.02)';
      });
      el.addEventListener('mouseleave', function(){ el.style.transform=''; });
    });
    document.querySelectorAll('.btn-primary').forEach(function(btn) {
      btn.addEventListener('mousemove', function(e) {
        var r=btn.getBoundingClientRect(),dx=(e.clientX-(r.left+r.width/2))/(r.width/2),dy=(e.clientY-(r.top+r.height/2))/(r.height/2);
        btn.style.transform='translate('+(dx*7)+'px,'+(dy*4)+'px)';
      });
      btn.addEventListener('mouseleave', function(){ btn.style.transform=''; });
    });
  }
})();
```

---

## Estrutura de Seções (ordem padrão)

### 1. TOPBAR
Countdown com `data-countdown`.

### 2. HERO
Grid de pontos, eyebrow, H1 com `.text-gradient`, lead text, CTA `.btn-primary.btn-pulse.btn-large`, trust badges.
Se tiver imagem de hero gerada: `<img>` à direita no split (desktop) / overlay (mobile).
Se tiver vídeo: `<video autoplay muted loop playsinline poster="[img-hero]">`.

### 3. STATS
4 `.stat` com `.stat-num` (JetBrains Mono) e `.stat-label`.

### 4. PROBLEMA
4–6 `.problem-card` com as dores do público.

### 5. MECANISMO
Seção explicando a abordagem única. Include caixa de destaque mostrando os 3 pilares: CRIAR → VENDER → RETER (ou equivalente do produto).

### 6. CURRICULUM (se tiver módulos)
Carrossel horizontal com JS de auto-scroll + loop por clonagem + dots.

Estrutura HTML:
```html
<div class="curriculum-outer">
  <button class="curriculum-arrow" id="cvPrev">←</button>
  <div class="curriculum-track" id="cvTrack">
    <!-- .curriculum-card por módulo -->
  </div>
  <button class="curriculum-arrow" id="cvNext">→</button>
</div>
<div class="curriculum-dots" id="cvDots"></div>
```

Cada card:
```html
<div class="curriculum-card">
  <img src="[imagem aprovada]" alt="Módulo X" loading="lazy">
  <div class="curriculum-card-body">
    <span class="curriculum-num">MÓDULO 01</span>
    <h4>Nome do módulo</h4>
    <p>1 linha de descrição</p>
    <ul class="curriculum-lessons">
      <li>Aula 01 — título</li>
    </ul>
  </div>
</div>
```

JS do carrossel (copiar padrão da página `agente-atendimento/index.html`):
- Clone dos cards originais para loop sem salto
- `setInterval` de 3200ms
- Pause on hover / touch
- Dots atualizados no scroll

### 7. ENTREGÁVEIS
`.stack` com `.stack-item` (check + texto + valor riscado).

### 8. DEPOIMENTOS — 3D PERSPECTIVE WALL

CSS:
```css
.testimonials-3d-wrap {
  overflow: hidden; perspective: 1400px;
  padding: 24px 0 64px;
  mask-image: linear-gradient(to bottom, transparent 0%, black 12%, black 88%, transparent 100%),
              linear-gradient(to right, transparent 0%, black 8%, black 92%, transparent 100%);
  mask-composite: intersect;
  -webkit-mask-image: linear-gradient(to bottom, transparent 0%, black 12%, black 88%, transparent 100%),
                      linear-gradient(to right, transparent 0%, black 8%, black 92%, transparent 100%);
  -webkit-mask-composite: destination-in;
  margin-top: 48px;
}
.testimonials-3d-grid {
  display: grid; grid-template-columns: repeat(3, 1fr);
  gap: 14px; max-width: 980px; margin: 0 auto;
  transform: rotateX(20deg) rotateY(-5deg) scale(0.92);
  transform-origin: center 30%; transform-style: preserve-3d;
  padding: 0 16px;
}
.t3d-card {
  background: var(--surface); border: 1px solid var(--border-strong);
  border-radius: 14px; padding: 18px 20px;
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
.t3d-name { font-weight: 700; font-size: 0.85rem; line-height: 1.2; }
.t3d-handle { font-size: 0.72rem; color: var(--text-subtle); }
.t3d-city { font-size: 0.7rem; color: var(--text-subtle); display: flex; align-items: center; gap: 3px; margin-top: 1px; }
.t3d-text { font-size: 0.84rem; line-height: 1.6; color: var(--text-muted); }
.t3d-result {
  display: inline-block; margin-top: 10px; font-size: 0.72rem; font-weight: 700;
  color: var(--accent-light); background: rgba(124,58,237,0.12);
  padding: 3px 10px; border-radius: 20px;
}
@media (max-width: 768px) {
  .testimonials-3d-grid { grid-template-columns: 1fr; transform: none; max-width: 420px; }
  .testimonials-3d-wrap { perspective: none; mask-image: linear-gradient(to bottom, transparent 0%, black 5%, black 95%, transparent 100%); -webkit-mask-image: linear-gradient(to bottom, transparent 0%, black 5%, black 95%, transparent 100%); }
}
```

HTML de cada card:
```html
<div class="t3d-card">
  <div class="t3d-header">
    <div class="t3d-avatar">AB</div>
    <div>
      <div class="t3d-name">Nome Sobrenome</div>
      <div class="t3d-handle">@handle</div>
      <div class="t3d-city">🇧🇷 Cidade · Estado</div>
    </div>
  </div>
  <p class="t3d-text">"Depoimento aqui."</p>
  <span class="t3d-result">Resultado destacado</span>
</div>
```

Avatar = iniciais. NUNCA usar fotos de rosto.

### 9. QUEM ENSINA
Split com foto (se disponível) + bio + credenciais.

### 10. PREÇO — Bloco de Oferta

```html
<section id="oferta">
  <div class="container container-narrow">
    <div class="offer-block reveal">
      <div class="offer-stats">
        <div class="offer-stat">
          <div class="offer-stat-num">[N]</div>
          <div class="offer-stat-label">VAGAS</div>
        </div>
        <div class="offer-stat">
          <div class="offer-stat-num">[N]H</div>
          <div class="offer-stat-label">JANELA</div>
        </div>
        <div class="offer-stat">
          <div class="offer-stat-num">[N]</div>
          <div class="offer-stat-label">MÓDULOS</div>
        </div>
      </div>
      <div class="offer-price-wrap">
        <p class="offer-de">DE <s>R$[PREÇO ORIGINAL]</s> POR</p>
        <div class="offer-price">
          <span class="offer-currency">R$</span>
          <span class="offer-value">[PREÇO]</span>
          <span class="offer-dot">.</span>
        </div>
        <p class="offer-parcelas">ou 12x R$[PARCELA] · pagamento único</p>
      </div>
      <a href="[LINK]" class="btn btn-primary btn-pulse btn-large offer-cta">
        GARANTIR MINHA VAGA · R$[PREÇO]
      </a>
      <p class="offer-urgency">DEPOIS DAS [N]H OU APÓS PREENCHER [N] VAGAS: <strong>R$[PREÇO CHEIO]</strong> SEM BÔNUS DE FUNDADOR</p>
      <div class="offer-includes">
        <h4 class="offer-includes-title">O QUE TÁ INCLUÍDO</h4>
        <ul class="offer-includes-list">
          <!-- <li> por item fornecido na Fase 1 -->
        </ul>
      </div>
    </div>
  </div>
</section>
```

CSS:
```css
.offer-block { background: var(--surface); border: 1px solid var(--border-strong); border-radius: var(--radius-lg); padding: 48px 40px; }
.offer-stats { display: flex; gap: 40px; justify-content: center; margin-bottom: 32px; }
.offer-stat-num { font-family: 'JetBrains Mono', monospace; font-size: 2.5rem; font-weight: 700; color: var(--accent-light); line-height: 1; }
.offer-stat-label { font-size: 0.72rem; letter-spacing: 0.1em; color: var(--text-subtle); margin-top: 4px; }
.offer-de { font-size: 0.85rem; color: var(--text-subtle); margin-bottom: 8px; }
.offer-price { display: flex; align-items: flex-start; line-height: 1; margin-bottom: 8px; }
.offer-currency { font-family: 'JetBrains Mono', monospace; font-size: 1.8rem; color: var(--text-muted); padding-top: 12px; }
.offer-value { font-family: 'Clash Display', sans-serif; font-size: 6rem; font-weight: 700; color: var(--text); }
.offer-dot { font-family: 'JetBrains Mono', monospace; font-size: 4rem; color: var(--accent); align-self: flex-end; padding-bottom: 8px; }
.offer-parcelas { font-size: 0.9rem; color: var(--text-muted); }
.offer-cta { width: 100%; text-align: center; margin: 24px 0 16px; font-size: 1rem; letter-spacing: 0.06em; }
.offer-urgency { font-size: 0.72rem; letter-spacing: 0.06em; color: var(--text-subtle); text-align: center; margin-bottom: 32px; }
.offer-includes-title { font-size: 0.8rem; letter-spacing: 0.1em; color: var(--accent-light); text-transform: uppercase; margin-bottom: 16px; padding-top: 24px; border-top: 1px solid var(--border); }
.offer-includes-list { list-style: none; padding: 0; display: flex; flex-direction: column; gap: 12px; }
.offer-includes-list li { display: flex; gap: 12px; align-items: flex-start; font-size: 0.92rem; color: var(--text-muted); }
.offer-includes-list li::before { content: '*'; color: var(--accent-light); font-weight: 700; flex-shrink: 0; }
```

### 11. AUDIÊNCIA
Split em 2 colunas: "É pra você se" (✅) e "Não é pra você se" (❌).

### 12. FAQ
`.faq-item` com `<details><summary>` — mínimo 5 perguntas.

### 13. CTA FINAL
Background com gradient roxo sutil + headline + CTA + garantia.

### 14. FOOTER
Logo + tagline + @handle + contato + legal.

---

## Template Seedance (entregar após end frame aprovado)

```
[0s-3s]
Camera: static wide shot
Scene: [start frame — ambiente vazio, sem pessoa]
Lighting: [luz fria/neutra]
Mood: expectation, empty space

[3s-7s]
Camera: slow push in
Scene: [professor entra, senta, câmera acompanha]
Action: smooth transition from empty to occupied
Lighting: [luzes do produto começam a aparecer — roxo/laranja]

[7s-10s]
Camera: hold, slight drift left
Scene: [end frame completo]
Action: symbols materialize from light particles — [símbolo 1] on right hand, [símbolo 2] on left, [símbolo 3] above head
Lighting: warm orange and deep purple rim light
Mood: mastery, control, power
Style: photorealistic, cinematic, 8K
```

---

## Checklist antes de entregar

- [ ] Todas as imagens aprovadas antes de inserir no HTML
- [ ] Prompt Seedance entregue junto com o HTML
- [ ] Clash Display carregando (preconnect + link fontshare)
- [ ] Inter e JetBrains Mono carregando (Google Fonts)
- [ ] Carrossel de módulos: auto-scroll + loop + dots + pause on hover
- [ ] Depoimentos: grid 3D com mínimo 9 cards
- [ ] Bloco de preço: offer-stats + offer-price + offer-includes
- [ ] Efeitos premium no JS (hero gradient, 3D tilt, magnetic buttons)
- [ ] Mobile responsivo (grid colapsa, 3D desativa)
- [ ] Links `../shared/styles.css` e `../shared/scripts.js` corretos
- [ ] Zero fotos de rosto nos depoimentos (só iniciais)
