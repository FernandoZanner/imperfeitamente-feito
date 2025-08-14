# Git Config

Documento de referência sobre as configurações do Git com foco especial no arquivo `.gitconfig` e na criação de `aliases`. 

---
> Este conteúdo é compartilhado de forma **imperfeita** e em construção. Sinta-se à vontade para explorar, comentar ou reutilizar com crédito.

# Menu Rápido

- [Configurações disponíveis para o arquivo .gitconfig](#configurações-disponíveis-para-o-arquivo-gitconfig)
- [Explicação das principais seções](#explicação-das-principais-seções)
- [Comandos via terminal para gerenciar o .gitconfig](#comandos-via-terminal-para-gerenciar-o-gitconfig)
    - [Configurações Globais e Locais](#configurações-globais-e-locais)
    - [Definir Nome de Usuário e Email](#definir-nome-de-usuário-e-email)
    - [Configurar o Editor Padrão](#configurar-o-editor-padrão)
    - [Configurar Aliases (Atalhos)](#configurar-aliases-atalhos)
    - [Configurar a Ferramenta de Merge e Diff](#configurar-a-ferramenta-de-merge-e-diff)
    - [Configurar Cache de Credenciais](#configurar-cache-de-credenciais)
    - [Configurar Coloração no Terminal](#configurar-coloração-no-terminal)
    - [Configurar Comportamento do Push](#configurar-comportamento-do-push)
    - [Configurar Arquivo .gitignore Global](#configurar-arquivo-gitignore-global)
    - [Visualizar Configurações](#visualizar-configurações)
    - [Editar o Arquivo .gitconfig Diretamente](#editar-o-arquivo-gitconfig-diretamente)
    - [Remover Configurações](#remover-configurações)
- [Comando git config](#comando-git-config)
    - [Localização do Arquivo de Configuração](#localização-do-arquivo-de-configuração)
    - [Ação](#ação)
    - [Tipo](#tipo)
    - [Outras Opções](#outras-opções)
- [Config Alias](#config-alias)
    - [O que são aliases no Git?](#o-que-são-aliases-no-git)
    - [Como configurar aliases no Git](#como-configurar-aliases-no-git)
    - [Exemplo de Adição de Aliases via Terminal](#exemplo-de-adição-de-aliases-via-terminal)
    - [Lista de aliases úteis com explicações](#lista-de-aliases-úteis-com-explicações)
        - [Aliases básicos](#aliases-básicos)
        - [Aliases para log e histórico](#aliases-para-log-e-histórico)
        - [Aliases para branches](#aliases-para-branches)
        - [Aliases para rebase e reset](#aliases-para-rebase-e-reset)
        - [Aliases para limpeza e otimização](#aliases-para-limpeza-e-otimização)
        - [Aliases para manipulação de arquivos](#aliases-para-manipulação-de-arquivos)
        - [Aliases para ferramentas externas e LFS](#aliases-para-ferramentas-externas-e-lfs)
        - [Aliases para operações com remotes](#aliases-para-operações-com-remotes)
        - [Aliases para pesquisa e exploração](#aliases-para-pesquisa-e-exploração)
        - [Aliases avançados](#aliases-avançados)
    - [Exemplos de Adição ao Seu .gitconfig](#exemplos-de-adição-ao-seu-gitconfig)
    - [Como usar os aliases](#como-usar-os-aliases)
    - [Dicas para criar seus próprios aliases](#dicas-para-criar-seus-próprios-aliases)
    - [Recursos adicionais](#recursos-adicionais)
    - [Conclusão](#conclusão)

# configurações disponíveis para o arquivo .gitconfig

O arquivo `.gitconfig` é utilizado para configurar as preferências globais ou locais do Git, como nome de usuário, editor padrão, aliases de comandos, e muito mais. Essas configurações podem ser feitas a nível global (para todo o sistema) ou local (para um repositório específico).

Aqui está um exemplo de como pode ser configurado um arquivo `.gitconfig` com explicações sobre cada seção:

```
[user]
    name = Seu Nome
    email = seu.email@exemplo.com
    signingkey = ABCD1234
    # Define o nome e email usados para as confirmações de commits.
    # O 'signingkey' é opcional e usado se você assina seus commits com uma chave GPG.

[core]
    editor = code --wait
    # Define o editor de texto padrão para quando precisar editar mensagens de commit, etc.
    # Aqui, está configurado para usar o Visual Studio Code.

[alias]
    co = checkout
    br = branch
    ci = commit
    st = status
    # Define aliases para comandos git, para que sejam mais curtos e fáceis de usar.
    # Exemplo: 'git co' vai funcionar como 'git checkout'.

[merge]
    tool = vimdiff
    # Define a ferramenta de merge para resolver conflitos.
    # 'vimdiff' é um exemplo, pode ser substituído por outras como 'meld', 'kdiff3', etc.

[diff]
    tool = vimdiff
    # Define a ferramenta para ver diferenças entre versões.
    # Também pode ser qualquer outra ferramenta suportada pelo Git.

[push]
    default = simple
    # Define o comportamento padrão para 'git push'.
    # 'simple' é recomendado para repositórios que seguem a prática de branch principal (master/main).

[commit]
    gpgSign = true
    # Se você assina seus commits com GPG, essa opção garante que todos os commits serão assinados por padrão.

[core]
    excludesfile = ~/.gitignore_global
    # Define um arquivo .gitignore global, onde você pode listar arquivos ou diretórios que devem ser ignorados em todos os seus repositórios.

[color]
    ui = auto
    # Ativa a coloração automática no terminal para facilitar a leitura dos comandos e saídas do Git.

[credential]
    helper = cache --timeout=3600
    # Define um helper de credenciais para que o Git armazene as credenciais em cache por um tempo específico (em segundos).
    # Neste exemplo, a cache é válida por 1 hora.

[log]
    decorate = true
    # Exibe informações adicionais no log, como tags e branches, tornando-o mais informativo.

[pull]
    rebase = false
    # Define se o comportamento padrão do 'git pull' deve ser 'merge' (padrão) ou 'rebase'.

```

### Explicação das principais seções:

1. **[user]**: Configura o nome de usuário e o e-mail que serão associados aos seus commits. Também pode incluir a chave GPG para assinar commits.
2. **[core]**: Define configurações principais do Git, como o editor padrão ou o arquivo `.gitignore` global.
3. **[alias]**: Permite criar atalhos para comandos do Git, facilitando e acelerando o trabalho com o Git.
4. **[merge]** e **[diff]**: Especifica as ferramentas para resolver conflitos de merge e para visualizar diferenças entre commits.
5. **[push]**: Configura o comportamento padrão do comando `git push`.
6. **[commit]**: Configurações relacionadas à criação de commits, como a assinatura com GPG.
7. **[color]**: Define se o Git deve utilizar cores na saída do terminal para tornar a visualização mais amigável.
8. **[credential]**: Define como o Git deve gerenciar as credenciais de acesso (por exemplo, cache temporário).
9. **[log]**: Ajusta a exibição de informações no log de commits.
10. **[pull]**: Define o comportamento do `git pull` (se deve fazer merge ou rebase).

Esses exemplos são comuns e podem ser adaptados conforme suas necessidades específicas. O arquivo `.gitconfig` pode ser editado manualmente ou usando comandos do Git (`git config`).

# comandos via terminal para gerenciar o .gitconfig

O Git permite que você gerencie as configurações do arquivo `.gitconfig` diretamente pelo terminal usando o comando `git config`. Aqui estão alguns exemplos de comandos comuns para configurar diferentes aspectos do seu `.gitconfig`:

### Configurações Globais e Locais

- **Global**: As configurações aplicam-se a todos os repositórios Git do usuário.
- **Local**: As configurações aplicam-se apenas ao repositório atual.

### Definir Nome de Usuário e Email

Essas são as configurações básicas que identificam o autor dos commits:

```bash
# Definir nome de usuário globalmente
git config --global user.name "Seu Nome"

# Definir email globalmente
git config --global user.email "seu.email@exemplo.com"

# Definir nome de usuário localmente (somente para o repositório atual)
git config user.name "Seu Nome"

# Definir email localmente (somente para o repositório atual)
git config user.email "seu.email@exemplo.com"

```

### Configurar o Editor Padrão

Você pode definir qual editor de texto será usado para editar mensagens de commit ou outros arquivos temporários:

```bash
# Configurar o editor globalmente
git config --global core.editor "code --wait"

# Configurar o editor localmente
git config core.editor "vim"

```

### Configurar Aliases (Atalhos)

Criar aliases (atalhos) para comandos comuns do Git pode economizar tempo:

```bash
# Alias global para 'git checkout'
git config --global alias.co checkout

# Alias global para 'git branch'
git config --global alias.br branch

# Alias global para 'git commit'
git config --global alias.ci commit

# Alias global para 'git status'
git config --global alias.st status

```

### Configurar a Ferramenta de Merge e Diff

Você pode definir quais ferramentas usar para resolver conflitos de merge e visualizar diferenças entre versões:

```bash
# Definir ferramenta de merge globalmente
git config --global merge.tool vimdiff

# Definir ferramenta de diff globalmente
git config --global diff.tool vimdiff

```

### Configurar Cache de Credenciais

Para evitar que o Git solicite sua senha várias vezes, você pode configurar o cache de credenciais:

```bash
# Configurar cache de credenciais com timeout de 1 hora (3600 segundos)
git config --global credential.helper "cache --timeout=3600"

```

### Configurar Coloração no Terminal

Ativar a coloração no terminal pode facilitar a leitura da saída do Git:

```bash
# Ativar coloração globalmente
git config --global color.ui auto

```

### Configurar Comportamento do Push

Você pode definir o comportamento padrão para o comando `git push`:

```bash
# Configurar comportamento padrão de push como 'simple'
git config --global push.default simple

```

### Configurar Arquivo `.gitignore` Global

Você pode definir um arquivo `.gitignore` global para ignorar arquivos em todos os seus repositórios:

```bash
# Configurar caminho para o arquivo .gitignore global
git config --global core.excludesfile ~/.gitignore_global

```

### Visualizar Configurações

Você pode visualizar as configurações atuais do Git usando:

```bash
# Ver todas as configurações globais
git config --global --list

# Ver todas as configurações locais (para o repositório atual)
git config --list

```

### Editar o Arquivo `.gitconfig` Diretamente

Você também pode abrir o arquivo `.gitconfig` em um editor de texto diretamente pelo terminal:

```bash
# Abrir o arquivo .gitconfig global para edição
git config --global --edit

# Abrir o arquivo .gitconfig local para edição (dentro de um repositório)
git config --edit

```

### Remover Configurações

Se você precisar remover uma configuração específica, pode usar o seguinte comando:

```bash
# Remover uma configuração global
git config --global --unset user.name

# Remover uma configuração local
git config --unset user.name

```

Esses comandos são bastante úteis para gerenciar suas configurações do Git de maneira eficiente, diretamente pelo terminal.

# Comando git config

Aqui está a tradução e explicação de cada opção do comando `git config` com exemplos simples de uso:

### Localização do Arquivo de Configuração

- **`-[no-]global`**: Usar o arquivo de configuração global.
    - **Exemplo**: `git config --global user.name "Seu Nome"`
    - **Explicação**: Este comando define o nome de usuário no nível global, aplicando a configuração a todos os repositórios do usuário.
- **`-[no-]system`**: Usar o arquivo de configuração do sistema.
    - **Exemplo**: `git config --system core.editor "vim"`
    - **Explicação**: Define o editor de texto "vim" como o editor padrão no nível do sistema, afetando todos os usuários no sistema.
- **`-[no-]local`**: Usar o arquivo de configuração do repositório.
    - **Exemplo**: `git config --local user.email "seu.email@exemplo.com"`
    - **Explicação**: Define o e-mail de usuário no nível local, aplicando a configuração apenas ao repositório atual.
- **`-[no-]worktree`**: Usar o arquivo de configuração específico por `worktree`.
    - **Exemplo**: `git config --worktree core.autocrlf true`
    - **Explicação**: Configura uma opção específica para a `worktree` atual.
- **`f, --[no-]file <file>`**: Usar o arquivo de configuração especificado.
    - **Exemplo**: `git config -f ~/.gitconfig-alt user.name "Outro Nome"`
    - **Explicação**: Utiliza um arquivo de configuração alternativo (`~/.gitconfig-alt`) para definir o nome de usuário.
- **`-[no-]blob <blob-id>`**: Ler a configuração de um objeto blob específico.
    - **Exemplo**: `git config --blob 1234567abcdef user.name`
    - **Explicação**: Obtém a configuração do nome de usuário de um blob específico no Git.

### Ação

- **`-[no-]get`**: Obter o valor de uma configuração.
    - **Exemplo**: `git config --get user.name`
    - **Explicação**: Exibe o valor da configuração `user.name`.
- **`-[no-]get-all`**: Obter todos os valores de uma chave.
    - **Exemplo**: `git config --get-all user.email`
    - **Explicação**: Exibe todos os valores associados à chave `user.email`.
- **`-[no-]get-regexp`**: Obter valores para expressões regulares.
    - **Exemplo**: `git config --get-regexp "user.*"`
    - **Explicação**: Exibe todas as configurações que correspondem à expressão regular `user.*`.
- **`-[no-]get-urlmatch`**: Obter valor específico para a URL.
    - **Exemplo**: `git config --get-urlmatch http.proxy <https://exemplo.com`>
    - **Explicação**: Obtém o valor da configuração de proxy para uma URL específica.
- **`-[no-]replace-all`**: Substituir todas as variáveis correspondentes.
    - **Exemplo**: `git config --replace-all user.name "Novo Nome"`
    - **Explicação**: Substitui todas as ocorrências da configuração `user.name` por "Novo Nome".
- **`-[no-]add`**: Adicionar uma nova variável.
    - **Exemplo**: `git config --add alias.co checkout`
    - **Explicação**: Adiciona um alias para o comando `checkout` chamado `co`.
- **`-[no-]unset`**: Remover uma variável.
    - **Exemplo**: `git config --unset user.name`
    - **Explicação**: Remove a configuração `user.name`.
- **`-[no-]unset-all`**: Remover todas as correspondências.
    - **Exemplo**: `git config --unset-all alias.co`
    - **Explicação**: Remove todas as ocorrências do alias `co`.
- **`-[no-]rename-section`**: Renomear uma seção.
    - **Exemplo**: `git config --rename-section old.name new.name`
    - **Explicação**: Renomeia a seção `old.name` para `new.name`.
- **`-[no-]remove-section`**: Remover uma seção.
    - **Exemplo**: `git config --remove-section alias`
    - **Explicação**: Remove a seção `alias` inteira do arquivo de configuração.
- **`l, --[no-]list`**: Listar todas as configurações.
    - **Exemplo**: `git config --list`
    - **Explicação**: Exibe todas as configurações atuais do Git.
- **`e, --[no-]edit`**: Abrir o arquivo de configuração em um editor.
    - **Exemplo**: `git config --global --edit`
    - **Explicação**: Abre o arquivo de configuração global no editor padrão.
- **`-[no-]get-color`**: Encontrar a cor configurada.
    - **Exemplo**: `git config --get-color branch.master "red"`
    - **Explicação**: Obtém a cor configurada para a branch `master`, usando "red" como padrão se não houver configuração.
- **`-[no-]get-colorbool`**: Encontrar a configuração de cor.
    - **Exemplo**: `git config --get-colorbool branch.master`
    - **Explicação**: Verifica se uma cor está configurada para a branch `master`.

### Tipo

- **`t, --[no-]type <type>`**: O valor é dado neste tipo.
    - **Exemplo**: `git config -t bool user.active true`
    - **Explicação**: Define a configuração `user.active` como um valor booleano (`true`).
- **`-bool`**: O valor é "true" ou "false".
    - **Exemplo**: `git config --bool core.autocrlf true`
    - **Explicação**: Define a configuração `core.autocrlf` como `true` (habilitado).
- **`-int`**: O valor é um número decimal.
    - **Exemplo**: `git config --int gc.auto 1000`
    - **Explicação**: Define a configuração `gc.auto` como `1000`.
- **`-bool-or-int`**: O valor é `-bool` ou `-int`.
    - **Exemplo**: `git config --bool-or-int gc.auto true`
    - **Explicação**: Define a configuração `gc.auto` como um valor booleano ou inteiro.
- **`-bool-or-str`**: O valor é `-bool` ou string.
    - **Exemplo**: `git config --bool-or-str user.active "true"`
    - **Explicação**: Define a configuração `user.active` como um valor booleano ou string.
- **`-path`**: O valor é um caminho (nome de arquivo ou diretório).
    - **Exemplo**: `git config --path core.excludesfile ~/.gitignore_global`
    - **Explicação**: Define o caminho para o arquivo `.gitignore_global`.
- **`-expiry-date`**: O valor é uma data de expiração.
    - **Exemplo**: `git config --expiry-date gc.pruneexpire "now"`
    - **Explicação**: Define a configuração `gc.pruneexpire` para expirar imediatamente.

### Outras Opções

- **`z, --[no-]null`**: Termina os valores com byte NUL.
    - **Exemplo**: `git config -z --list`
    - **Explicação**: Lista todas as configurações terminando com um byte NUL em vez de uma nova linha.
- **`-[no-]name-only`**: Mostra apenas os nomes das variáveis.
    - **Exemplo**: `git config --name-only --get-regexp "alias.*"`
    - **Explicação**: Mostra apenas os nomes das variáveis que correspondem à expressão regular `alias.*`.
- **`-[no-]includes`**: Respeita as diretivas de inclusão ao buscar.
    - **Exemplo**: `git config --includes --get user.name`
    - **Explicação**: Obtém a configuração `user.name`, respeitando as diretivas de inclusão (`include`).
- **`-[no-]show-origin`**: Mostra a origem da configuração.
    - **Exemplo**: `git config --show-origin --list`
    - **Explicação**: Lista todas as configurações mostrando de qual arquivo elas se originam.
- **`-[no-]show-scope`**: Mostra o escopo da configuração.
    - **Exemplo**: `git config --show-scope --get user.name`
    - **Explicação**: Mostra o escopo da configuração `user.name`, indicando se é global, local, etc

.

- **`-[no-]default <value>`**: Com `-get`, usa o valor padrão quando a entrada está ausente.
    - **Exemplo**: `git config --default "Nome Padrão" --get user.name`
    - **Explicação**: Obtém o valor da configuração `user.name`, retornando "Nome Padrão" se a configuração não existir.

Esses exemplos cobrem uma ampla gama de comandos `git config` para configurar e gerenciar as preferências e comportamentos do Git.

# CONFIG ALIAS

Configurar aliases no Git pode agilizar significativamente seu fluxo de trabalho, permitindo executar comandos complexos com atalhos simples. Abaixo está uma lista de aliases úteis, explicando para que servem e como usá-los, além de instruções sobre como adicioná-los ao seu arquivo `.gitconfig`.

### O Que São Aliases no Git?

Aliases no Git são atalhos personalizados para comandos Git que você utiliza com frequência. Eles ajudam a economizar tempo e a simplificar operações comuns, tornando seu trabalho mais eficiente.

### Como Configurar Aliases no Git

Você pode configurar aliases de duas maneiras:

1. **Editando o arquivo `.gitconfig` diretamente**:
    - No Windows, este arquivo geralmente está localizado em `C:\\Users\\SeuUsuario\\.gitconfig`.
    - Abra o arquivo em um editor de texto e adicione uma seção `[alias]` se ela ainda não existir.
2. **Usando comandos Git no terminal**:
    - Utilize o comando `git config --global alias.<alias> <comando>` para adicionar aliases.

### Exemplo de Adição de Aliases via Terminal:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit

```

### Lista de Aliases Úteis com Explicações

A seguir, apresento uma lista de aliases úteis divididos em categorias, com explicações detalhadas sobre para que servem e como usá-los.

### **Aliases Básicos**

1. **st** – Status
    - **Alias**: `st`
    - **Comando Completo**: `status`
    - **Configuração**:
        
        ```
        [alias]
            st = status
        
        ```
        
    - **Uso**:
        
        ```bash
        git st
        
        ```
        
2. **co** – Checkout
    - **Alias**: `co`
    - **Comando Completo**: `checkout`
    - **Configuração**:
        
        ```
        [alias]
            co = checkout
        
        ```
        
    - **Uso**:
        
        ```bash
        git co <branch-name>
        
        ```
        
3. **br** – Branch
    - **Alias**: `br`
    - **Comando Completo**: `branch`
    - **Configuração**:
        
        ```
        [alias]
            br = branch
        
        ```
        
    - **Uso**:
        
        ```bash
        git br
        
        ```
        
4. **ci** – Commit
    - **Alias**: `ci`
    - **Comando Completo**: `commit`
    - **Configuração**:
        
        ```
        [alias]
            ci = commit
        
        ```
        
    - **Uso**:
        
        ```bash
        git ci -m "Mensagem do commit"
        
        ```
        

### **Aliases para Log e Histórico**

1. **lg** – Log com Gráfico
    - **Alias**: `lg`
    - **Comando Completo**: `log --graph --oneline --decorate --all`
    - **Configuração**:
        
        ```
        [alias]
            lg = log --graph --oneline --decorate --all
        
        ```
        
    - **Uso**:
        
        ```bash
        git lg
        
        ```
        
2. **last** – Mostrar Último Commit
    - **Alias**: `last`
    - **Comando Completo**: `log -1 HEAD`
    - **Configuração**:
        
        ```
        [alias]
            last = log -1 HEAD
        
        ```
        
    - **Uso**:
        
        ```bash
        git last
        
        ```
        
3. **shortlog** – Log Resumido
    - **Alias**: `shortlog`
    - **Comando Completo**: `log --oneline`
    - **Configuração**:
        
        ```
        [alias]
            shortlog = log --oneline
        
        ```
        
    - **Uso**:
        
        ```bash
        git shortlog
        
        ```
        
4. **graph** – Log Gráfico Detalhado
    - **Alias**: `graph`
    - **Comando Completo**: `log --graph --decorate --pretty=oneline --abbrev-commit`
    - **Configuração**:
        
        ```
        [alias]
            graph = log --graph --decorate --pretty=oneline --abbrev-commit
        
        ```
        
    - **Uso**:
        
        ```bash
        git graph
        
        ```
        

### **Aliases para Branches**

1. **branches** – Listar Branches com Detalhes
    - **Alias**: `branches`
    - **Comando Completo**: `branch -vv`
    - **Configuração**:
        
        ```
        [alias]
            branches = branch -vv
        
        ```
        
    - **Uso**:
        
        ```bash
        git branches
        
        ```
        
2. **merged** – Branches Mescladas
    - **Alias**: `merged`
    - **Comando Completo**: `branch --merged`
    - **Configuração**:
        
        ```
        [alias]
            merged = branch --merged
        
        ```
        
    - **Uso**:
        
        ```bash
        git merged
        
        ```
        
3. **unmerged** – Branches Não Mescladas
    - **Alias**: `unmerged`
    - **Comando Completo**: `branch --no-merged`
    - **Configuração**:
        
        ```
        [alias]
            unmerged = branch --no-merged
        
        ```
        
    - **Uso**:
        
        ```bash
        git unmerged
        
        ```
        
4. **current** – Branch Atual
    - **Alias**: `current`
    - **Comando Completo**: `rev-parse --abbrev-ref HEAD`
    - **Configuração**:
        
        ```
        [alias]
            current = rev-parse --abbrev-ref HEAD
        
        ```
        
    - **Uso**:
        
        ```bash
        git current
        
        ```
        

### **Aliases para Rebase e Reset**

1. **rb** – Rebase Interativo
    - **Alias**: `rb`
    - **Comando Completo**: `rebase -i`
    - **Configuração**:
        
        ```
        [alias]
            rb = rebase -i
        
        ```
        
    - **Uso**:
        
        ```bash
        git rb <commit>
        
        ```
        
2. **undo** – Desfazer Último Commit
    - **Alias**: `undo`
    - **Comando Completo**: `reset --soft HEAD~1`
    - **Configuração**:
        
        ```
        [alias]
            undo = reset --soft HEAD~1
        
        ```
        
    - **Uso**:
        
        ```bash
        git undo
        
        ```
        
3. **amend** – Alterar Último Commit
    - **Alias**: `amend`
    - **Comando Completo**: `commit --amend`
    - **Configuração**:
        
        ```
        [alias]
            amend = commit --amend
        
        ```
        
    - **Uso**:
        
        ```bash
        git amend -m "Nova mensagem do commit"
        
        ```
        

### **Aliases para Limpeza e Otimização**

1. **cleanup** – Remover Arquivos Não Rastreáveis
    - **Alias**: `cleanup`
    - **Comando Completo**: `clean -fd`
    - **Configuração**:
        
        ```
        [alias]
            cleanup = clean -fd
        
        ```
        
    - **Uso**:
        
        ```bash
        git cleanup
        
        ```
        
2. **gc** – Coleta de Lixo e Otimização
    - **Alias**: `gc`
    - **Comando Completo**: `gc --prune=now --aggressive`
    - **Configuração**:
        
        ```
        [alias]
            gc = gc --prune=now --aggressive
        
        ```
        
    - **Uso**:
        
        ```bash
        git gc
        
        ```
        

### **Aliases para Manipulação de Arquivos**

1. **unstage** – Remover Arquivo da Área de Staging
    - **Alias**: `unstage`
    - **Comando Completo**: `reset HEAD --`
    - **Configuração**:
        
        ```
        [alias]
            unstage = reset HEAD --
        
        ```
        
    - **Uso**:
        
        ```bash
        git unstage <arquivo>
        
        ```
        
2. **show-files** – Mostrar Arquivos de um Commit
    - **Alias**: `show-files`
    - **Comando Completo**: `show --name-only`
    - **Configuração**:
        
        ```
        [alias]
            show-files = show --name-only
        
        ```
        
    - **Uso**:
        
        ```bash
        git show-files <commit>
        
        ```
        

### **Aliases para Ferramentas Externas e LFS**

1. **visual** – Abrir Ferramenta Visual de Diff
    - **Alias**: `visual`
    - **Comando Completo**: `difftool`
    - **Configuração**:
        
        ```
        [alias]
            visual = difftool
        
        ```
        
    - **Uso**:
        
        ```bash
        git visual
        
        ```
        
2. **lfs-status** – Status do Git LFS
    - **Alias**: `lfs-status`
    - **Comando Completo**: `lfs status`
    - **Configuração**:
        
        ```
        [alias]
            lfs-status = lfs status
        
        ```
        
    - **Uso**:
        
        ```bash
        git lfs-status
        
        ```
        

### **Aliases para Operações com Remotes**

1. **fetch-all** – Buscar de Todos os Remotes
    - **Alias**: `fetch-all`
    - **Comando Completo**: `fetch --all`
    - **Configuração**:
        
        ```
        [alias]
            fetch-all = fetch --all
        
        ```
        
    - **Uso**:
        
        ```bash
        git fetch-all
        
        ```
        
2. **cloneall** – Clonar com Submódulos
    - **Alias**: `cloneall`
    - **Comando Completo**: `clone --recurse-submodules`
    - **Configuração**:
        
        ```
        [alias]
            cloneall = clone --recurse-submodules
        
        ```
        
    - **Uso**:
        
        ```bash
        git cloneall <repository-url>
        
        ```
        
3. **remote-branches** – Listar Branches Remotos
    - **Alias**: `remote-branches`
    - **Comando Completo**: `branch -r`
    - **Configuração**:
        
        ```
        [alias]
            remote-branches = branch -r
        
        ```
        
    - **Uso**:
        
        ```bash
        git remote-branches
        
        ```
        
4. **push-all** – Push para Todos os Remotes
    - **Alias**: `push-all`
    - **Comando Completo**: `push --all`
    - **Configuração**:
        
        ```
        [alias]
            push-all = push --all
        
        ```
        
    - **Uso**:
        
        ```bash
        git push-all
        
        ```
        
5. **pull-all** – Pull de Todos os Remotes
    - **Alias**: `pull-all`
    - **Comando Completo**: `pull --all`
    - **Configuração**:
        
        ```
        [alias]
            pull-all = pull --all
        
        ```
        
    - **Uso**:
        
        ```bash
        git pull-all
        
        ```
        

### **Aliases para Pesquisa e Exploração**

1. **find** – Buscar por uma String nos Commits
    - **Alias**: `find`
    - **Comando Completo**: `grep`
    - **Configuração**:
        
        ```
        [alias]
            find = grep
        
        ```
        
    - **Uso**:
        
        ```bash
        git find "texto a buscar"
        
        ```
        
2. **blame** – Blame de Arquivo
    - **Alias**: `blame`
    - **Comando Completo**: `blame -c`
    - **Configuração**:
        
        ```
        [alias]
            blame = blame -c
        
        ```
        
    - **Uso**:
        
        ```bash
        git blame <arquivo>
        
        ```
        

### **Aliases Avançados**

1. **count-commits** – Contar Commits
    - **Alias**: `count-commits`
    - **Comando Completo**: `rev-list --count HEAD`
    - **Configuração**:
        
        ```
        [alias]
            count-commits = rev-list --count HEAD
        
        ```
        
    - **Uso**:
        
        ```bash
        git count-commits
        
        ```
        
2. **detailed-log** – Log Detalhado
    - **Alias**: `detailed-log`
    - **Comando Completo**: `log --pretty=format:"%h - %an, %ar : %s"`
    - **Configuração**:
        
        ```
        [alias]
            detailed-log = log --pretty=format:"%h - %an, %ar : %s"
        
        ```
        
    - **Uso**:
        
        ```bash
        git detailed-log
        
        ```
        
3. **squash** – Squash Commits
    - **Alias**: `squash`
    - **Comando Completo**: `rebase -i HEAD~<n>`
    - **Configuração**:
        
        ```
        [alias]
            squash = "!f() { git rebase -i HEAD~$1; }; f"
        
        ```
        
    - **Uso**:
        
        ```bash
        git squash 3
        
        ```
        

**Nota**: Alguns aliases mais avançados, especialmente aqueles que envolvem scripts ou funções de shell, podem requerer configuração adicional ou ajustes conforme seu ambiente específico.

### Exemplos de Adição ao Seu `.gitconfig`

Com base no seu arquivo `.gitconfig` atual, você pode adicionar a seção `[alias]` da seguinte maneira:

```
[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    lg = log --graph --oneline --decorate --all
    last = log -1 HEAD
    shortlog = log --oneline
    graph = log --graph --decorate --pretty=oneline --abbrev-commit
    branches = branch -vv
    merged = branch --merged
    unmerged = branch --no-merged
    current = rev-parse --abbrev-ref HEAD
    rb = rebase -i
    undo = reset --soft HEAD~1
    amend = commit --amend
    cleanup = clean -fd
    gc = gc --prune=now --aggressive
    unstage = reset HEAD --
    show-files = show --name-only
    visual = difftool
    lfs-status = lfs status
    fetch-all = fetch --all
    cloneall = clone --recurse-submodules
    remote-branches = branch -r
    push-all = push --all
    pull-all = pull --all
    find = grep
    blame = blame -c
    count-commits = rev-list --count HEAD
    detailed-log = log --pretty=format:"%h - %an, %ar : %s"

```

### Como Usar os Aliases

Após configurar os aliases, você pode usá-los como se fossem comandos Git normais. Aqui estão alguns exemplos:

- **Ver o status do repositório**:
    
    ```bash
    git st
    
    ```
    
- **Fazer checkout para uma branch**:
    
    ```bash
    git co nome-da-branch
    
    ```
    
- **Listar branches com detalhes**:
    
    ```bash
    git branches
    
    ```
    
- **Ver log com gráfico**:
    
    ```bash
    git lg
    
    ```
    
- **Desfazer o último commit mantendo as mudanças**:
    
    ```bash
    git undo
    
    ```
    
- **Abrir ferramenta visual de diff**:
    
    ```bash
    git visual
    
    ```
    

### Dicas para Criar Seus Próprios Aliases

1. **Seja Consistente**: Use nomes de aliases que sejam fáceis de lembrar e consistentes com seus hábitos de uso.
2. **Evite Conflitos**: Certifique-se de que o nome do alias não conflite com comandos Git existentes.
3. **Use Alias Descritivos para Comandos Complexos**: Para comandos que você usa raramente ou que são complexos, escolha nomes de alias que descrevam claramente a ação que serão realizadas.
4. **Documente Seus Aliases**: Mantenha um documento com os aliases que você criou para referência futura, especialmente se você trabalha em diferentes máquinas ou ambientes.

### Recursos Adicionais

- **Documentação Oficial do Git sobre Configuração**: [git-config Documentation](https://git-scm.com/docs/git-config#_alias)
- **Listas de Aliases Populares**: Pesquise online para encontrar listas de aliases que outros desenvolvedores acham úteis e adapte-os conforme necessário.

### Conclusão

Adicionar aliases ao Git pode transformar a maneira como você interage com seus repositórios, tornando as operações diárias mais rápidas e eficientes. A lista acima oferece um ponto de partida robusto, mas sinta-se à vontade para personalizá-la de acordo com suas necessidades específicas.
