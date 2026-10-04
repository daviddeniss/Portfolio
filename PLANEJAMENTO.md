# Planejamento — Melhorias do Portfólio

> Documento de planejamento. Nada aqui foi aplicado ainda: revise, responda às
> [perguntas restantes](#8-perguntas-restantes) e depois executamos fase por fase.

---

## 1. Objetivo

Transformar o portfólio de um template com textos de exemplo em uma vitrine para vagas de
**Engenheiro de Software Júnior** ou **Cientista de Dados Júnior**:

1. Mostrar **projetos de verdade** na seção Projetos (Crypto Dashboard, Emergy Analysis e EcoGrid).
2. Corrigir **bugs** que hoje quebram ícones, fontes e formulários.
3. Remover todo **conteúdo placeholder** e todo link que não leva a lugar nenhum.
4. Deixar o site **mais leve, acessível e encontrável** (imagens otimizadas, `alt`, SEO).
5. Publicar no **GitHub Pages**.

---

## 2. Decisões tomadas

| Pergunta | Resposta | Consequência no plano |
|----------|----------|-----------------------|
| Demos online | Os projetos estão só no GitHub; o portfólio vai para o GitHub Pages | Cards com botão **"Código"** (GitHub). Sem botão "Demo". |
| Público-alvo | Emprego: Eng. de Software Júnior / Cientista de Dados | Remover a seção **Orçamento**; criar **Sobre mim**; reorganizar Conhecimentos para mostrar back-end + dados. |
| Mais projetos | Usar o que houver em `C:\David Denis\Java` e `\Python` | Adicionado o **EcoGrid Management** (Java/Spring Boot). |
| Links sem destino | Remover | Sai Instagram, Twitter, Facebook, Google+, Pinterest e a newsletter. Ficam GitHub e LinkedIn. |

---

## 3. Diagnóstico do estado atual

### 3.1 Bugs (quebram algo hoje)

| # | Onde | Problema | Efeito |
|---|------|----------|--------|
| B1 | `assets/css/proprieties.css` | Os `@import` (Google Fonts e Font Awesome) vêm **depois** da regra `:root`. Pelo padrão CSS, `@import` fora do topo é ignorado. | Ícones (`fa-github`, `fa-python`...) e fontes podem não carregar. |
| B2 | `index.html` | `id="Close-menu"` repetido 6 vezes (hambúrguer + 5 links do menu). | HTML inválido; o JS funciona por acaso com `querySelectorAll("#...")`. |
| B3 | `index.html` | `id="email"` repetido (form de contato e footer). | O `<label for="email">` aponta para o campo errado. |
| B4 | `index.html` | `<div class="conhecimentos">` e `<div class="budget-wrapper">` não são fechados. | Layout depende da correção automática do navegador. |
| B5 | Contato | Formulário sem `action`, botão com `type="send"` (inválido). | Mensagens não são enviadas para lugar nenhum. |
| B6 | Footer | Form "Subscribe" faz `POST` para a própria página. | Recarrega a página e não faz nada. |

> Os bugs do Orçamento (`label for="layout-não"`, preço `NaN`) deixam de importar porque a seção será removida.

### 3.2 Conteúdo placeholder

- Modal do "Saiba mais" do banner: `Lorem ipsum...`
- 3 cards de projeto: `projeto1/2/3`, `HTML, CSS`, `Lorem ipsum`.
- Footer: parágrafo `Lorem ipsum` e 5 ícones de redes sociais com `href=""`.
- Instagram na sidebar: `https://www.instagram.com/seu-usuario`.
- README cita Webpack, Figma e "formulário funcional com validação", que não existem no projeto.

### 3.3 Desempenho

Imagens muito pesadas para a web (~7 MB no total):

| Arquivo | Tamanho | Uso |
|---------|---------|-----|
| `media/proj1.jpg` | 2,3 MB | card (vai ser substituída) |
| `assets/images/code.jpg` | 2,0 MB | fundo do banner |
| `media/proj4.jpg` | 1,7 MB | não usada |
| `assets/images/backgroundimg.jpg` | 1,1 MB | verificar |
| `media/proj3.jpg` | 0,6 MB | card (vai ser substituída) |

### 3.4 Acessibilidade e SEO

- Todas as `<img>` com `alt=""`.
- Sem `<meta name="description">` nem tags Open Graph (o link fica sem prévia no LinkedIn/WhatsApp).
- `<title>` genérico: "Portfólio".
- Elementos com `data-anime` ficam com `opacity: 0`: sem JS, ou antes do primeiro scroll, a seção some.
- Menu hambúrguer é uma `div` (não acessível por teclado) e não tem `aria-label`.
- Sem `prefers-reduced-motion` para quem desativa animações.

---

## 4. Seção Projetos — conteúdo proposto

Ordem sugerida: o projeto de dados primeiro (diferencial para as duas vagas), depois o
front-end e por fim o back-end Java.

### 4.1 Emergy Analysis — Iniciação Científica

- **Repositório:** https://github.com/daviddeniss/Emergy-Analysis-Pipeline
- **Imagem:** diagrama em `C:\David Denis\2D\Emergy 2.png` (ou `Emegy 3.png`).
  ⚠️ O diagrama mostra a arquitetura **antiga** (`pipeline/run_pipeline.py`, `models/models.py`),
  anterior à refatoração em 3 pacotes. Ver P2.
- **Tags:** Python · pandas · Streamlit · Plotly · SQLAlchemy · Pydantic · pytest · Docker
- **Selo:** `Pesquisa científica`
- **Descrição curta (card):**
  > Ferramenta científica de avaliação emergética: calcula a emergia de cada fluxo, os
  > totais R/N/F e os índices de sustentabilidade (EYR, ELR, EIR, ESI), com CLI e app web.
- **Destaques (modal "Saiba mais"):**
  - Monorepo com 3 pacotes (uv workspace): biblioteca, CLI e app web
  - `emergy-core`: núcleo científico reutilizável com pandas, Pydantic e SQLAlchemy
  - CLI `emergy` com Typer + Rich; app interativo em Streamlit + Plotly
  - Mesmo núcleo para CLI e web → resultados reprodutíveis
  - Lê inventários CSV/XLSX e converte UEVs entre baselines (GEB2016, GEB2000...)
  - Testes com pytest e Hypothesis, CI, pre-commit e Docker

### 4.2 Crypto Dashboard

- **Repositório:** https://github.com/daviddeniss/Crypto-Dashboard
- **Imagem:** `Crypto-Dashboard/docs/screenshot-light.png` (e `screenshot-dark.png`)
- **Tags:** Vue 3 · TypeScript · Pinia · Chart.js · WebSocket · Vitest
- **Descrição curta (card):**
  > Dashboard de criptomoedas em tempo real, com preços via WebSocket da Binance,
  > gráficos históricos, favoritos e alertas de preço.
- **Destaques (modal "Saiba mais"):**
  - Top 100 moedas com busca, ordenação e filtro de favoritos
  - Preços ao vivo via WebSocket, assinando só as moedas visíveis
  - Gráficos de 24h a 1 ano com Chart.js
  - Alertas de preço com notificação do sistema
  - Tema claro/escuro, mobile first, acessibilidade (contraste AA)
  - Reconexão com backoff exponencial, cache com TTL
  - Testes com Vitest + MSW, CI no GitHub Actions

### 4.3 EcoGrid Management — APS UNIP

- **Repositório:** https://github.com/daviddeniss/EcoGrid-Management
- **Imagem:** `Java/APS - EcoGrid/docs/img/desktop-painel.png`
- **Tags:** Java 25 · Spring Boot · JPA · PostgreSQL · JavaFX · JUnit · Mockito
- **Selo:** `Projeto acadêmico`
- **Descrição curta (card):**
  > Plataforma de eficiência energética: uma API REST calcula a pegada de carbono (tCO₂e)
  > das empresas, audita o teto de emissões e sugere ações alinhadas à ISO 14001.
- **Destaques (modal "Saiba mais"):**
  - Arquitetura cliente-servidor: API Spring Boot + cliente desktop JavaFX
  - Camadas Controller → Service → Repository (Spring Data JPA)
  - H2 em desenvolvimento, PostgreSQL em produção só trocando a configuração
  - Chamadas assíncronas com `HttpClient` + `CompletableFuture` (a interface não trava)
  - Simulação de créditos de carbono e recomendações por fonte de emissão
  - 47 testes com JUnit, Mockito e MockMvc

### 4.4 Formato do card

```
┌──────────────────────────────────┐
│          [screenshot]            │
├──────────────────────────────────┤
│ Emergy Analysis  [Pesquisa]      │  ← selo opcional
│ [Python] [pandas] [Streamlit] …  │  ← tags em "chips"
│ Ferramenta científica de ...     │
│                                  │
│ [ </> Código ]   [ Saiba mais ]  │  ← GitHub + modal de detalhes
└──────────────────────────────────┘
```

- Cards escritos **direto no HTML** (simples, bom para SEO, sem dependência de JS).
- "Código" abre o GitHub em nova aba (`target="_blank" rel="noopener"`).
- "Saiba mais" abre um modal com os destaques, reaproveitando o modal que já existe.
- Imagens copiadas para `media/` com nomes claros (`emergy.webp`, `crypto-dashboard.webp`,
  `ecogrid.webp`), convertidas para WebP e com `loading="lazy"`.

---

## 5. Outras seções

### 5.1 Banner
- Subtítulo: trocar "Desenvolvedor Full-Stack" por algo alinhado às vagas, ex.:
  **"Engenharia de Software · Ciência de Dados"**.
- Botão "Saiba mais" passa a rolar até a seção **Sobre mim** (em vez de abrir o modal com Lorem ipsum).
- Adicionar botão **"Baixar currículo"** se houver um PDF (ver P3).

### 5.2 Sobre mim (nova, no lugar de Orçamento)
- 1–2 parágrafos: formação, Iniciação Científica, interesse em back-end e dados.
- Rascunho será proposto por mim com base nos projetos (ver P4).

### 5.3 Conhecimentos (reorganizada em grupos)

| Grupo | Tecnologias |
|-------|-------------|
| Linguagens | Python · Java · TypeScript · JavaScript · SQL |
| Back-end | Spring Boot · JPA · REST APIs · SQLAlchemy · Pydantic |
| Dados | pandas · Plotly · Streamlit · Jupyter |
| Front-end | Vue 3 · Pinia · HTML · CSS |
| Qualidade e DevOps | pytest · JUnit · Vitest · Docker · GitHub Actions · Git |

> React sai, a não ser que você queira manter (não há projeto React nos repositórios).

### 5.4 Menu
`home · sobre · conhecimentos · projetos · contato`

### 5.5 Contato
Trocar o formulário (que não envia nada) por um bloco simples e que **funciona sem servidor**:
e-mail (`mailto:`), LinkedIn e GitHub. Opcionalmente, integrar o formulário com Formspree depois.

### 5.6 Footer
Nome, ano, links do GitHub e LinkedIn, e "Feito com HTML, CSS e JavaScript". Sem newsletter.

---

## 6. Plano de execução

### Fase 1 — Correções e limpeza
- [x] B1: mover os `@import` para o topo de `proprieties.css`
- [x] B2/B3: trocar ids repetidos por classes (`.js-toggle-menu`)
- [x] B4: fechar as `div`s abertas
- [x] Remover seção Orçamento (HTML, CSS e JS) e newsletter do footer
- [x] Remover links sem destino (Instagram, Twitter, Facebook, Google+, Pinterest) e seus ícones
- [x] Apagar imagens não usadas (`proj1-4.jpg`, ícones sociais, etc.)

### Fase 2 — Seção Projetos
- [x] Copiar e converter as 3 imagens para `media/` em WebP (Emergy usa o diagrama provisoriamente — P2)
- [x] Escrever os 3 cards com conteúdo real, tags, selo, botão "Código" e "Saiba mais"
- [x] Modal de detalhes por projeto
- [x] Ajustar o CSS dos cards (chips, botões, grid de 3 colunas → 1 no celular)

### Fase 3 — Conteúdo
- [x] Banner com novo subtítulo
- [x] Sobre mim (feito como modal do "Saiba mais" do banner)
- [ ] Conhecimentos em grupos
- [x] Contato e footer novos (e-mail, WhatsApp, LinkedIn, GitHub) + favicon "DD"
- [ ] Atualizar o README do portfólio (tirar Webpack/Figma, colocar o link do GitHub Pages)

### Fase 4 — Desempenho, acessibilidade e SEO
- [ ] Converter e redimensionar a imagem do banner (`code.jpg`, 2 MB)
- [ ] `alt` descritivo em todas as imagens
- [ ] `<title>`, `meta description` e Open Graph (com imagem de prévia)
- [ ] Hambúrguer como `<button>` com `aria-label` e `aria-expanded`
- [ ] Animação de scroll com `IntersectionObserver` + `prefers-reduced-motion`
- [ ] Conteúdo visível mesmo sem JS

### Fase 5 — Publicação no GitHub Pages
- [ ] Ativar em *Settings → Pages* (branch `main`, pasta `/`) → `https://daviddeniss.github.io/Portfolio/`
- [ ] Testar todos os links no site publicado
- [ ] Colocar o link no README, no LinkedIn e no perfil do GitHub
- [ ] Rodar o Lighthouse e anotar as notas antes/depois

---

## 7. Fora do escopo / riscos

- Sem migrar para framework e sem redesenho completo: mantemos a identidade atual
  (banner escuro, vermelho, JetBrains Mono).
- Corrigir B1 vai **fazer as fontes e ícones carregarem de verdade**: o visual pode mudar
  um pouco. Vale comparar antes/depois.
- Sugestões fora deste repositório (não serão feitas agora):
  - README do EcoGrid tem `git clone https://github.com/SEU-USUARIO/...` — trocar pelo link real.
  - Emergy: gerar um print da app Streamlit e colocar no README.
  - Fixar (pin) os 3 repositórios no seu perfil do GitHub.

---

## 8. Perguntas restantes

- **P1. Repositórios públicos:** os 3 repositórios (Emergy-Analysis-Pipeline, Crypto-Dashboard,
  EcoGrid-Management) já estão **públicos** no GitHub? Repositório privado = link quebrado para o recrutador.
- **P2. Imagem do Emergy:** usar o diagrama de arquitetura (desatualizado) ou você tira um print
  da aplicação Streamlit (`uv run emergy-web`)? Recomendo o **print** — mostra o produto funcionando.
- **P3. Currículo:** tem um PDF de currículo para o botão "Baixar currículo"?
- **P4. Sobre mim:** curso, instituição (UNIP?) e semestre/previsão de formatura. Posso escrever
  o rascunho a partir disso.
- **P5. E-mail de contato:** qual e-mail deve aparecer no site?
