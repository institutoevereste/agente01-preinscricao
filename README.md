# Pré-inscrição · Agente 01 · Evereste Academy

Página estática de pré-inscrição do curso Agente 01. Não tem etapa de build: é HTML, CSS e JavaScript em um arquivo.

## O que publicar

Endereço final: `https://evereste.org/academy-agente01/`

Copie o **conteúdo da pasta `academy/`** (o `index.html` e a pasta `img/`) para a pasta `academy-agente01/` do servidor do site. Os caminhos são relativos, então a página funciona em qualquer pasta.

As tags de prévia do link (`og:url` e `og:image`, no começo do `academy/index.html`) já apontam para o endereço final.

O `index.html` da raiz é a versão antiga da página (identidade do Instituto). Ela não vai para o domínio.

## Banco de dados

A página grava direto no Firestore pelo navegador, sem servidor. Funciona de qualquer domínio.

- Projeto Firebase: `agente01-preinscricao`, coleção `preinscricoes`.
- O id de cada documento é o telefone, então o mesmo número não entra duas vezes.
- Regras em `firestore.rules`: só permitem criar inscrição. Ninguém lê, altera ou apaga pelo navegador.
- Para publicar as regras: `npx -y firebase-tools@latest deploy --only firestore:rules --project agente01-preinscricao`

Para usar outro banco, troque as três variáveis no fim do `academy/index.html`:

| Variável | O que é |
|---|---|
| `BANCO` | Endereço REST da coleção no Firestore |
| `CHAVE` | Chave pública do app web do Firebase (não é segredo) |
| `PLANILHA` | URL `/exec` do Apps Script que copia a inscrição para a planilha e avisa por e-mail. Deixe vazio (`""`) para desligar |

Se trocar de projeto, publique o `firestore.rules` no projeto novo antes de divulgar a página.

## Campos enviados

`nome`, `whatsapp` (só dígitos, com DDD), `email`, `curso` (`"agente01"`) e `consentimento` (`true`, caixa da LGPD).

## Testar depois de publicar

1. Abrir a página no celular e no desktop.
2. Fazer uma inscrição com nome "TESTE" e conferir o documento no Firestore.
3. Repetir o mesmo telefone: a página deve avisar que o número já está inscrito.
4. Apagar o documento de teste no console do Firebase.
