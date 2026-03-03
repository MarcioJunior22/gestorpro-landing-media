# Mídia da landing page

Coloque aqui os vídeos e imagens usados na landing. O código referencia estes caminhos (servidos em `/landing/videos/` e `/landing/images/`).

**Se der 404** mesmo com os arquivos aqui: faça commit e push das imagens. Se no deploy (ex.: Vercel) ainda der 404, use a **mesma repo** via GitHub Raw (veja seção "Usar o próprio repositório (GitHub Raw)" no final deste README).

## Hero (opcional)

- **videos/hero-demo.mp4** – Vídeo de abertura
- **images/hero-dashboard.png** – Imagem do dashboard no hero

## Seção "O que o sistema faz" (7 blocos)

Use estes **nomes exatos** para os arquivos (em minúsculo, com hífen, sem acento):

| Nome na tela | Vídeo (`videos/`) | Imagem (`images/`) |
|--------------|-------------------|---------------------|
| Dashboard | dashboard.mp4 | dashboard.png |
| Painel Kanban pedidos | painel-kanban-pedidos.mp4 | painel-kanban-pedidos.png |
| Pedido continuação | pedido-continuacao.mp4 | pedido-continuacao.png |
| Pedido modelo | pedido-modelo.mp4 | pedido-modelo.png |
| Tela orçamento | tela-orcamento.mp4 | tela-orcamento.png |
| Tela pedido | tela-pedido.mp4 | tela-pedido.png |
| Telas geração de orçamento | telas-geracao-orcamento.mp4 | telas-geracao-orcamento.png |

Recomendação: **vídeos** curtos (15–45 s), sem áudio, MP4. **Imagens** em PNG, largura máxima ~1200–1600 px.

---

## Hosting externo (quando as imagens não sobem no repositório principal)

Se as imagens não forem commitadas (tamanho, .gitignore, etc.), você pode hospedá-las em um **repositório público no GitHub** ou no **Firebase Storage** e configurar variáveis de ambiente no Next.js.

### Opção 1: Repositório público no GitHub

1. Crie um repositório público (ex.: `meu-usuario/gestorpro-landing-media`).
2. Dentro dele, crie a pasta `landing` com as pastas `images/` e `videos/`.
3. Coloque os arquivos com os **nomes exatos** da tabela acima (ex.: `dashboard.png`, `hero-dashboard.png`, `painel-kanban-pedidos.png`).
4. No projeto Next.js (Vercel ou `.env.local`), defina:
   ```env
   NEXT_PUBLIC_LANDING_MEDIA_BASE_URL=https://raw.githubusercontent.com/MEU_USUARIO/MEU_REPO/main/landing
   ```
   Troque `MEU_USUARIO`, `MEU_REPO` e `main` (branch) conforme seu repositório.

As URLs finais serão: `BASE_URL/images/hero-dashboard.png`, etc.

### Opção 2: Firebase Storage

1. No Firebase Console, crie um bucket (ou use o existente) e ative acesso público de leitura para os arquivos da pasta `landing` (ou use regras que permitam leitura pública desses arquivos).
2. Crie a estrutura **landing/images/** e **landing/videos/** e faça upload dos arquivos com os nomes da tabela.
3. Copie a URL base do bucket (ex.: `https://firebasestorage.googleapis.com/v0/b/SEU_PROJECT.appspot.com/o`).
4. No projeto Next.js, defina:
   ```env
   NEXT_PUBLIC_LANDING_MEDIA_BASE_URL=https://firebasestorage.googleapis.com/v0/b/SEU_PROJECT.appspot.com/o
   NEXT_PUBLIC_LANDING_MEDIA_FIREBASE=true
   ```

O código monta automaticamente a URL no formato do Storage (`.../o/landing%2Fimages%2Farquivo.png?alt=media`).

---

### Usar o próprio repositório (GitHub Raw)

Se as imagens já estão neste repo mas dão 404 no deploy (ex.: Vercel não servindo `public/` direito), você pode carregá-las do **mesmo repositório** via GitHub Raw:

1. Certifique-se de que as imagens estão em `next-frontend/public/landing/images/` com os **nomes exatos** (ex.: `hero-dashboard.png`, `painel-kanban-pedidos.png`) e que fez **commit e push**.
2. No projeto (Vercel ou `.env.local`), defina:
   ```env
   NEXT_PUBLIC_LANDING_MEDIA_BASE_URL=https://raw.githubusercontent.com/MarcioJunior22/GestorproFinal/main/next-frontend/public/landing
   ```
   Troque `MarcioJunior22`, `GestorproFinal` e `main` pelo seu usuário, nome do repo e branch.
3. Faça um novo deploy. As imagens passarão a ser carregadas diretamente do GitHub (mesmo repo).
