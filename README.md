# Guia de boas práticas, convenções e procedimentos com o Git

---

# Sumário
1. [Convenções](#convenções)
2. [Comandos](#comandos)
    - [Clonar repositório](#1a-primeira-coisa-a-se-fazer-é-clonar-o-repositório-na-sua-máquina-para-fazer-isso-é-só-escrever-os-seguintes-comandos-no-terminal)
    - [Configurar usuário](#2-agora-devemos-fazer-a-configuração-do-seu-usuário-e-email-para-identificar-os-commits-que-faremos-mais-adiante)
    - [Listar branches](#3-então-conferimos-as-branches-existentes)
    - [Mudar de branch](#4-depois-devemos-mudar-para-a-branch-a-qual-vamos-trabalhar)
    - [Criar nova branch](#5-caso-seja-um-repositório-novo-apenas-com-a-branch-main-devemos-criar-uma-nova-branch)
    - [Renomear branch](#6-caso-tenha-criado-uma-branch-com-o-nome-errado-podemos-renomear-a-branch-em-que-estamos-com)
    - [Adicionar arquivos ao staging](#7-depois-de-estar-na-branch-certa-podemos-codar-ou-refatorar-o-código-para-preparar-as-alterações-para-o-próximo-commit-devemos-adicionar-os-arquivos-ao-staging-com)
    - [Fazer commit](#8-agora-devemos-fazer-o-commit-com)
    - [Renomear commit](#9-para-corrigirrenomear-a-mensagem-do-último-commit-em-caso-de-erro)
    - [Subir commits/branch para o repositório remoto (upload)](#10-depois-de-fazer-oos-commits-desejados-podemos-subir-para-o-repositório-remoto-com)
    - [Baixar mudanças do repositório remoto (download)](#11-para-baixar-possíveis-mudanças-do-repositório-remoto-utilize)
    - [Deletar o último commit](#12-para-deletar-o-último-commit)
    - [Conferir status dos arquivos](#13-para-conferir-o-status-dos-arquivos-o-que-está-em-stage-para-ser-commitado-os-arquivos-que-foram-modificados-e-arquivos-novos-que-não-estão-rastreados)
    - [Ver diferenças (git diff)](#14-para-exibir-as-mudanças-que-ainda-não-foram-preparadas-para-o-commit)
    - [Ver o histórico de commits](#15-para-conferir-o-histórico-de-commits)
    - [Fazer merge](#16-depois-de-concluir-todas-as-alterações-na-branch-voce-deve-realizar-um-merge-primeiro-vá-para-a-branch-que-irá-receber-as-alterações-ex-caso-você-queira-mesclar-uma-branch-feature-a-branch-develop-você-deve-estar-na-branch-develop-com-git-checkout-develop-e-depois)
    - [Revertendo o merge](#17-caso-o-merge-da-feature-na-develop-tenha-sido-um-erro-ex-revisões-insuficientes-na-pr-faltou-subir-algum-commit-você-pode-reverter-o-merge-com)
    - [Deletar uma branch](#18-depois-de-dar-merge-podemos-deletar-a-brach)
    - [Git tag para definir versões](#19-depois-de-qualquer-merge-na-branch-main-devemos-marcar-com-um-tag-de-versão-com)
    - [Git Rebase](#20-o-git-rebase)
    - [Git stash para salvar alterações sem fazer commit](#21-git-stash-para-salvar-alterações-sem-fazer-um-commit)
    - [Listar os stashes](#22-para-listar-os-stashes)
    - [Aplicar stash](#23-aplicando-stashes)
    - [Remover stash da lista](#24-remover-stashes-da-lista)
    - [Criar branch a partir de um stash](#25-para-criar-uma-branch-a-partir-do-stash-mais-recente)
3.  [Como funciona o gitflow](#como-funciona-o-git-flow)
4. [Pull Requests](#pull-requests)

---

# Convenções

### 1. Fazer commits com mensagens de fato descritivas, usando o ```tempo verbal no imperativo``` como: "adicionA login" ou "corrigE erro no crud" ```para lermos```: "```esse commit adiciona login```" ou "```esse commit corrige erro no crud```"
### 2. Proibido fazer ```git commit -m "."``` ou 'git commit -m " :pray: " ' ou qualquer coisa do tipo
### 3. Não criar títulos muito longos para commits, utilizar o formato "título curto + corpo detalhado" quando necessário:
Título: O que foi feito.
Corpo: Por que e como foi feito.

Um título acima de 72 caracteres já é considerado longo. Após esse ponto, muitas ferramentas cortam 
a mensagem ou dificultam a visualização em logs curtos (ex.: git log --oneline). O título: 
```Adiciona validação de email no formulário de cadastro para melhorar segurança``` (77 caracteres) 
ja é considerado um título longo.

### 4. Evitar fazer commits gigantes: Facilita a revisão e reduz conflitos.
### 5. Evitar fazer branches gigantes: Facilita a revisão e reduz conflitos.
### 6. Criar branches com o prefixo ```fix/``` ou ```feature/``` seguido de um nome no ```tempo verbal infinitivo```: "adicionAR login" "corrigIR crud" de acordo com o propósito da branch
### 7. Na nossa equipe utilizaremos o git flow, para ver como ele funciona [clique aqui](#como-funciona-o-git-flow)
### 8. Não criar branches hotfix explicado [aqui](#obs-na-nossa-equipe-iremos-considerar-o-uso-de-um-hotfix-como-desleixo-e-falta-de-preparo-pois-estamos-desenvolvendo-algo-voltado-à-escola-de-ti-e-não-temos-usuários-utilizando-a-versão-de-produção-então-não-utilizaremos-a-branch-hotfix)
## Convenções sobre [Pull Requests](#pull-requests)
### 9. Só abrir uma PR quando achar que a branch está concluída e de fato pode ser mergeada
### 10. Fazer títulos para as Pull Requests seguindo o mesmo padrão da convenção dos commits ([item 1](#1-fazer-commits-com-mensagens-de-fato-descritivas-usando-o-tempo-verbal-no-imperativo-como-adiciona-login-ou-corrige-erro-no-crud-para-lermos-esse-commit-adiciona-login-ou-esse-commit-corrige-erro-no-crud))
### 11. Descreva o PR incluindo o propósito, o que foi feito e como testar.
### 12. Adicione revisores garantindo que o time revise antes do merge.
### 13. Teste antes de submeter: Certifique-se de que o código compila e os testes passam.
### 14. Mantenha PRs pequenos: Facilita a revisão e reduz conflitos.
### 15. Sempre forneça descrições detalhadas no PR e responda prontamente aos feedbacks para agilizar o processo de revisão.

---

# Comandos

### 1. A primeira coisa a se fazer é clonar o repositório na sua máquina, para fazer isso é só escrever os seguintes comandos no terminal: 

- Clonar o repositório:
```
git clone <url-do-repositório> 
```
- Caso queira começar um repositório novo a partir da sua máquina local:
```
git init <nome_do_repositório>
```
- O comando acima cria um repositório em uma pasta filha com o nome que você digitou, caso queira criar o repositório na mesma pasta em que já está utilize apenas:
```
git init
```
- Depois de criar um repositório local novo vamos criar um repositório remoto e conectar a ele:
```
git remote add origin <URL_do_repositório_remoto>
```
- OBS: **Não** inicialize o repositório remoto com README ou outros arquivos se você já tem um repositório local, para evitar conflitos. Apenas crie um repositório vazio.

### 2. Agora devemos fazer a configuração do seu usuário e email para identificar os commits que faremos mais adiante:
- Inserir seu nome
```
git config --global user.name "<seu_nome>"
```
- Inserir seu email
```
git config --global user.email "<seu_email>"
```

### 3. Então conferimos as branches existentes

- Para listar todas as branches presentes no repositório remoto:
```
git branch -r
```

- Para listar todas as branches presentes no repositório local:
```
git branch
```

### 4. Depois devemos mudar para a branch a qual vamos trabalhar: 
```
git checkout <nome_da_branch>
```
- Ou 
```
git switch <nome_da_branch>
```

- OBS: quando clonamos um repositório, é baixada na máquina local apenas a branch main do repositório remoto, porém
ao utilizar um dos dois comandos acima para alterar para alguma branch do repositório remoto que vimos com ```git branch -r```
essa branch é baixada automaticamente e a troca de branch é efetuada.

### 5. Caso seja um repositório novo, apenas com a branch main devemos criar uma nova branch:
```
git branch <nome_da_branch>
```
- Para criar uma nova branch e já mudar para ela:
```
git checkout -b <nome_da_branch>
```
- Ou 
```
git switch -c <nome_da_branch>
```

### 6. Caso tenha criado uma branch com o nome errado podemos renomear a branch em que estamos com:
```
git branch -m <nome_novo>
```
- Se você quiser renomear uma branch específica (sem estar nela) use:
```
git branch -m <nome_antigo> <nome_novo>
```

### 7. Depois de estar na branch certa podemos codar ou refatorar o código. Para preparar as alterações para o próximo commit devemos adicionar os arquivos ao "staging" com:
```
git add <nome_do_arquivo>
```
- Ou para adicionar todos os arquivos que foram modificados
```
git add .
```

### 8. Agora devemos fazer o commit com:
```
git commit -m "<titulo_do_commit>"
```
- Caso queira fazer uma descrição longa para o commit use:
```
git commit -m "<titulo_do_commit>" -m "<descricao_detalhada>"
```

### 9. Para corrigir/renomear a mensagem do último commit em caso de erro:
```
git commit --amend -m "<novo_titulo_do_commit>"
```

### 10. Depois de fazer o/os commits desejados podemos subir para o repositório remoto com:
```
git push -u origin <nome_da_branch>
```

Nota: com esse comando, caso você esteja publicando a branch no repositório remoto pela primeira vez 
a flag ```-u```, que é a abreviação de ```--set-upstream``` é utilizado para estabelecer uma relação 
de rastreamento (tracking) entre sua branch local e a branch remota. Isso permite que você use os 
comandos ```git pull``` e ```git push``` diretamente, sem precisar especificar explicitamente a 
branch remota e o repositório toda vez. Quando utilizamos ```git branch -r``` e depois ```git switch``` ou ```git checkout``` para baixar a branch do remoto e já mudar para ela esse rastreamento/
tracking já é estabelecido automaticamente.

### 11. Para baixar possíveis mudanças do repositório remoto utilize:
```
git pull origin <nome_da_branch>
```
- Caso queira puxar **sem** mesclar as mudanças com o que você tem na sua máquina utilize:
```
git fetch
```
- Para remover as referências a branches que já foram deletadas no remoto da sua máquina use:
```
git fetch origin --prune
```
 
### 12. Para deletar o último commit:
```
git reset --soft HEAD~1
```
- No caso acima ele apaga o último commit porém mantém as alterações no staging, ou seja, as alterações feitas são mantidas podendo ser commitadas novamente, já se quiser apagar completamente o commit use: 
```
git reset --hard HEAD~1
```
- Isso deleta o commit e apaga as alterações que estavam no staging, ou seja, tudo que foi criado / atualizado nesse commit é desfeito.

### 13. Para conferir o status dos arquivos (o que está em stage para ser commitado, os arquivos que foram modificados e arquivos novos que não estão rastreados):
```
git status
```
- Dica: é melhor de ver essas diferenças pela própria interface do Vs Códigos

- O git status também é muito útil para ver em qual branch você está trabalhando (ex.: On branch main) e se ela está atualizada em relação ao repositório remoto (como "Your branch is up to date with 'origin/main'")

### 14. Para exibir as mudanças que ainda não foram preparadas para o commit:
```
git diff
```
- Para mostrar as diferenças entre o que está na área de staging e o último commit, em outras palavras o que está preparado para o próximo commit:
```
git diff --staged
```
- Para comparar as diferenças introduzidas no último commit.
```
git diff HEAD^ HEAD: 
```
- Para comparar as diferenças entre duas branches, como git diff main develop:
```
git diff <branch1> <branch2>
```

- Dica: é melhor de ver essas diferenças pela própria interface do Vs Códigos

### 15. Para conferir o histórico de commits:
```
git log
```
- Para exibir o histórico de commits do repositório em formato de gráfico ASCII, mostrando visualmente as ramificações e merges entre branches. É útil para entender a estrutura do projeto e como as branches se conectam.
```
git log --graph
```

### 16. Depois de concluir todas as alterações na branch voce deve realizar um merge, **primeiro vá para a branch que irá receber as alterações** (ex: caso você queira mesclar uma branch feature a branch develop você deve estar na branch develop) com ```git checkout develop``` e depois:
```
git merge feature/<nome_da_feature>
```

- Para criar um commit de merge explícito, garantindo clareza, rastreabilidade e facilidade de reversão no histórico do Git:

```
git merge --no-ff feature/filtro-por-capacidade
```

- OBS: o comando git merge não será muito utilizado pois faremos os merges com os [Pull Requests](#pull-requests) através da 
interface do GitHub, mas pode ser utilizado caso haja necessidade de atualizar alguma branch feature em relação a develop por 
exemplo.

### 17. Caso o merge da feature na develop tenha sido um erro (ex.: revisões insuficientes na PR, faltou subir algum commit), você pode reverter o merge com:

```
git revert -m 1 <ID_do_commit>
```

### 18. Depois de dar merge podemos deletar a brach:
```
git branch -d feature/<nome_da_feature>
```
- Para deletar uma branch que foi criada com o nome errado usamos:
```
git branch -D feature/<nome_da_feature>
```
- Do modo acima o git não se importa se a branch já foi mesclada ou não (com o 'd' minúsculo o git não exclui sem ter feito merge, dá erro)

- Para deletar a branch no repositório remoto: 
```
git push origin --delete <nome_da_branch>
```

### 19. Depois de qualquer merge na branch main devemos marcar com um tag de versão com:
```
git tag -a <nome_da_tag> -m "<descrição_da_tag>"
```
- Do modo acima marcamos o último commit (HEAD) com a tag, mas se quisermos marcar um commit anterior fazemos:
```
git tag -a <nome_da_tag> <ID_do_commit> -m "<descrição_da_tag>"
```
- Para ver todas as tags do repositório:
```
git tag
```
- Para ver com mais detalhes, ver a descrição da tag:
```
git show <nome_da_tag>
```
- As tags não são enviadas automaticamente ao repositório remoto por isso use:
```
git push origin <nome_da_tag>
```
- Para enviar todas as tags de uma vez:
```
git push origin --tags
```
- Para deletar uma tag localmente:
```
git tag -d <nome_da_tag>
```
- Para deletar uma tag remotamente:
```
git push origin --delete <nome_da_tag>
```

### 20. O git Rebase

O git rebase reescreve o histórico de uma branch, movendo seus commits para a base de outra branch. Em vez de criar um merge, ele 
aplica os commits da branch atual sobre a branch de destino, resultando em um histórico linear, como se tudo tivesse sido feito em 
sequência.
Exemplo:

```
git rebase develop
```
O comando acima (realizado estando na branch feature) pega os commits de feature e os reaplica sobre o último commit de develop. 
Como se você tivesse começado a trabalhar na feature depois das últimas mudanças da develop. 

- OBS: O git rebase **Não** é usado no Git Flow: O Git Flow prioriza a rastreabilidade e a 
preservação do histórico de merges, enquanto o rebase altera o histórico, eliminando a 
visibilidade das branches separadas. Isso pode dificultar a colaboração em equipes, pois 
reescrever commits já compartilhados (ex.: em um repositório remoto) causa conflitos para outros 
desenvolvedores. O Git Flow valoriza a clareza do fluxo em vez de um histórico linear. O git 
rebase até seria aceitável caso esteja trabalhando sozinho em uma branch feature "pequena", mas 
caso a branch seja compartilhada é melhor não fazer.

### 21. Git stash para salvar alterações sem fazer um commit

- Caso você precise salvar alterações temporariamente, para mudar de branch por exemplo, ou caso você tenha começado a realizar 
alterações na branch errada sem perceber use:
```
git stash save "<mensagem_descritiva>"
```
- Ou se não precisar de mensagem, apenas:
```
git stash
```
### 22. Para listar os stashes:
```
git stash list
```

### 23. Aplicando stashes

- Para aplicar o stash mais recente, mantendo-o na lista:
```
git stash apply
```
- Para aplicar um stash específico pelo índice:
```
git stash apply 'stash@{n}'
```
- Para aplicar o stash mais recente, removendo-o da lista:
```
git stash pop
```
- Para aplicar um stash específico e remove-lo da lista:
```
git stash pop 'stash@{n}'
```
### 24. Remover stashes da lista
- Para remover o último stash:
```
git stash drop
```
- Para remover um stash n específico:
```
git stash drop 'stash@{n}'
```
- Para remover todos os stashes
```
git stash clear
```
### 25. Para criar uma branch a partir do stash mais recente:
```
git stash brach <nome_da_branch>
```

---

# Como funciona o git flow

Gitflow é uma estratégia de branching (ramificação) que organiza o trabalho em equipe. As principais branches são:

- **main/master**: Contém o código estável e pronto para produção.

- **develop**: Integra funcionalidades em desenvolvimento, ainda não prontas para produção.

- **feature/***: Branches temporárias para desenvolver novas funcionalidades (ex.: feature/nova-funcionalidade).

- **hotfix/***: Branches para corrigir bugs urgentes em produção (ex.: hotfix/corrigir-bug-login).

- **release/***: Branches para preparar uma nova versão para produção (ex.: release/v1.0.0).

![imagem do git flow](./images/Git-flow.jpeg)

- Dica: Sempre comece entendendo o estado atual do repositório com [git branch](#3-então-conferimos-as-branches-existentes) e [git log](#15-para-conferir-o-histórico-de-commits).

- A **branch main e a branch develop** são as únicas branches permanentes
- teremos uma **branch feature** (que sempre sai da branch develop) para cada nova funcionalidade do nosso projeto, depois são mergeadas de volta a branch develop
- as **branches release** (não pode haver mais de uma branch desse tipo simultaneamente) saem da branch develop e servem para testar e corrigir uma nova versão a ser lançada, quando finalizar esse processo ela será mergeada tanto na main, gerando uma nova tag de versão, quanto na develop
- por último as **branches hotfix**, que servem para consertar erros críticos em produção, saem da branch main e são mergeados tanto na main gerando uma nova tag ([comandos para gerar tag](#19-depois-de-qualquer-merge-na-branch-main-devemos-marcar-com-um-tag-de-versão-com)) quanto na develop.

#### OBS: Na nossa equipe, iremos considerar o uso de um Hotfix como desleixo e falta de preparo, pois estamos desenvolvendo algo voltado à escola de TI e não temos usuários utilizando a versão de produção. Então não utilizaremos a branch hotfix.

- No caso de identificar bugs, ter a necessidade de refatorar código ou de uma feature que foi 
mergeada incompleta, devemos ou [reverter o merge](#17-caso-o-merge-da-feature-na-develop-tenha-sido-um-erro-ex-revisões-insuficientes-na-pr-faltou-subir-algum-commit-você-pode-reverter-o-merge-com) 
ou **proceder igual fazemos com as branches feature**, [criando uma nova branch](#5-caso-seja-um-repositório-novo-apenas-com-a-branch-main-devemos-criar-uma-nova-branch) 
como "fix/nome_da_feature", "refactor/nome_da_refatoracao", **nunca fazer commits diretamente na develop, muito menos na main**

caso ainda possua dúvidas sobre o gitFlow veja o [artigo da alura](https://www.alura.com.br/artigos/git-flow-o-que-e-como-quando-utilizar) à respeito

---

# Pull Requests

- Um Pull Request (PR) é uma proposta de integração de código. Ele serve como um checkpoint para revisão e aprovação antes do merge, garantindo qualidade e alinhamento com o projeto.
  
![fluxograma do pull request](./images/Fluxograma-Pull-Request.jpeg)

No fluxo GitFlow, Pull Requests (PRs) são utilizados para integrar branches como feature, hotfix ou release nas branches develop ou main. Esse processo permite discussões, revisões de código e resolução de conflitos antes da fusão.

## Passo a passo para criar e gerenciar uma PR

**1. Certifique-se de que sua branch está atualizada (Opcional*)**
Antes de abrir o PR, garanta que sua branch (ex.: feature/<nome_da_feature>) esteja sincronizada com as últimas alterações da branch develop.

Para isso, execute os seguintes comandos localmente no terminal: ```git switch develop```, ```git pull```, ```git switch feature/<nome_da_feature>``` e ```git merge develop``` (não se preocupe, 
fazer merge da develop na sua branch feature não fará você perder os commits feitos na feature)

Se houver conflitos, resolva-os manualmente, faça o commit das alterações e confirme que tudo está funcionando.

Nota: Prefira git merge em vez de git rebase para evitar reescrever o histórico, especialmente se a branch for compartilhada.

- * Esse passo é mais importante caso haja alterações ou correções importantes para a sua branch na 
develop e a feature ainda não está pronta para ser mergeada, ou a feature é muito grande e está 
levando muito tempo, de modo que há vários commits de diferença acumulados na develop. Como realizar 
esse passo pode causar conflitos, você estará adiantando a resolução desses conflitos que surgiriam 
apenas ao fazer o merge da feature.

**2. Envie sua branch para o repositório remoto**
Após atualizar a branch localmente, envie-a para o GitHub: ```git push -u origin feature/<nome_da_feature>```

**3. Acesse o repositório no GitHub**
Abra o navegador e vá até o repositório no website do GitHub onde sua branch foi enviada.

**4. Inicie o processo de criação do Pull Request**
Na página principal do repositório, clique na aba "Pull requests". Clique no botão verde "New pull request".

**5. Configure as branches do Pull Request**
No campo ```base```, selecione develop (a branch na qual você quer mesclar suas alterações).

No campo ```compare```, selecione feature/<nome_da_feature> (a branch com suas alterações).

O GitHub exibirá as diferenças entre as duas branches para revisão.

Nota: preste atenção neste passo pois, após a PR ser criada ela não pode ser excluída, apenas podemos alterar seu nome, incluir 
novos commits ou fechá-la (similar a arquivar). Evitar inconvenientes fazendo merge na branch errada.

**6. Preencha os detalhes do Pull Request**
Adicione um título claro e descritivo (ex.: "Adicionar funcionalidade X ao sistema").

No campo de descrição, inclua informações úteis como:
O objetivo das alterações.

Links para issues relacionadas, se houver.

Instruções específicas para revisores.

Opcionalmente, adicione revisores, labels ou milestones no lado direito da tela.

**7. Crie o Pull Request**
Revise as alterações exibidas na seção "Files changed" para garantir que tudo está correto.

Clique no botão verde "Create pull request" para abrir o PR oficialmente.

**8. Monitore revisões e responda a feedbacks**
Após abrir o PR, outros desenvolvedores podem revisar seu código e deixar comentários ou sugestões.

Se forem solicitadas alterações:
Faça os ajustes na sua branch localmente.

Commit e envie as mudanças com ```git push```.

**Atualizações com os novos commits aparecerão automaticamente no PR**.

**9. Mantenha a branch atualizada**
Se a branch develop receber novas alterações enquanto seu PR estiver em revisão, atualize sua branch novamente com git merge develop e envie as mudanças para o remoto.

Caso surjam conflitos, o GitHub indicará isso no PR, e você poderá resolvê-los localmente ou diretamente no website, siga as instruções exibidas na interface (caso os conflitos sejam muito extensos você terá que resolver localmente).

**10. Aprovação e fusão do Pull Request**
Após a aprovação dos revisores, o PR estará pronto para ser mesclado.

Na página do PR, clique em "Merge pull request" (se você tiver permissão) e escolha o método de fusão:
Merge commit: Cria um commit de mesclagem, preservando o histórico. (essa é a opção padrão e a que mais utilizaremos, 
é como o ```git merge --no-ff```)

Squash and merge: Combina todos os commits em um único commit, ideal para um histórico mais limpo. (```git merge --squash```)

Rebase and merge: Esta opção aplica os commits individuais da branch 'compare' diretamente na branch 'base', sem criar um commit 
de merge. Isso é similar a fazer um rebase local seguido de um fast-forward merge.

Confirme a fusão clicando em "Confirm merge".

**11. Delete a branch**
Após a fusão, o GitHub oferecerá a opção de deletar a branch feature/<nome_da_feature> no repositório remoto. Clique em "Delete branch" para manter o repositório organizado.

Localmente, você pode deletar a branch com: ```git branch -d feature/<nome_da_feature>```

- Para voltar ao sumário [clique aqui](#sumário)