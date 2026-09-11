# Plugins Kinbox

Marketplace da equipe Kinbox para distribuir plugins do Codex.

| Marketplace | Plugin | Versão | Servidor MCP |
| --- | --- | --- | --- |
| `kinbox-team` | `kinbox` | `0.1.0` | `https://mcp.kinbox.com.br/mcp` |

O plugin inicial conecta o Codex ao Kinbox para consultar e gerenciar contatos,
conversas e negócios. As ferramentas disponíveis dependem das permissões da
conexão. Esta versão contém a configuração MCP e os elementos de apresentação;
skills poderão ser adicionadas posteriormente.

## Instalar no Codex

É necessário ter o Codex CLI instalado. Este repositório é público, então a
instalação por HTTPS não exige autenticação no GitHub nem configuração de SSH.

Execute:

```bash
codex plugin marketplace add https://github.com/kinboxapp/kinbox-plugins.git
codex plugin add kinbox@kinbox-team
```

Também é possível usar o atalho `kinboxapp/kinbox-plugins` como origem do
marketplace. O acesso aos dados do Kinbox continua exigindo a conexão OAuth
descrita abaixo.

Depois da instalação:

1. Abra o plugin **Kinbox**, do marketplace **Kinbox Team**, no Codex.
2. Use a opção de conexão e conclua o login e a autorização no Kinbox pelo OAuth.
3. Abra uma nova tarefa para carregar as ferramentas.
4. Teste com: **Liste as etiquetas disponíveis no meu workspace Kinbox.**

Cada funcionário autoriza sua própria conexão. O repositório contém apenas a
URL pública do servidor e os arquivos do plugin, sem tokens ou credenciais.

Se já houver uma instalação de desenvolvimento em outro marketplace, use a
versão **Kinbox Team** neste teste para identificar claramente a origem.

## Importar para o workspace da empresa

Quando a administração de plugins estiver disponível no workspace:

1. Acesse **Admin → Plugins → Add → Import marketplace**.
2. Informe **Source**: `https://github.com/kinboxapp/kinbox-plugins`.
3. Deixe **Path** vazio, pois o marketplace está na raiz do repositório.
4. Informe **Branch**: `main`.
5. Autorize o acesso ao repositório no GitHub e conclua a importação.
6. Disponibilize o plugin para os funcionários ou papéis que participarão do teste.

A importação não conecta automaticamente as contas Kinbox dos funcionários.
Plugins importados com `.mcp.json`, como este, são classificados como
**Desktop only** nesse fluxo.

## Atualizações

Para atualizar uma instalação feita pelo CLI após novas versões serem publicadas:

```bash
codex plugin marketplace upgrade kinbox-team
codex plugin add kinbox@kinbox-team
```

Abra uma nova tarefa depois de atualizar. Na distribuição pelo workspace,
use **Admin → Plugins → Marketplaces → Sync now** ou aguarde a sincronização
automática diária.

## Estrutura

```text
.agents/plugins/marketplace.json
plugins/kinbox/
├── .codex-plugin/plugin.json
├── .mcp.json
└── assets/icon.png
```

O caminho `./plugins/kinbox` no catálogo é relativo à raiz deste repositório.
O servidor continua hospedado pelo Kinbox; instalar o plugin não exige executar
um backend local. O MCP anuncia descoberta OAuth, registro dinâmico de clientes
e PKCE S256, permitindo a conexão sem incluir um client ID fixo no pacote.

## Referências

- [Instalação e uso de plugins](https://learn.chatgpt.com/docs/plugins)
- [Importação e sincronização de marketplaces pelo GitHub](https://learn.chatgpt.com/docs/enterprise/plugin-management)
- [MCP e OAuth no Codex](https://learn.chatgpt.com/docs/extend/mcp?surface=cli)
