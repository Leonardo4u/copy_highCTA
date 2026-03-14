# Gerador de Campanhas - 5 Niveis de Consciencia

Aplicacao web estaticas em HTML, CSS e JavaScript para analisar uma landing page e gerar campanhas com base nos 5 niveis de consciencia do mercado.

O app le a URL informada, tenta extrair o conteudo com Jina Reader, usa IA via OpenRouter e Groq para estruturar a analise da pagina e monta copys por nivel de consciencia, incluindo historico local e exportacao para PDF.

## O que a aplicacao faz

- Analisa uma landing page a partir de uma URL.
- Extrai contexto da oferta, headline, CTAs, prova, objecoes e estrutura da copy.
- Gera campanhas para os 5 niveis de consciencia.
- Permite ajustar persona, dores, tom de voz, nicho e concorrentes.
- Faz fallback entre Groq e OpenRouter.
- Salva historico no navegador com localStorage.
- Exporta o resultado em formato de impressao/PDF.

## Stack

- HTML puro
- CSS puro
- JavaScript puro no navegador
- Jina Reader para leitura de pagina
- OpenRouter para inferencia
- Groq como opcional mais rapido, com fallback para OpenRouter
- Vercel para hospedagem estatica

## Estrutura do projeto

- [copy.html](copy.html): aplicacao completa, incluindo interface, estilos e logica.
- [vercel.json](vercel.json): rewrite da raiz para [copy.html](copy.html) na Vercel.
- [README.md](README.md): documentacao do projeto.

## Como rodar localmente

Como o projeto e estatico, voce pode abrir direto no navegador:

```powershell
Start-Process .\copy.html
```

Ou usar um servidor local no VS Code, por exemplo com Live Server.

## Como usar

1. Abra a aplicacao.
2. Clique em API Keys.
3. Informe uma chave do OpenRouter.
4. Opcionalmente informe uma chave do Groq.
5. Cole a URL da landing page que deseja analisar.
6. Se quiser, preencha configuracoes avancadas como persona, dores, concorrentes e tom de voz.
7. Clique em Analisar e Gerar.
8. Revise as abas dos niveis, a sugestao de nivel e a campanha final.
9. Exporte em PDF se quiser salvar o resultado.

## Chaves de API

### OpenRouter

- Obrigatoria.
- Usada como provedor principal ou fallback.
- O app tenta varios modelos gratuitos em sequencia.

### Groq

- Opcional.
- Quando configurada, o app tenta usar Groq primeiro.
- Se falhar, cai automaticamente para OpenRouter.

## Como funciona internamente

Fluxo principal da aplicacao:

1. O usuario informa a URL.
2. O app tenta ler o conteudo da pagina via Jina Reader.
3. A IA extrai dados estruturados da landing page.
4. O app monta contexto adicional com persona, dores, nicho e concorrentes.
5. Sao geradas campanhas para cada nivel de consciencia.
6. O sistema sintetiza uma campanha final.
7. O resultado e salvo no historico local.

## Persistencia de dados

Os dados ficam salvos no localStorage do navegador, incluindo:

- chave OpenRouter
- chave Groq
- historico de analises
- estados auxiliares da interface

Isso significa que os dados ficam no navegador atual, nao em um banco de dados.

## Deploy na Vercel

Este projeto pode ser publicado como site estatico.

### Arquivo importante

Como a pagina principal do projeto e [copy.html](copy.html) e nao index.html, o arquivo [vercel.json](vercel.json) faz o rewrite da rota raiz para esse arquivo.

### Passo a passo

1. Envie o projeto para um repositorio no GitHub.
2. Importe o repositorio na Vercel.
3. Mantenha a configuracao como projeto estatico.
4. Faça o deploy.

Se necessario, o deploy tambem pode funcionar sem build command e sem output directory customizado, porque o projeto e apenas um conjunto de arquivos estaticos.

## Limitacoes importantes

- As chaves de API sao usadas no front-end. Isso e pratico para uso pessoal, mas nao e a abordagem ideal para um produto publico multiusuario.
- Se Jina Reader nao conseguir ler a pagina, a analise pode ficar menos precisa.
- O app depende da resposta dos provedores de IA retornarem JSON valido.
- O historico fica apenas no navegador do usuario.

## Recomendacao para producao

Se voce quiser transformar isso em uma aplicacao publica de verdade, o proximo passo correto e mover as chamadas para OpenRouter e Groq para um backend ou serverless function. Assim voce protege as chaves e controla melhor custos, limites e abuso.

## Melhorias futuras

- Backend para proteger chaves
- Banco de dados para historico persistente
- Sistema de autenticacao
- Templates extras por canal de midia
- Comparativo entre versoes de copy
- Logs e monitoramento de falhas de API

## Licenca

Sem licenca definida no momento.