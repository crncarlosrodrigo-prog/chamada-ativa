# Chamada Ativa

Sistema mobile (PWA) de controle de presença e evolução para um programa de atividade física de idosas.
Projeto extensionista — Análise e Desenvolvimento de Sistemas, PUCPR.

## Funcionalidades
- **Chamada pelo celular**: por turma e data, com um toque (Presente / Faltou / Justificou + motivo). Botão "Todas presentes".
- **Regra de faltas automática**: conta as faltas sem justificativa e alerta quando a aluna chega ao limite (padrão 3, configurável). Também mostra quem está a 1 falta do limite.
- **Aviso no WhatsApp**: gera a mensagem personalizada para o celular cadastrado da aluna (um toque para enviar).
- **Lista de espera**: ao liberar uma vaga, o app mostra as próximas da fila (prioriza quem prefere a mesma turma).
- **Evolução de 1 a 5**: registro rápido do nível + anotações, com histórico por aluna.
- **Funciona sem internet** depois da primeira abertura; dados ficam só no celular; cópia de segurança em arquivo.

## Como publicar (gratuito, GitHub Pages)
1. Crie um repositório público no GitHub (ex.: `chamada-ativa`) e envie os 5 arquivos desta pasta.
2. No repositório: **Settings → Pages → Branch: main / (root) → Save**.
3. Em 1–2 minutos o app fica em `https://<seu-usuario>.github.io/chamada-ativa/`.

## Como instalar no celular da profissional
- **Android (Chrome)**: abrir o link → menu ⋮ → **Adicionar à tela inicial / Instalar app**.
- **iPhone (Safari)**: abrir o link → Compartilhar → **Adicionar à Tela de Início**.

## Primeiro uso
1. Aba **Mais** → cadastrar as turmas.
2. Aba **Alunas** → cadastrar cada aluna (marcar a autorização LGPD).
3. Pessoas da fila: cadastrar com situação **Lista de espera**.
4. Para demonstração/vídeo, use **Mais → Carregar dados fictícios** e depois **Apagar todos os dados**.

## Privacidade (LGPD)
- Coleta mínima: nome, celular, turma, presenças, nível e anotações.
- Nenhum dado é enviado a servidores: fica no armazenamento do navegador do aparelho.
- Fazer **cópia de segurança** semanal (Mais → Baixar cópia) e guardá-la em local protegido.
- A ficha da aluna permite excluir todos os dados dela a pedido.

## Limitação conhecida e evolução futura
O envio do aviso exige um toque da profissional (abre o WhatsApp com a mensagem pronta). O envio 100% automático
exigiria um servidor e a API oficial do WhatsApp Business (paga) ou um serviço de SMS, além de armazenar os dados
fora do celular — o que aumenta custo e risco à privacidade. Foi uma escolha consciente para esta versão.

## Estrutura
| Arquivo | Função |
| --- | --- |
| `index.html` | App completo (HTML, CSS e JavaScript, sem dependências) |
| `manifest.webmanifest` | Permite instalar como app |
| `sw.js` | Service worker (funcionamento offline) |
| `icon-192.png`, `icon-512.png` | Ícones |

Modelo de dados (localStorage, chave `chamada-ativa-v1`): `turmas[]`, `alunas[]` (status: ativa / espera / inativa,
`desde` = início da contagem de faltas), `chamadas{ "turmaId|AAAA-MM-DD": { alunaId: {s:'P'|'F'|'J', m:motivo} } }`,
`avaliacoes[]` (alunaId, data, nível 1–5, obs).
