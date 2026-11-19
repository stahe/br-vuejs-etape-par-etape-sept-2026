# Introdução passo a passo ao framework Vue.js

📖 **Leia o tutorial: [https://stahe.github.io/br-vuejs-etape-par-etape-sept-2026/](https://stahe.github.io/br-vuejs-etape-par-etape-sept-2026/)**

Este curso ensina como construir uma aplicação web usando o framework [Vue.js](https://vuejs.org) 3: uma **aplicação de página única** (SPA), em que as páginas são renderizadas **no navegador** a partir de dados JSON fornecidos por um servidor.

Ele dá continuidade ao curso [Introdução passo a passo ao framework web NestJS](https://stahe.github.io/br-nestjs-html-sept-2026/), oferecendo uma perspectiva diferente:

| Curso NestJS | Curso Vue.js |
|---|---|
| o servidor renderiza as páginas HTML (Handlebars) | o navegador renderiza as páginas (Vue.js) |
| o navegador exibe o que recebe | o servidor retorna apenas JSON |
| controllers, views, `res.render` | componentes `.vue`, roteador, stores |
| dicionários lidos pelo servidor | dicionários no cliente (vue-i18n); o servidor retorna apenas chaves |
| mensagem flash em um cookie | mensagem flash em um store Pinia |

As páginas em si permanecem inalteradas: são as mesmas da aplicação **RdvMedecins** já apresentada com os outros frameworks.

## A abordagem: muitos exemplos curtos, depois um estudo de caso

O curso é estruturado em torno de **20 exemplos curtos**, cada um focado em um único conceito. Eles compartilham um único comando `npm install` e um único servidor de desenvolvimento (Vite), que exibe o sumário deles.

| Capítulo | Conteúdo | Exemplos |
|---|---|---|
| Primeiros passos | um projeto Vite, `ref` / `reactive` / `computed` / `watch`, diretivas, eventos, formulários, validação | 01–06 |
| Componentes | props, eventos, `v-model` em um componente, slots, ciclo de vida, composables, `provide` / `inject`, diálogo de confirmação | 07–12 |
| Roteamento | vue-router, parâmetros, query, navigation guards, carregamento tardio (lazy loading) | 13–14 |
| Estado compartilhado | stores Pinia, `localStorage` | 15 |
| Internacionalização | vue-i18n: configurações, plurais, datas, números | 16 |
| O servidor: uma caixa-preta | Instalação do servidor JSON, sua API, 48 exemplos com `curl` | – |
| Comunicação com o servidor | `fetch`, proxy do Vite, cookie `httpOnly`, camada de acesso à API, erros do servidor | 17–20 |

Cada exemplo é apresentado com seu código completo, comentado linha por linha, e uma captura de tela de sua execução.

## O servidor: uma caixa-preta

O servidor é o servidor NestJS da lição anterior, cujos controllers agora retornam **JSON**. Esta lição o trata como uma **caixa-preta**: nós o configuramos, estudamos sua API e o consultamos com `curl`—mas não precisamos ler seu código (que é fornecido e comentado para os curiosos).

- Todos os erros têm o mesmo formato: `{ "statusCode": 409, "cle": "ERRORS.LOGIN_TAKEN", "params": {...}, "champs": {...} }` — **chaves** para tradução, nunca texto simples;
- Autenticação por meio de um token JWT em um cookie `httpOnly` / `sameSite=strict`: o JavaScript do lado do cliente nunca vê o token;
- Proteção CSRF: cookie `sameSite`, e todas as requisições POST devem ser em JSON;
- Um “modo de teste” para o CAPTCHA, para que você possa consultar a API com `curl`.

## O estudo de caso: o cliente Vue.js do RdvMedecins

Uma aplicação completa para **agendamento de consultas em um consultório médico**, com **todos** os seus arquivos (cerca de quarenta) listados e comentados.

- **Três papéis**: `ADMIN` (gerencia médicos e clientes), `DOCTOR` (agenda e cancela consultas), `USER` (o paciente: reserva consultas para si mesmo, gerencia sua conta).
- **Privacidade**: um paciente nunca recebe os nomes de outros pacientes—o servidor não os envia.
- **Todo o estado da página na URL**: `/agenda?idMedecin=1&jour=2026-10-05&reserver=7` reabre a janela de reserva após pressionar F5; os botões Anterior/Próximo funcionam.
- **Validação no servidor**: os formulários exibem, abaixo de cada campo, os erros retornados pela API; bloqueio otimista, nomes duplicados, nome de usuário já utilizado, etc.
- **Sessão**: restaurada após pressionar F5 (`GET /api/auth/moi`), expiração gerenciada em um único local (resposta 401).
- **Francês / inglês**, janela de confirmação acessível pelo teclado, Bootstrap 5.
- **Implantação**: o cliente compilado é servido pelo próprio servidor JSON (mesma origem, sem CORS).

## Tecnologias

Vue.js 3.5 (Composition API, `<script setup>`) · TypeScript 5.9 · Vite 7 · vue-router 4 · Pinia 3 · vue-i18n 11 · Bootstrap 5 · no servidor: NestJS 10 · TypeORM · MySQL 8 / MariaDB · Passport JWT · svg-captcha

## Pré-requisitos

- Um conhecimento básico de JavaScript (ou TypeScript), HTML e do protocolo HTTP.
- Node.js 22 (ou pelo menos 20.19), Visual Studio Code com a extensão Vue (Official) e um servidor MySQL (por exemplo, Laragon no Windows) para o servidor JSON. As instruções de instalação são fornecidas nos apêndices do curso.

## Autor

Este curso, seus exemplos, o servidor JSON e o estudo de caso foram escritos por **Claude**, a IA da [Anthropic](https://www.anthropic.com) (setembro de 2026), a pedido de **Serge Tahé**.
