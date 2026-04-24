# Guia de Configuração — Sincronização via Google Sheets

Tempo estimado: 10–15 minutos. Feito uma vez, funciona para sempre.

---

## PASSO 1 — Criar a planilha Google

1. Acesse **sheets.google.com** com a conta Google compartilhada entre vocês dois
2. Clique em **+ Em branco** para criar uma nova planilha
3. Dê um nome para ela, por exemplo: `Diário de Humor`
4. Deixe a aba aberta — você vai precisar dela no Passo 2

---

## PASSO 2 — Criar o Apps Script

1. Dentro da planilha, clique no menu **Extensões → Apps Script**
   - Uma nova aba vai abrir com o editor de código
2. Apague todo o código que aparecer na tela (geralmente tem uma função vazia)
3. Abra o arquivo **apps-script.gs** que veio junto com este guia
4. Copie **todo o conteúdo** do arquivo apps-script.gs
5. Cole no editor do Apps Script
6. Clique no ícone de **disquete** (💾) ou pressione Ctrl+S para salvar
7. Dê um nome ao projeto se pedir, por exemplo: `DiarioHumor`

---

## PASSO 3 — Publicar como Web App

1. No editor do Apps Script, clique em **Implantar → Nova implantação**
2. Clique no ícone de engrenagem ⚙ ao lado de "Selecionar tipo" e escolha **App da Web**
3. Preencha os campos:
   - **Descrição**: `Diário de Humor v1` (qualquer nome)
   - **Executar como**: `Eu (seu e-mail)`
   - **Quem tem acesso**: `Qualquer pessoa`
     ⚠ Isso é necessário para o formulário acessar sem login
4. Clique em **Implantar**
5. Na primeira vez, vai pedir para **autorizar o acesso** — clique em "Autorizar acesso", escolha a conta Google compartilhada e clique em "Permitir"
6. Após a autorização, vai aparecer uma tela com a **URL do app da Web**
   - Ela tem formato: `https://script.google.com/macros/s/XXXXXX.../exec`
7. **Copie essa URL** — você vai precisar dela no Passo 4

---

## PASSO 4 — Colar a URL no formulário HTML

1. Abra o arquivo **controle-humor-v2.html** em qualquer editor de texto
   - No Windows: clique direito → Abrir com → Bloco de Notas
   - No Mac: clique direito → Abrir com → Editor de Texto
2. Use Ctrl+F (ou Cmd+F no Mac) para buscar o texto:
   ```
   COLE_A_URL_DO_APPS_SCRIPT_AQUI
   ```
3. Substitua exatamente esse trecho pela URL que você copiou no Passo 3
   - Antes: `const SCRIPT_URL = 'COLE_A_URL_DO_APPS_SCRIPT_AQUI';`
   - Depois: `const SCRIPT_URL = 'https://script.google.com/macros/s/XXXXX/exec';`
4. Salve o arquivo

---

## PASSO 5 — Subir o arquivo atualizado no GitHub

1. Acesse seu repositório no GitHub
2. Clique no arquivo **controle-humor-v2.html**
3. Clique no ícone de lápis ✏ para editar
4. Apague todo o conteúdo e cole o novo arquivo atualizado
   - **OU** faça o upload do arquivo direto pelo GitHub: clique em "Add file → Upload files"
5. Clique em **Commit changes**
6. Aguarde 1–2 minutos e acesse o link do GitHub Pages — a sincronização já estará ativa

---

## Como funciona a partir daí

- Quando **ela** salva um registro no celular dela → vai para a planilha Google
- Quando **você** abre o formulário no seu celular → clica em "↻ Sincronizar" na tela de comparação → os registros dela aparecem
- E vice-versa
- A planilha funciona como banco de dados central — vocês dois podem ver ela direto no Google Sheets também

---

## Verificando se está funcionando

1. Abra o formulário, preencha um registro e salve
2. Acesse a planilha Google Sheets
3. A aba **registros** deve ter uma nova linha com os dados
4. Se aparecer, está funcionando ✓

---

## Problemas comuns

**"Erro ao sincronizar — salvo localmente"**
- Verifique se a URL foi colada corretamente no HTML (sem espaços extras)
- Verifique se o acesso da Web App está como "Qualquer pessoa"
- Tente republicar o Apps Script: Implantar → Gerenciar implantações → editar → nova versão

**Os dados aparecem na planilha mas não carregam no formulário**
- Clique em "↻ Sincronizar" na tela de comparação
- Verifique se a aba da planilha se chama exatamente `registros` (minúsculo)

**Pediu para fazer login ao acessar o formulário**
- O Apps Script foi publicado com acesso restrito. Repita o Passo 3 e escolha "Qualquer pessoa" em "Quem tem acesso"

---

## Segurança e privacidade

- Os dados ficam em uma planilha Google privada, na conta de vocês
- A URL do Apps Script funciona como uma "senha" — não compartilhe com outras pessoas
- Nenhum dado passa por servidores de terceiros além do Google
- A planilha pode ser excluída a qualquer momento para apagar todos os dados
