# Seriema · site institucional

Site de página única, **estático**. Sem build, sem framework, sem dependência de servidor.
Todo o CSS está embutido no `index.html`, o logotipo é um SVG em `data:` URI e não há
JavaScript executável — o único `<script>` do arquivo é o bloco `application/ld+json`
de dados estruturados, que o navegador não roda.

## Conteúdo da pasta

| Arquivo | Para que serve |
|---|---|
| `index.html` | A página inteira. É o único arquivo obrigatório. |
| `og.png` | Imagem 1200×630 do preview no WhatsApp, LinkedIn, Slack e X. |
| `favicon.ico` | Ícone da aba (16/32/48/64 px no mesmo arquivo). |
| `apple-touch-icon.png` | Ícone ao salvar na tela inicial do iPhone (180 px). |
| `icone-192.png`, `icone-512.png` | Ícones do manifesto (Android, PWA). |
| `site.webmanifest` | Nome, cores e ícones do site. |
| `robots.txt`, `sitemap.xml` | Indexação pelo Google. |
| `vercel.json` | Cabeçalhos de segurança e política de cache. |

## Publicar na Vercel

**Opção A — arrastar e soltar (mais rápido)**

1. Entre em `vercel.com/new`.
2. Arraste **a pasta inteira** para a área de upload — não o `index.html` sozinho,
   senão os ícones e o `og.png` ficam de fora.
3. Framework Preset: **Other**. Build Command e Output Directory: deixe em branco.
4. Deploy.

**Opção B — pela linha de comando**

```bash
npm i -g vercel
cd <esta-pasta>
vercel --prod
```

## Ligar o domínio

1. No projeto da Vercel: **Settings → Domains → Add**, e cadastre
   `seriemaapp.com.br` **e** `www.seriemaapp.com.br`.
2. A Vercel mostra o valor do CNAME — é único por projeto, no formato
   `<hash>.vercel-dns-0NN.com`. Copie o valor que **ela** exibir.
3. Publique os registros no seu DNS conforme o documento **Zona DNS do Seriema**:
   apex em `A → 76.76.21.21`, `www` e `app` em CNAME para o valor do passo 2.
4. Deixe `seriemaapp.com.br` como domínio principal e `www` redirecionando para ele
   (a Vercel faz isso sozinha ao marcar o apex como *Primary*).

O certificado HTTPS é emitido pela Vercel automaticamente, em alguns minutos após
o DNS propagar.

## Depois de publicar — três conferências

1. **Preview do link**: cole `https://seriemaapp.com.br` numa conversa do WhatsApp
   e veja se aparece a imagem escura com a manchete. Se não aparecer, use o
   *Sharing Debugger* do Facebook para forçar a releitura do cache.
2. **Botão do WhatsApp**: abra pelo celular e confirme que cai na conversa com a
   mensagem já escrita, no número **+55 11 98834-6666**.
3. **Tema escuro**: a página se adapta ao tema do sistema de quem visita.
   Teste nos dois modos.

## Alterar o conteúdo depois

Os pontos que mais mudam ficam fáceis de achar no `index.html`:

- **Telefone e e-mail**: procure por `wa.me/5511988346666` e por
  `contato@seriemaapp.com.br`. Aparecem nos botões do topo, do herói,
  da seção de preço e nos cartões de contato.
- **Preços**: procure por `R$ 690,00`. A tabela de planos e o valor da
  implantação estão logo ali, na seção `id="preco"`.
- **Cores da marca**: as variáveis no topo do `<style>` (`--azul`, `--tinta`,
  `--chao`) valem para a página inteira. Cada uma é redeclarada no bloco do
  tema escuro — se mudar uma, mude nos dois lugares.

Depois de editar, é só refazer o deploy: a Vercel mantém a mesma URL.

## Se o e-mail ainda não existir

O endereço `contato@seriemaapp.com.br` precisa estar criado no Zoho antes
de o site ir ao ar — caso contrário o botão de e-mail leva a uma caixa que não
recebe. Os registros MX, SPF, DKIM e DMARC estão no documento **Zona DNS do Seriema**.
