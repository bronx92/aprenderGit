
# Comandos Git

## Veja abaixo alguns comandos básicos (porém muito úteis) do Git

### **git log**
 
 Esse comando é muito importante pois é com ele que podemos consultar de maneira detalhada tudo que foi feito no repositório, o que resulta na possibilidade de realizarmos o Controle de Versão. Esse comando exibe informações gerais sobre commits realizados no repositório. 

#### Opções de git log
* *git log 'directory_name ou file_name'* - acessa o log de uma pasta ou arquivo específico;
* *git log --decorate* - formata a exibição do log para que facilite a visualização. É mais útil quando o projeto possui muitas Branchs e Tags, pois esse comando exibe de forma destacada a qual branch se refere cada commit, bem como as tags que cada commit possua;
* *git log --author "Name"* - lista todos os commits do autor citado;
* *git shortlog* - lista todos os commits realizados por todos os autores de forma curta;
* *git log --graph* - mostra de forma gráfica os commits no repositório;
* *git log --oneline* - mostra cada commit resumidos em 1 linha.

### **git show 'HASH'**

 Esse comando mostra as modificações de forma mais detalhada em um commit específico, definido pelo HASH .

 ### **git diff**

Exibe (destacando em verde) as alterações salvas no arquivo antes dele ser adicionado ao stage. É uma maneira de conferir o que foi feito antes do commit. Pode ser utilizado com a opção *--name-only*, que exibe somente o nome dos aquivos modificados, o que se torna útil caso o repositório tenha uma lista grande de arquivos e seja necessário saber quais foram modificados.

### **git restore 'file.ext'**

 Descarta as alterações realizadas no arquivo mencionado no comando apagando **todas** as adições feitas no arquivo. Ao usar esse comando, é necessário estar certo de que nenhuma das alterações serão aproveitadas. Quando esse comando é usado com a opção _--staged_ o arquivo apenas será removido do stage mas suas modificações reais permanecerão intactas.

### **git checkout 'file.ext'**

Descarta as alterações realizadas no arquivo mencionado. Tem a mesma função do *git restore 'file.ext'*.

### **git reset**

Esse comando permite desfazer commits quando necessário. O comportamento padrão desse comando é desfazer os commits e alterar o estado dos arquivos. Existem também algumas opções que devem ser utilizadas em situações diferentes. 

* **git reset 'iniciais da HASH'** - Desfaz o commit mencionado;
* **git reset HEAD~1** - Esse comando diz extamente o seguinte: encontre o último commit e desfaça o commit anterior. Caso seja mudado o número para 2, por exemplo, ele vai desfazer os últimos 2 commits anteriores ao HEAD e assim por diante;

Esses comandos mencionados acima apenas desfazem os commits mas não alteram os estados dos arquivos. Para fazê-lo existem outras maneiras, dentre elas existem as flags --soft e --mixed.

* **git reset 'file.ext'** - Remove o arquivo do Stage colocando-o novamente no estado de untracked ou modified. Caso a alteração no arquivo já tenha sido commitada, esse comando não funciona;
* **git reset --soft 'iniciais da HASH'** - Desfaz o commit e retorna o arquivo ao stage, sem apagar do arquivo nenhuma alteração feita. Para isso, deve-se informar o HASH anterior ao commit que se deseja desfazer. Essa opção também pode ser usada para casos em que seja necessário reescrever o comentário sobre as mudanças feitas. 
Obs.: Quando é necessário desfazer dois ou mais commits através desse comando, o git conserva as modificações "na fila" exatamente como foram realizadas nos commits desfeitos. Ex.: Ao retornar dois commits, o git mantém no stage, prontas pra serem commitadas, as alterações feitas depois commit do HASH informado, e mantém fora do stage, porém também inalteradas, as modificações do último commit realizado. Isso possibilita alterar somente o comentário dos commits, sem modificar o histórico das alterações. Basta que seja feito o commit com a mensagem corrigida, uma nova adição ao stage e por fim o último commit (exatamente nessa ordem), garantindo assim o histórico anterior inalterado e as correções devidas nos comentários;
* **git reset --mixed 'iniciais da HASH'** - Este é o comportamento padrão do comando **git reset** caso seja utilizado sem as flags mencionadas. Ele desfaz o(s) commit(s) e retorna o arquivo ao aos estados *modified* ou *unteacked*, ou seja, antes de ser adicionado ao stage. Assim como o soft, não apaga do arquivo as alterações feitas. Essa opção pode ser usada para casos em seja necessário revisar ou refazer as alterações e/ou adições que possam estar incorretas;

Já a flag *__--hard__* Desfaz o commit e apaga todas as modificações daquele commit. Deve ser utilizado com muito cuidado pois arquivos podem ser destruídos, afetando todos os usuários que trabalham nesse repositório. É executado da seguinte maneira:

* **git reset --hard 'iniciais da HASH'**.



### **git revert**

Esse comando afeta somente os commits e os arquivos, sem alterar os estados dos arquivos. Ele reverte as alterações realizadas no commit informado sem apagar o histórico de commits, para isso ele cria outro commit e armazena as informações do commit desfeito, como HASH e arquivos afetados. Isso pode apagar arquivos, caso um novo arquivo tenha sido adicionado no commit desfeito. Ele pode ser útil quando um determinado commit precisa ser desfeito mas o usuário deseja manter as informações das alterações daquele commit. Pode ser usado das seguintes formas:

* **git revert 'iniciais da HASH'** - Revert o commit mencionado;
* **git revert HEAD~1** - funciona exatamente como o reset HEAD~1.

### **git stash**

Pode ser necessário transitar entre as branchs do seu repositorio local. Ao mudar de branch, todos os arquivos modificados e tudo que foi adicionado ao stage da branch anterior é adicionado à branch acessada. Isso pode ser um problema em casos em que determinados arquivos de uma branch não devem ser adicionados à nenhuma outra. Para evitar situações como essa podemos usar o git stash. Esse é um comando muito conveniente também em situações onde o usuário faz alterações em algum arquivo local e precisa pausar essas alterações para fazer um pull e atualizar o repositório local. Ele funciona como um array, em que o último stash é posicionado no índice zero e "empurra" os anteriores para o próximo índice, indo de zero a infinito. Veja abaixo as opções para uso desse comando

* **git stash** - remove temporariamente as alterações salvas em um arquivo, reservando-as em "standby", aguardando o momento certo de serem reaplicadas ao arquivo editado. Isso evita possíveis conflitos em repositórios desatualizados (por qualquer motivo que seja...) quando o usuário aplica um *git pull*, sem que se perca toda evolução do trabalho já realizado antes da atualização do repositório;
* **git stash apply** - "devolve" ao arquivo as alterações que estavam em standby;
* **git stash list** - lista todos os stashs criados, identificando em qual branch foi originado;
* **git stash clear** - limpa todos os stashs criados. Pode ser usado após aplicar as alterações que estavam guardadas;
* **git stash pop 1** (o número 1 representa o índice que você desejar) - remove arquivos do stash definindo pelo índice desejado.

Ao criar um ou vários stashs e acessar outra branch, pode ser que demore até que se possa retornar ao que estava sendo feito e foi salvo no stash. Nesses casos, existe a possibilidade de darmos um contexto à stash criada:
*git stash save "Texto informando o que estava fazendo antes de adicionar o arquivo ao stash"*.


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
* **git push origin --tags** - subir as tags criadas para o repositório remoto;
* **git tag -d 'versao-que-desejar'** - deleta a tag informada do repositório local;
* **git push origin :'versao-que-desejar'** - deleta do repositório remoto a tag informada.
