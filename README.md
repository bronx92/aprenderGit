
# Comandos Git

## Veja abaixo alguns comandos básicos (porém muito úteis) do Git

**git log**
 
 Esse comando é muito importante pois é com ele que podemos consultar de maneira detalhada tudo que foi feito no repositório, o que resulta na possibilidade de realizarmos o Controle de Versão. Esse comando exibe informações gerais sobre commits realizados no repositório. 

#### Opções de git log
* *git log --decorate* - formata a exibição do log para que facilite a visualização. É mais útil quando o projeto possui muitas Branchs e Tags, pois esse comando exibe de forma destacada a qual branch se refere cada commit, bem como as tags que cada commit possua;
* *git log --author "Name"* - lista todos os commits do autor citado;
* *git shortlog* - lista todos os commits realizados por todos os autores de forma curta;
* *git log --graph* - mostra de forma gráfica os commits no repositório;
* *git log --oneline* - mostra cada commit resumidos em 1 linha.

**git show 'HASH'**

 Esse comando mostra as modificações de forma mais detalhada em um commit específico, definido pelo HASH .

 **git diff**

Exibe (destacando em verde) as alterações salvas no arquivo antes dele ser adicionado ao stage. É uma maneira de conferir o que foi feito antes do commit. Pode ser utilizado com a opção *--name-only*, que exibe somente o nome dos aquivos modificados, o que se torna útil caso o repositório tenha uma lista grande de arquivos e seja necessário saber quais foram modificados.

**git restore 'file.ext'**

 Descarta as alterações realizadas no arquivo mencionado no comando apagando **todas** as adições feitas no arquivo. Ao usar esse comando, é necessário estar certo de que nenhuma das alterações serão aproveitadas. Quando esse comando é usado com a opção _--staged_ o arquivo apenas será removido do stage mas suas modificações reais permanecerão intactas.

 **git checkout 'file.ext'**

Descarta as alterações realizadas no arquivo mencionado. Tem a mesma função do *git restore 'file.ext'*.

**git reset**

Esse comando permite desfazer commits caso seja necessário. Para isso existem algumas opções que devem ser utilizadas em casos diferentes, mas em todos eles deve ser em mente o seguinte: é necessário informar o HASH anterior ao commit que deseja-se desfazer. 

* **git reset HEAD 'file.ext'** - Remove o arquivo mencionado do stage.
* **git reset --soft 'HASH'** - Desfaz o commit e retorna o arquivo ao stage, sem apagar do arquivo nenhuma alteração feita. Para isso, deve-se informar o HASH anterior ao commit que se deseja desfazer. Essa opção também pode ser usada para casos em que seja necessário reescrever o comentário sobre as mudanças feitas. 
Obs.: Quando é necessário desfazer dois ou mais commits através desse comando, o git conserva as modificações "na fila" exatamente como foram realizadas nos commits desfeitos. Ex.: Ao retornar dois commits, o git mantém no stage, prontas pra serem commitadas, as alterações feitas depois commit do HASH informado, e mantém fora do stage, porém também inalteradas, as modificações do último commit realizado. Isso possibilita alterar somente o comentário dos commits, sem modificar o histórico das alterações. Basta que seja feito o commit com a mensagem corrigida, uma nova adição ao stage e por fim o último commit (exatamente nessa ordem), garantindo assim o histórico anterior inalterado e as correções devidas nos comentários.
* **git reset --mixed 'HASH'** - Desfaz o(s) commit(s) e retorna o arquivo ao ao estado *modified*, ou seja, antes de ser adicionado ao stage. Assim como o soft, não apaga do arquivo as alterações feitas. Essa opção pode ser usada para casos em seja necessário revisar ou refazer as alterações e/ou adições que possam estar incorretas.
* **git reset --hard 'HASH'** - Desfaz o commit e apaga todas as modificações feitas no(s) commit(s) desfeitos. Deve ser utilizado com muito cuidado

**git revert**

Esse comando reverte as alterações realizadas no commit informado sem apagar o histórico de commits bem como os arquivos alterados nesse commit. Ele é ser útil quando um determinado commit precisa ser desfeito mas o usuário quer analisar as alterações desse commit. Para isso basta rodar o commando __*git revert 'HASH'*__.

**git stash**

Esse é um comando muito conveniente em situações onde o usuário faz alterações em algum arquivo local e precisa pausar essas alterações para fazer um pull e atualizar o repositório local ou ainda criar uma nova branch onde essas alterações inicialmente não devem ser inseridas. Veja abaixo as opções para uso desse comando

* **git stash** - remove temporariamente as alterações salvas em um arquivo, reservando-as em "standby", aguardando o momento certo de serem reaplicadas ao arquivo editado. Isso evita possíveis conflitos em repositórios desatualizados (por qualquer motivo que seja...) quando o usuário aplica um *git pull*, sem que se perca toda evolução do trabalho já realizado antes da atualização do repositório;
* **git stash apply** - "devolve" ao arquivo as alterações que estavam em standby;
* **git stash list** - lista todos os stashs criados, identificando em qual branch foi originado.
* **git stash clear** - limpa todos os stashs criados. Pode ser usado após aplicar as alterações que estavam guardadas.


## Trabalhando com Branchs

* Criar uma branch - **git checkout -b 'nome-da-branch'**;
* Exibir branchs criadas no repositório local - **git branch**;
* Acessar a branch onde se deseja trabalhar - **git checkout 'nome-da-branch'**;
* Deletar branch do repositório local - **git branch -D 'nome-da-branch'**;
* Deletar branch do repositório remoto - **git push :'nome-da-branch'**.


## Usando Alias

Alias são atalhos que podem ser criados para facilitar o trabalho, evitando digitação de comandos longos ou que precisem ser digitados constantemente. Para criar um atalho basta usar o comando **git config --global alias.nome-que-desejar comando-a-ser-mudado**.
Ex.: *git config --global alias.s status* para digitar __*git s*__ no lugar de __*git status*__.


## Versionando com Tags

As Tags são utilizadas para realizar o versionamento (ou releases) do projeto. Veja abaixo como utilizar tags no git:

* **git tag 'versao-que-desejar'** - cria uma tag;
* **git tag 'versao-que-desejar' -a** - cria uma tag com um arquivo contendo uma anotação ou mensagem. No momento da criação da Tag o usuário pode definir a messagem do arquivo usando __-m "mensagem qualquer"__;
* **git push origin main --tags** - subir as tags criadas para o repositório remoto;
* **git tag -d 'versao-que-desejar'** - deleta a tag informada do repositório local;
* **git push :'versao-que-desejar'** - deleta do repositório remoto a tag informada.