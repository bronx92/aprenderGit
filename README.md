
# Comandos Git

## Veja abaixo os comandos mais básicos do Git

**git log**
 
 Esse comando é muito importante pois é com ele que podemos consultar de maneira detalhada tudo que foi feito no repositório, o que resulta na possibilidade de realizarmos o Controle de Versão. Esse comando exibe informações gerais sobre commits realizados no repositório. 

#### Opções
* *git log decorate* - Pesquisar finalidade!;
* *git log --author "Name"* - lista todos os commits do autor citado;
* *git shortlog* - lista todos os commits realizados por todos os autores de forma resumida
* *git log --graph* - mostra de forma gráfica os commits no repositório.

**git show 'HASH'**

 Esse comando mostra as modificações de forma mais detalhada em um commit específico, definido pelo HASH .

 **git diff**

Exibe (destacando em verde) as alterações salvas no arquivo antes dele ser adicionado ao stage. É uma maneira de conferir o que foi feito antes do commit. Pode ser utilizado com a opção *--name-only*, que exibe somente o nome dos aquivos modificados, o que se torna útil caso o repositório tenha uma lista grande de arquivos e seja necessário saber quais foram modificados.

**git restore 'file.ext'**

 Descarta as alterações realizadas no arquivo mencionado no comando apagando **todas** as adições feitas no arquivo. Ao usar esse comando, é necessário estar certo de que nenhuma das alterações serão aproveitadas. Quando esse comando é usado com a opção _--staged_ o arquivo apenas será removido do stage mas suas modificações reais permanecerão intactas.

**git reset**

Esse comando permite desfazer alguns comandos caso seja necessário. Para isso existem algumas opções que devem ser utilizadas para casos diferentes:

* **git reset HEAD 'file.ext'** - Remove o arquivo mencionado do stage.
* **git reset --soft 'HASH'** - Desfaz o commit desejado, retornando o arquivo ao stage. Para isso, deve-se informar o HASH para o qual se deseja retornar. 
* **git reset --mixed 'HASH'** - 
* **git reset --hard 'HASH'** - 

**git checkout 'file.ext'**

Descarta as alterações realizadas no arquivo mencionado. Tem a mesma função do *git restore 'file.ext'*.