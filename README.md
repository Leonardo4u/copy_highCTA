# Gerador de Campanhas - 5 Niveis de Consciencia

Aplicacao web estatica para analisar landing pages e gerar campanhas com base nos 5 niveis de consciencia do mercado. O projeto combina leitura automatica da pagina, analise estrutural por IA e geracao de copys orientadas por contexto, persona, dores e posicionamento da oferta.

## Visao geral

O usuario informa a URL de uma pagina de vendas e a aplicacao:

1. tenta extrair o conteudo da pagina via Jina Reader;
2. estrutura a oferta com apoio de IA;
3. gera campanhas para cada nivel de consciencia;
4. monta uma campanha final consolidada;
5. salva o resultado no navegador e permite exportacao em PDF.

## Principais recursos

- Analise de landing page a partir de URL.
- Extracao de headline, subheadline, CTAs, provas, bonus, objecoes e sinais de estrutura comercial.
- Geracao de copys para os 5 niveis de consciencia.
- Configuracoes avancadas para persona, dores, concorrentes, nicho e tom de voz.
- Uso opcional de Groq com fallback automatico para OpenRouter.
- Historico local com localStorage.
- Exportacao do resultado em formato de impressao/PDF.

## Stack

- HTML
- CSS
- JavaScript no navegador
- Jina Reader
- OpenRouter
- Groq
- Vercel

## Estrutura do projeto

- [copy.html](copy.html): interface, estilos e logica da aplicacao em um unico arquivo.
- [vercel.json](vercel.json): rewrite da rota raiz para [copy.html](copy.html) no deploy.
- [README.md](README.md): documentacao do projeto.

## Como executar localmente

Por ser um projeto estatico, voce pode abrir o arquivo direto no navegador:

```powershell
Start-Process .\copy.html
```

Se preferir, rode com um servidor local, como Live Server no VS Code.

## Como usar

1. Abra a aplicacao.
2. Clique em API Keys.
3. Configure ao menos uma chave do OpenRouter.
4. Opcionalmente configure uma chave do Groq.
5. Cole a URL da landing page.
6. Ajuste os campos avancados, se quiser refinar o contexto.
7. Clique em Analisar e Gerar.
8. Revise as campanhas por nivel, a recomendacao principal e a campanha final.
9. Exporte em PDF, se precisar compartilhar ou arquivar o material.

## Chaves de API

### OpenRouter

- Obrigatoria para o funcionamento do app.
- Serve como provedor principal ou fallback.
- O app tenta diferentes modelos gratuitos em sequencia.

### Groq

- Opcional.
- Quando presente, e usado antes do OpenRouter.
- Em caso de erro, a aplicacao volta automaticamente para OpenRouter.

## Fluxo da aplicacao

1. O usuario informa a URL da pagina.
2. O sistema tenta ler o conteudo com Jina Reader.
3. A IA retorna uma estrutura resumida da oferta.
4. O app combina esse contexto com persona, dores, tom e concorrentes.
5. Sao geradas campanhas para os 5 niveis de consciencia.
6. Uma campanha final e sintetizada a partir dos melhores elementos.
7. O resultado fica salvo no historico local.

## Persistencia

Os dados sao armazenados no localStorage do navegador. Isso inclui:

- chave OpenRouter
- chave Groq
- historico de analises
- preferencias da interface

Nao existe banco de dados nem sincronizacao entre dispositivos.

## Deploy na Vercel

O projeto pode ser publicado como site estatico sem etapa de build.

Como a entrada principal esta em [copy.html](copy.html), o arquivo [vercel.json](vercel.json) faz o rewrite da rota / para esse arquivo.

Passo a passo:

1. Envie o projeto para um repositorio no GitHub.
2. Importe o repositorio na Vercel.
3. Mantenha a configuracao como projeto estatico.
4. Publique o deploy.

## Limitacoes atuais

- As chaves de API ficam no front-end, o que e aceitavel para uso pessoal, mas nao ideal para uma aplicacao publica.
- Se o Jina Reader nao conseguir ler a pagina, a analise perde qualidade.
- A aplicacao depende de respostas de IA em JSON valido.
- O historico existe apenas no navegador em que foi gerado.

## Recomendacao para evolucao

Para transformar o projeto em uma aplicacao publica, o passo correto e mover as chamadas para OpenRouter e Groq para um backend ou funcao serverless. Isso protege as chaves, reduz risco de abuso e melhora o controle de custo e observabilidade.

## Melhorias futuras

- Backend para proteger credenciais
- Persistencia em banco de dados
- Autenticacao de usuarios
- Templates adicionais por canal de trafego
- Comparacao entre variacoes de copy
- Telemetria e logs de falhas de API

## Licenca

Sem licenca definida no momento.