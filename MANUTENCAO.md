# Guia de manutenção

Tudo o que é preciso para continuar mantendo o site em outro computador.
Este repositório é **público**: nada de senhas, CPF, boletos ou telefones pessoais aqui.

## 1. Preparar um computador novo

1. Instalar o [Git para Windows](https://git-scm.com/download/win).
2. Clonar o repositório:
   ```
   git clone https://github.com/Linykercs/mfdobrasil.git
   cd mfdobrasil
   git config user.name "Linyker"
   git config user.email "204272230+Linykercs@users.noreply.github.com"
   ```
   No primeiro `git push` o Git abre o login do GitHub no navegador.
3. Copiar à mão a pasta **`_material-daniel/`** do computador antigo para dentro de `mfdobrasil/`
   (pendrive ou Google Drive). Ela **não vai para o GitHub** (está no `.gitignore`) porque tem
   o material bruto do cliente, boleto e documentos. Dentro dela está também o
   `CONTEXTO-PRIVADO.md`, com o histórico completo do projeto e as pendências com detalhes.
4. Se for usar o Claude Code: abra o Claude na pasta `mfdobrasil` e peça para ele ler este
   arquivo e o `_material-daniel/CONTEXTO-PRIVADO.md` antes de começar.

## 2. Estrutura

```
index.html          site inteiro (HTML + CSS + JS no mesmo arquivo, sem build)
daniel/index.html   cartão de visita digital do Daniel (mfdobrasil.com/daniel/)
img/                fotos (versões "-p" são as miniaturas leves)
video/              vídeos do site (só exporta-2 está em uso)
_material-daniel/   material privado, fora do Git
```

## 3. Como editar textos (3 idiomas)

- Todo texto traduzível tem um atributo `data-i="chave"` no HTML.
- As traduções ficam no fim do `index.html`, no objeto `var I = { pt: {...}, fr: {...}, en: {...} }`.
- **Ao mudar um texto, mude nos três dicionários** (`pt`, `fr`, `en`). O texto escrito direto no
  HTML é só o que aparece antes do JavaScript carregar; quem manda é o dicionário `pt`.
- `data-i-alt="chave"` faz o mesmo para o texto alternativo de imagens.
- Prefixos usados: `qs_*` Quem somos · `lg_*` O legado (Nossa história) · `ne_*`/`gi_*`/`gu_*` raças ·
  `st*` setores · `t1..t7` linha do tempo · `co*` cooperação · `ex*`/`pf*`/`g*` legendas de fotos.
- Textos longos usam "Ler mais": `<details class="leia">` com o resumo `rz_mais`/`rz_menos`.

## 4. Pré-visualizar localmente

Abrir o `index.html` direto no navegador já funciona. Para testar como no servidor, qualquer
servidor estático serve (ex.: `npx serve`, `python -m http.server`, ou a extensão Live Server do VS Code).

## 5. Publicar na Hostinger

1. Entrar no hPanel da Hostinger → site **mfdobrasil.com** → **Arquivos → Gerenciador de arquivos**
   → "Acessar arquivos de mfdobrasil.com".
2. Abrir a pasta `public_html`.
3. Clicar em **Upload** (seta para cima), escolher o(s) arquivo(s) alterado(s) e confirmar
   **"Replace all files in destination folder"**. Os caminhos devem espelhar o repositório
   (ex.: uma foto nova vai em `public_html/img/`).
4. Abrir https://mfdobrasil.com e conferir (Ctrl+F5 para ignorar o cache).
5. Depois de publicar, registrar no Git:
   ```
   git add -A
   git commit -m "Descrição da mudança"
   git push
   ```

A sessão do gerenciador de arquivos expira rápido; se der erro 403, reabra pelo hPanel.
Existe no servidor um `index-backup-2026-11-10.html` com a versão original, caso precise voltar.

## 6. Regras combinadas com o cliente

- **Faixa vermelha "Site em atualização"** (`<div class="obra">`, chave `obra`): manter até
  ~10/12/2026, depois remover a pedido.
- **Prévia de link (og:image)**: nunca usar foto com bandeiras de países específicos
  (o cliente não quer favorecer países). Hoje usa `img/poster.jpg`. A foto das bandeiras só
  pode ficar na galeria.
- Foto da vaca Girolando vem da Associação Brasileira dos Criadores de Girolando, com crédito
  na legenda (pedido do cliente).
- Setor "Educação e formação profissional" está com selo "Em atualização", sem conteúdo, até o
  cliente enviar o texto.

## 7. Pendências (dependem do cliente)

- Foto do Nelore; texto do Gir Leiteiro.
- Conteúdo do setor Educação e formação profissional.
- Legendas reais das fotos com autoridades.
- Cartão `/daniel`: cargo, retrato; avaliar QR apontando para a URL em vez do vCard.
- Conteúdo opcional de Avicultura.
- Remover a faixa "Site em atualização" por volta de 10/12/2026.

## 8. Serviços

- **Hospedagem, domínio e e-mails**: Hostinger (hPanel). E-mail corporativo Starter Business,
  4 caixas @mfdobrasil.com, ativo até 12/11/2027 com **renovação automática desligada**.
  Webmail: mail.hostinger.com · IMAP `imap.hostinger.com:993` SSL · SMTP `smtp.hostinger.com:465` SSL.
- **Código**: este repositório no GitHub (branch `main`).
