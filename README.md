# Bugs de Fernando Nahopa — Blog

Blog pessoal hospedado no GitHub Pages com Jekyll.

---

## ESTRUTURA DO PROJECTO

```
blog-nahopa/
├── _config.yml          ← configurações do site
├── _layouts/
│   ├── default.html     ← layout base (navbar, sidebar, footer)
│   └── post.html        ← layout de post individual
├── _includes/
│   └── sidebar.html     ← sidebar lateral
├── _posts/              ← OS TEUS POSTS VÃO AQUI
│   └── YYYY-MM-DD-titulo-do-post.md
├── assets/
│   ├── css/main.css     ← todo o design
│   └── js/main.js       ← relógio do status bar
├── index.html           ← página principal
├── arquivo.html         ← arquivo de posts
├── sobre.html           ← página sobre
└── Gemfile              ← dependências Ruby/Jekyll
```

---

## PASSO 1 — CRIAR REPOSITÓRIO NO GITHUB

1. Vai a **github.com** e cria uma conta se ainda não tens
2. Clica em **New repository**
3. Nome do repositório: `blog-nahopa` (ou qualquer nome)
4. Deixa como **Public**
5. **NÃO** inicializes com README
6. Clica em **Create repository**

---

## PASSO 2 — INSTALAR GIT (se ainda não tens)

**Windows:** https://git-scm.com/download/win  
**Mac:** `brew install git` no terminal  
**Linux:** `sudo apt install git`

Depois configura:
```bash
git config --global user.name "Fernando Nahopa"
git config --global user.email "teu@email.com"
```

---

## PASSO 3 — COLOCAR OS FICHEIROS NO GITHUB

Abre o terminal na pasta `blog-nahopa` e corre:

```bash
git init
git add .
git commit -m "primeiro commit — blog nahopa"
git branch -M main
git remote add origin https://github.com/SEU-USERNAME/blog-nahopa.git
git push -u origin main
```

⚠️ Substitui `SEU-USERNAME` pelo teu username do GitHub.

---

## PASSO 4 — ACTIVAR O GITHUB PAGES

1. No repositório do GitHub, vai a **Settings**
2. No menu lateral clica em **Pages**
3. Em "Source" selecciona **GitHub Actions**
4. Cria o ficheiro `.github/workflows/jekyll.yml` com este conteúdo:

```yaml
name: Deploy Jekyll
on:
  push:
    branches: [main]
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.2'
          bundler-cache: true
      - run: bundle exec jekyll build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: _site
      - uses: actions/deploy-pages@v4
```

5. Depois de fazer push, o site fica disponível em:  
   `https://SEU-USERNAME.github.io/blog-nahopa`

---

## PASSO 5 — CONFIGURAR O OBSIDIAN

### Instalar Obsidian
Vai a **obsidian.md** e descarrega.

### Apontar o Vault para a pasta _posts
1. Abre o Obsidian
2. **Open folder as vault**
3. Selecciona a pasta `blog-nahopa/_posts`

### Criar posts no Obsidian
Cada ficheiro `.md` que criares na pasta `_posts` é um post.  
O nome do ficheiro **TEM** de seguir este formato:

```
YYYY-MM-DD-titulo-do-post.md
```

Exemplo: `2025-03-01-a-internet-esta-chata.md`

### Cabeçalho obrigatório (Front Matter)
No início de cada post, coloca sempre isto:

```yaml
---
layout: post
title: "O título do teu post"
date: 2025-03-01
categories: [Filosofia]
read_time: "5 min"
excerpt: "Uma frase curta que aparece na lista de posts."
---

O teu texto começa aqui...
```

### Categorias disponíveis (podes criar novas)
- Filosofia
- Críticas
- Tecnologia
- Design
- Pessoal
- Sociedade
- Música
- Cinema

---

## PASSO 6 — PUBLICAR UM POST NOVO

Depois de escrever um post no Obsidian, abre o terminal e corre:

```bash
cd blog-nahopa
git add .
git commit -m "novo post: titulo do post"
git push
```

O GitHub detecta a mudança, reconstrói o site, e em 1-2 minutos o post já está online.

---

## MARKDOWN — REFERÊNCIA RÁPIDA

```markdown
# Título grande
## Subtítulo
### Sub-subtítulo

Parágrafo normal. Basta escrever.

**negrito**  
*itálico*

> Citação aparece como blockquote com fundo bege

- lista
- de itens

1. lista
2. numerada

[texto do link](https://url.com)
![imagem](caminho/imagem.jpg)

`código inline`

\`\`\`
bloco de código
\`\`\`
```

---

## DÚVIDAS FREQUENTES

**Como actualizo o texto da página Sobre?**  
Edita o ficheiro `sobre.html` directamente.

**Como mudo o nome do blog?**  
Edita o `_config.yml`, linha `title:`.

**Como adiciono o meu domínio próprio?**  
Em Settings → Pages → Custom domain, mete o teu domínio. Depois cria um ficheiro `CNAME` na raiz com o domínio dentro.

**Posso pré-visualizar localmente antes de publicar?**  
Sim. Instala Ruby e corre `bundle install` e depois `bundle exec jekyll serve`. O site fica em `localhost:4000`.
"# blog-nahopa"  
