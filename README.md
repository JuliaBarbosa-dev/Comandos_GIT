# git-introducao

## Introdução ao Uso do GIT

### Sua Identidade
A primeira coisa que você deve fazer após instalar o Git é definir o seu nome de usuário e 
endereço de e-mail. Isso é muito importante porque todos os commits no Git utilizam essas 
informações que são anexadas nos commits que você realiza. Veja exemplo com meu nome e e-mail abaixo:

    git config --global user.name "Julia Barbosa"
    git config --global user.email "juliabarbosa@gmail.com"
    
Você só precisará fazer isso uma vez (opção --global), pois o Git sempre usará essa informação para 
qualquer comando git que você use no sistema.  

### Verificando Suas Configurações
Caso você queira verificar suas configurações, você pode utilizar o comando git config --list para listar todas as configurações que o Git encontrar num dado momento:

    git config --list
    
### Obtendo Ajuda
Caso você precise de ajuda usando o Git, exitem três formas de se obter ajuda das páginas de manual (manpage) para quaisquer comandos do Git. A forma mais simples é digitar :

    git help <verbo>  
    
Exemplo

    git help status
    
## Obtendo um Repositório Git
Você pode obter um projeto Git utilizando duas formas diferentes. 
1. A primeira faz uso de um projeto ou diretório existente e o importa para o Git. 
2. A segunda clona um repositório Git existente a partir de outro servidor, por exemplo, [github.com](http://github.com).

Segue abaixo uma descrição das duas opções: 

## Opção 1

### Inicializando um Repositório em um Diretório Existente
Caso você esteja iniciando o monitoramento de um projeto existente com Git, você precisa ir para o diretório do projeto e digitar

    git init
    
Isso cria um novo subdiretório chamado .git que contem todos os arquivos necessários de seu repositório — um esqueleto de repositório Git. Neste ponto, nada em seu projeto é monitorado. (Veja o Capítulo 9 para maiores informações sobre quais arquivos estão contidos no diretório .git que foi criado.)

Caso você queira começar a controlar o versionamento dos arquivos existentes (diferente de um diretório vazio), você provavelmente deve começar a monitorar esses arquivos e fazer um commit inicial. Você pode realizar isso com poucos comandos git add que especificam quais arquivos você quer monitorar, seguido de um commit:

    touch README.md
    vi README.md

    git add *.html
    git add README.md
    git commit -m 'versão Inicial do meu projeto'
    
Suponha que você tenha criado um Repositório no GitHub para seu projeto. Suponha que o repositório se chame `git-introducao` 

Neste caso o comando abaixo irá enviar as alterações objeto do commit para o repositório remoto.

    git remote add origin https://github.com/julia-barbosa/git-introducao.git
    git push -u origin master

Bem, nós iremos repassar esses comandos mais a frente. Neste ponto, você tem um repositório Git com um README.md e arquivos HTML monitorados em um commit inicial. Além disso os arquivos "comitados" estão armazenados seguramente em servidor remoto.

## Opcão 2

### Clonando um Repositório Existente
Caso você queira copiar um repositório Git já existente — por exemplo, um projeto que você queira contribuir — o comando necessário é git clone. Caso você esteja familiarizado com outros sistemas VCS, tais como Subversion, você perceberá que o comando é clone e não checkout. Essa é uma diferença importante — Git recebe uma cópia de quase todos os dados que o servidor possui. Cada versão de cada arquivo no histórico do projeto é obtida quando você roda git clone. De fato, se o disco do servidor ficar corrompido, é possível utilizar um dos clones em qualquer cliente para reaver o servidor no estado em que estava quando foi clonado (você pode perder algumas características do servidor, mas todos os dados versionados estarão lá — veja o Capítulo 4 para maiores detalhes).

Você clona um repositório com git clone [url]. Por exemplo, caso você queria clonar a biblioteca Git do Ruby chamada Grit, você pode fazê-lo da seguinte forma:

    git clone https://github.com/joao-parana/git-introducao.git
Isso cria um diretório chamado grit, inicializa um diretório .gitdentro deste, obtém todos os dados do repositório e verifica a cópia atual da última versão. Se você entrar no novo diretório grit, você verá todos os arquivos do projeto nele, pronto para serem editados ou utilizados. Caso você queira clonar o repositório em um diretório diferente de grit, é possível especificar esse diretório utilizando a opção abaixo:

    git clone https://github.com/joao-parana/git-introducao.git meuEstudoGit
    
Este comando faz exatamente a mesma coisa que o anterior, mas o diretório alvo será chamado `meuEstudoGit`.

O Git possui diversos protocolos de transferência que você pode utilizar. O exemplo anterior utiliza o protocolo https://, mas você também pode usar git(s):// ou user@server:/path.git, que utiliza o protocolo de transferência SSH. 

### Gravando Alterações no Repositório
Você tem um repositório Git e um checkout ou cópia funcional dos arquivos para esse projeto. Você precisa fazer algumas mudanças e fazer o commit das partes destas mudanças em seu repositório cada vez que o projeto atinge um estado estavel no qual você queira gravar. Por exemplo, após implementar alguma funcionalidade nova e testa-la com sucesso.

Lembre-se que cada arquivo em seu diretório de trabalho pode estar em um de dois estados: 

* monitorado 
* não monitorado 

Arquivos monitorados são arquivos que estavam no último snapshot (fotografia); podendo estar inalterados, 
modificados ou selecionados. 

Arquivos não monitorados são todo o restante — qualquer arquivo em seu diretório de trabalho que não 
estava no último snapshot e também não estão em sua área de seleção. 

Quando um repositório é inicialmente clonado, todos os seus arquivos estarão monitorados e 
inalterados porque você simplesmente os obteve e ainda não os editou.

Conforme você edita esses arquivos, o Git passa a vê-los como modificados, porque você os alterou desde seu último commit.

Você seleciona esses arquivos modificados e então faz o commit de todas as alterações selecionadas. 
Este ciclo se repete indefinidamente. Este ciclo é apresentado na abaixo.

### Verificando o Status de Seus Arquivos
A principal ferramenta utilizada para determinar quais arquivos estão em quais estados é o comando `git status`. 
Se você executar este comando diretamente após uma clonagem, você deverá ver algo similar a isso:

    git status
    
    On branch master
    Your branch is up-to-date with 'origin/master'.
    nothing to commit, working directory clean
    
Isso significa que você tem um diretório de trabalho limpo — em outras palavras, não existem arquivos 
monitorados e modificados. Git também não encontrou qualquer arquivo não monitorado, caso contrário eles seriam listados aqui. Por fim, o comando lhe mostra em qual branch você se encontra. Por enquanto, esse sempre é o master, que é o padrão; você não deve se preocupar com isso. No próximo capítulo nós vamos falar sobre branches e referências em detalhes.

Vamos supor que você adicione um novo arquivo no seu projeto, um simples arquivo 404.html. Caso o arquivo não exista e você execute git status, você verá o arquivo não monitorado dessa forma:

    cat 404.html
    git status 
    On branch master 
    Untracked files:
    (use "git add <file>..." to include in what will be committed)
    404.html
    nothing added to commit but untracked files present (use "git add" to track)
    
Você pode ver que o seu novo arquivo 404.html não está sendo monitorado, pois está listado sob o cabeçalho "Untracked files" na saída do comando status. Não monitorado significa basicamente que o Git está vendo um arquivo que não existia na última captura (commit); o Git não vai incluí-lo nas suas capturas de commit até que você o diga explicitamente que assim o faça. Ele faz isso para que você não inclua acidentalmente arquivos binários gerados, ou outros arquivos que você não têm a intenção de incluir. 

Digamos, que você queira incluir o arquivo 404.html, portanto vamos começar a monitorar este arquivo.

### Monitorando Novos Arquivos
Para passar a monitorar um novo arquivo, use o comando `git add`. Para monitorar o arquivo 404.html, você pode rodar isso:

    git add 404.html
    
Se você rodar o comando status novamente, você pode ver que o seu arquivo 404.html agora está sendo monitorado e está selecionado.

Você pode dizer que ele está selecionado pois está sob o cabeçalho “Changes to be committed”. Se você commitar neste ponto, a versão do arquivo no momento em que você rodou o comando git add é a que estará na captura (snapshot) do histórico. 
Você deve se lembrar que quando rodou o comando git init anteriormente, logo em seguida rodou o comando git add (arquivos) — fez isso para passar a monitorar os arquivos em seu diretório. O comando git add recebe um caminho de um arquivo ou diretório; se é de um diretório, o comando adiciona todos os arquivos do diretório **recursivamente**.

### Selecionando Arquivos Modificados
Vamos alterar um arquivo que já está sendo monitorado. Se você alterar um aquivo previamente monitorado chamado index.html e então rodar o comando status novamente, você terá algo semelhante a:

    git status 
    . . . 
    Changes not staged for commit: 
    (use "git add <file>..." to update what will be committed)
     
     modified:   index.html
     
O arquivo index.html aparece sob a seção chamada “Changes not staged for commit” — que significa que um arquivo monitorado foi modificado no diretório de trabalho, mas ainda não foi selecionado (staged). Para selecioná-lo, utilize o comando `git add` (é um comando com várias funções — você o utiliza para monitorar novos arquivos, selecionar arquivos, e para fazer outras coisas como marcar como resolvido aquivos com conflito). 

Agora vamos rodar o comando git add para selecionar o arquivo index.html, e então rodar git status novamente:

    git add index.html
    git status 
    
Ambos os arquivos estão selecionados e serão consolidados no seu próximo commit. Neste momento, vamos supor que você lembrou de uma mudança que queria fazer no arquivo index.html antes de commitá-lo. Você o abre novamente e faz a mudança, e então está pronto para commitar. No entanto, rode git status mais uma vez para ver o status dos arquivos do ponto de vista do GIT:

    vi index.html
    git status
    
Observe que agora o arquivo index.html aparece listado como selecionado e não selecionado. 
Como isso é possível? Acontece que o Git seleciona um arquivo exatamente como ele era quando o comando git add foi executado. Se você fizer o commit agora, a versão do index.html como estava na última vez que você rodou o comando git add é que será incluída no commit e não a versão do arquivo que estará no seu diretório de trabalho quando rodar o comando git commit. Se você modificar um arquivo depois que rodou o comando git add, **terá de rodar o git add de novo** para selecionar a última versão do arquivo:

    git add index.html
    git status
    
Poemos agora fazer o commit das alterações.

    git commit -m "Alteração no index.html e adicionado tratamento de erro para o codigo HTTP 404"
    
### Ignorando Arquivos
Muitas vezes, você terá uma classe de arquivos que não quer que o Git automaticamente adicione ou mostre como arquivos não monitorados. Normalmente estes arquivos são gerados automaticamente como arquivos de log ou produzidos pelo seu sistema de build. Nestes casos, você pode criar um arquivo contendo uma lista de padrões a serem checados chamado .gitignore. Eis um exemplo de arquivo .gitignore:

    cat .gitignore
    *.[oa]
    *~

A primeira linha fala para o Git ignorar qualquer arquivo finalizado em .o ou .a — arquivos objetos e archive (compactados) que devem ter produto da construção (build) de seu código. A segunda linha fala para o Git ignorar todos os arquivos que terminam com um til (~), os quais são utilizados por muitos editores de texto para marcar arquivos temporários. Você também pode incluir um diretório log, tmp ou pid; documentação gerada automaticamente; e assim por diante. 

Configurar um arquivo .gitignore antes de começar a trabalhar, normalmente é uma boa prática, pois evita que você commite acidentalmente arquivos que não deveriam ir para o seu repositório Git. Por exemplo, você não gostaria que sua senha de acesso ao database que está num arquivo de configuração seja publicado.

As regras para os padrões que você pode pôr no arquivo `.gitignore` são as seguintes:

* Linhas em branco ou iniciando com # são ignoradas.
* Padrões glob comuns funcionam.
* Você pode terminar os padrões com uma barra (/) para especificar diretórios.
* Você pode negar um padrão ao iniciá-lo com um ponto de exclamação (!).

Padrões glob são como expressões regulares simples que os shells usam. Um asterísco (*) significa zero ou mais caracteres; [abc] condiz com qualquer um dos caracteres de dentro dos colchetes (nesse caso, a, b, ou c); um ponto de interrogação (?) condiz com um único caractere; e os caracteres separados por hífen dentro de colchetes ([0-9]) condizem à qualquer um dos caracteres entre eles (neste caso, de 0 à 9).

Segue um outro exemplo de arquivo .gitignore:

    # um comentário começa com tralha - isto é ignorado
    # sem arquivos terminados em .a
    *.a
    # mas rastreie lib.a, mesmo que você tenha ignorado arquivos terminados em .a acima
    !lib.a
    # apenas ignore o arquivo TODO na raiz, não o subdiretório TODO
    /TODO
    # ignore todos os arquivos no diretório build/
    build/
    # ignore doc/notes.txt mas, não ignore doc/server/arch.txt
    doc/*.txt

### Visualizando Suas Mudanças Selecionadas e Não Selecionadas
Se o comando git status for muito vago — você quer saber exatamente o que você alterou, não apenas quais arquivos foram alterados — você pode utilizar o comando git diff. Nós trataremos o comando git diff em mais detalhes posteriormente; mas provavelmente você vai utilizá-lo com frequência para responder estas duas perguntas: O que você alterou, mas ainda não selecionou (stage)? E o que você selecionou, que está para ser commitado? Apesar do comando git status responder essas duas perguntas de maneira geral, o git diff mostra as linhas exatas que foram adicionadas e removidas — o patch, por assim dizer.

Vamos dizer que você edite e selecione o arquivo README.md de novo e então edite o arquivo index.html sem selecioná-lo. Você poderá  rodar o comando status para ver o que ocorre

    git status


Você pode ver também o que alterou mas ainda não selecionou, digitando o comando git diff sem nenhum argumento:

    git diff
    
Este comando compara o que está no seu diretório de trabalho com o que está na sua área de seleção (staging). O resultado te mostra as mudanças que você fez que ainda não foram selecionadas.

Se você quer ver o que selecionou que irá no seu próximo commit, pode utilizar `git diff --cached` ou `git diff --staged`, que é mais fácil de lembrar. Este comando compara as mudanças selecionadas com o seu último commit:

    git diff --staged 
    
    
É importante notar que o git diff por si só não mostra todas as mudanças desde o último commit — apenas as mudanças que ainda não foram selecionadas. Isso pode ser confuso, pois se você selecionou todas as suas mudanças, git diff não te dará nenhum resultado.

Como um outro exemplo, se você selecionar o arquivo index.html e então editá-lo, você pode utilizar o git diff para ver as mudanças no arquivo que estão selecionadas, e as mudanças que não estão:

    git add index.html
    echo '# test line' >> index.html
    git status
    On branch master
    
    Changes to be committed:
    
    modified:   index.html
    
    Changes not staged for commit:
    
    modified:   index.html
    
    
Agora você pode utilizar o git diff para ver o que ainda não foi selecionado:

    git diff
    git diff --cached
    
### Fazendo Commit de Suas Mudanças
Agora que a sua área de seleção está do jeito que você quer, você pode fazer o commit de suas mudanças. Lembre-se que tudo aquilo que ainda não foi selecionado — qualquer arquivo que você criou ou modificou que você não tenha rodado o comando git add desde que editou — não fará parte deste commit. Estes arquivos permanecerão como arquivos modificados em seu disco. Neste caso, a última vez que você rodou git status, viu que tudo estava selecionado, portanto você está pronto para fazer o commit de suas mudanças. O jeito mais simples é digitar git commit:

    git commit
    
Ao fazer isso, seu editor de escolha é acionado. (Isto é configurado através da variável de 
ambiente $EDITOR de seu shell - normalmente vim ou emacs, apesar de poder ser configurado 
o que você quiser utilizando o comando `git config --global` core.editor  

O editor mostra um texto e espera que você digite uma mensagem.

Você pode remover a mensagem Default e digitar sua mensagem de commit adequada.

Alternativamente, você pode digitar sua mensagem de commit junto ao comando commit ao especificá-la após a flag -m, assim:

    git commit -m "Corrigindo BUG 137"
    
Agora você acabou de criar o seu commit observe que o git te mostrou uma saída informando qual o branch que recebeu o commit (master), qual o checksum SHA-1 que o commit teve (463dc4f), quantos arquivos foram alterados, e estatísticas a respeito das linhas adicionadas e removidas no commit.

Lembre-se que o commit grava a captura da área de seleção. Qualquer coisa que não foi selecionada ainda permanece lá modificada; você pode fazer um outro commit para adicioná-la ao seu histórico. Toda vez que você faz um commit, está gravando a captura do seu projeto o qual poderá reverter ou comparar posteriormente.

### Pulando a Área de Seleção
Embora possa ser extraordinariamente útil para a elaboração de commits exatamente como você deseja, a área de seleção às vezes é um pouco mais complexa do que você precisa no seu fluxo de trabalho. Se você quiser pular a área de seleção, o Git provê um atalho simples. Informar a opção -a ao comando git commit faz com que o Git selecione automaticamente cada arquivo que está sendo monitorado antes de realizar o commit, permitindo que você pule a parte do git add:

    git commit -a -m 'Corrigindo BUG 137'
    
Note que, neste caso, você não precisa rodar o git add no arquivo index.html antes de fazer o commit.

### Removendo Arquivos
Para remover um arquivo do Git, você tem que removê-lo dos arquivos que estão sendo monitorados (mais precisamente, removê-lo da sua área de seleção) e então fazer o commit. O comando git rm faz isso e também remove o arquivo do seu diretório para você não ver ele como arquivo não monitorado (untracked file) na próxima vez.

Se você simplesmente remover o arquivo do seu diretório, ele aparecerá em “Changes not staged for commit” (isto é, fora da sua área de seleção ou unstaged) na saida do seu git status:

    rm lixo.txt
    git status

Em seguida, se você rodar git rm, a remoção do arquivo é colocada na área de seleção:

    git rm lixo.txt 
    git status
    
Na próxima vez que você fizer o commit, o arquivo sumirá e não será mais monitorado. Se você modificou o arquivo e já o adicionou na área de seleção, você deve forçar a remoção com a opção -f. Essa é uma funcionalidade de segurança para prevenir remoções acidentais de dados que ainda não foram gravados em um snapshot e não podem ser recuperados do Git.

Outra coisa útil que você pode querer fazer é manter o arquivo no seu diretório, mas apagá-lo da sua área de seleção. Em outras palavras, você quer manter o arquivo no seu disco rígido mas não quer que o Git o monitore mais. Isso é particularmente útil se você esqueceu de adicionar alguma coisa no seu arquivo .gitignore e acidentalmente o adicionou, como um grande arquivo de log ou muitos arquivos .a compilados. Para fazer isso, use a opção --cached:

    git rm --cached meu-site.log
    
Você pode passar arquivos, diretórios, e padrões de nomes de arquivos para o comando git rm. Isso significa que você pode fazer coisas como:

    git rm log/\*.log
Note a barra invertida (\) na frente do *. Isso é necessário pois o Git faz sua própria expansão no nome do arquivo além da sua expansão no nome do arquivo no shell. Esse comando remove todos os arquivos que tem a extensão .log no diretório log/. Ou, você pode fazer algo como isso:

    git rm \*~
    
Esse comando remove todos os arquivos que terminam com ~.

### Movendo Arquivos
O Git não monitora explicitamente arquivos movidos. Se você renomeia um arquivo, nenhum metadado é armazenado no Git que identifique que você renomeou o arquivo. No entanto, o Git é inteligente e tenta descobrir isso depois do fato ocorrido.

É um pouco confuso que o Git tenha um comando mv. Se você quiser renomear um arquivo no Git, você pode fazer isso com

    git mv arquivo_origem arquivo_destino
    
e funciona. De fato, se você fizer algo desse tipo e consultar o status, você verá que o Git considera que o arquivo foi renomeado:

    git mv README.txt README
    git status
 
No entanto, isso é equivalente a rodar algo como:

    mv README.txt README
    git rm README.txt
    git add README
    
O Git descobre que o arquivo foi renomeado implicitamente, então ele não se importa se você renomeou por este caminho ou com o comando mv. A única diferença real é que o comando mv é mais conveniente, executa três passos de uma vez. 

O mais importante, você pode usar qualquer ferramenta para renomear um arquivo, e usar add/rm depois, antes de consolidar com o commit.

### Visualizando o Histórico de Commits
Depois que você tiver criado vários commits, ou se clonou um repositório com um histórico de commits existente, você provavelmente vai querer ver o que aconteceu. A ferramente mais básica e poderosa para fazer isso é o comando `git log`.

Estes exemplos usam um projeto muito simples chamado simplegit, que eu frequentemente uso para demonstrações. Para pegar o projeto, execute:

git clone git://github.com/schacon/simplegit-progit.git
Quando você executar git log neste projeto para ver a saida.

    git log
    
Por padrão, sem argumentos, git log lista os commits feitos naquele repositório em ordem cronológica reversa. Isto é, os commits mais recentes primeiro. Como você pode ver, este comando lista cada commit com seu checksum SHA-1, o nome e e-mail do autor, a data e a mensagem do commit.

Um grande número e variedade de opções para o comando git log estão disponíveis para mostrá-lo exatamente o que você quer ver. Aqui, nós mostraremos algumas das opções mais usadas.

Uma das opções mais úteis é -p, que mostra o diff introduzido em cada commit. Você pode ainda usar -2, que limita a saída somente às duas últimas entradas.

    git log -p -2
    
Esta opção mostra a mesma informação, mas com um diff diretamente seguido de cada entrada. Isso é muito útil para revisão de código ou para navegar rapidamente e saber o que aconteceu durante uma série de commits que um colaborador adicionou. Você pode ainda usar uma série de opções de sumarização com git log. 

Por exemplo, se você quiser ver algumas estatísticas abreviadas para cada commit, você pode usar a opção --stat

    git log --stat
    
Como você pode ver, a opção --stat imprime abaixo de cada commit uma lista de arquivos modificados, quantos arquivos foram modificados, e quantas linhas nestes arquivos foram adicionadas e removidas. Ele ainda mostra um resumo destas informações no final. Outra opção realmente útil é --pretty. Esta opção muda a saída do log para outro formato que não o padrão. Algumas opções pré-construídas estão disponíveis para você usar. A opção oneline mostra cada commit em uma única linha, o que é útil se você está olhando muitos commits. Em adição, as opções short, full e fuller mostram a saída aproximadamente com o mesmo formato, mas com menos ou mais informações, respectivamente:

    git log --pretty=oneline

A opção mais interessante é format, que permite que você especifique seu próprio formato de saída do log. Isto é especialmente útil quando você está gerando saída para análise automatizada (parsing) — porque você especifica o formato explicitamente, você sabe que ele não vai mudar junto com as atualizações do Git:

    git log --pretty=format:"%h - %an, %ar : %s"

As opções oneline e format são particularmente úteis com outra opção chamada --graph. Esta opção gera um agradável gráfico ASCII mostrando seu branch e histórico de merges, que nós podemos ver em nossa cópia do repositório do projeto Grit:

    git log --pretty=format:"%h %s" --graph
    * 2d3acf9 ignore errors from SIGCHLD on trap
    *  5e3ee11 Merge branch 'master' of git://github.com/dustin/grit
    |\
    | * 420eac9 Added a method for getting the current branch.
    * | 30e367c timeout code and tests
    * | 5a09431 add timeout protection to grit
    * | e1193f8 support for heads with slashes in them
    |/
    * d6016bc require time for xmlschema
    *  11d191e Merge branch 'defunkt' into local
    
Estas são apenas algumas opções de formatação de saída do git log — há muito mais

### Limitando a Saída de Log
Em adição às opções de formatação, git log tem inúmeras opções de limitações úteis — que são opções que lhe deixam mostrar somente um subconjunto de commits. Você já viu algumas — a opção -2, que mostra apenas os dois últimos commits. De fato, você pode fazer -<n>, onde n é qualquer inteiro para mostrar os últimos n commits. Na verdade, você provavelmente não usará isso frequentemente, porque por padrão o Git enfileira toda a saída em um paginador, e então você vê somente uma página da saída do log por vez.

No entanto, as opções de limites de tempo como --since e --until são muito úteis. Por exemplo, este comando pega a lista de commits feitos nas últimas duas semanas:

    git log --since=2.weeks
    

## Desfazendo Coisas
Em qualquer fase, você pode querer desfazer alguma coisa. Aqui, veremos algumas ferramentas básicas para desfazer modificações que você fez. Cuidado, porque você não pode desfazer algumas dessas mudanças. Essa é uma das poucas áreas no Git onde você pode perder algum trabalho se fizer errado.

###Modificando Seu Último Commit
Uma das situações mais comuns para desfazer algo, acontece quando você faz o commit muito cedo e possivelmente esqueceu de adicionar alguns arquivos, ou você bagunçou sua mensagem de commit. Se você quiser tentar fazer novamente esse commit, você pode executá-lo com a opção --amend:

$ git commit --amend
Esse comando pega sua área de seleção e a utiliza no commit. Se você não fez nenhuma modificação desde seu último commit (por exemplo, você rodou esse comando imediatamente após seu commit anterior), seu snapshot será exatamente o mesmo e tudo que você mudou foi sua mensagem de commit.

O mesmo editor de mensagem de commits abre, mas ele já tem a mensagem do seu commit anterior. Você pode editar a mensagem como sempre, mas ela substituirá seu último commit.

Por exemplo, se você fez um commit e esqueceu de adicionar na área de seleção as modificações de um arquivo que gostaria de ter adicionado nesse commit, você pode fazer algo como isso:

     git commit -m 'initial commit'
     git add forgotten_file
     git commit --amend
     
Depois desses três comandos você obterá um único commit — o segundo commit substitui os resultados do primeiro.


### Tirando um arquivo da área de seleção

As duas próximas seções mostram como trabalhar nas suas modificações na área de seleção e diretório de trabalho. A parte boa é que o comando que você usa para ver a situação nessas duas áreas também lembra como desfazer suas alterações. Por exemplo, vamos dizer que você alterou dois arquivos e quer fazer o commit deles como duas modificações separadas, mas você acidentalmente digitou git add * e colocou os dois na área de seleção. Como você pode retirar um deles? O comando git status lembra você:

      git add .
      git status
       On branch master
       Changes to be committed:
         (use "git reset HEAD <file>..." to unstage)

             modified:   README.txt
             modified:   benchmarks.rb
  

Logo abaixo do texto “Changes to be committed”, ele diz use git reset HEAD <file>... to unstage ("use git reset HEAD <file>... para retirá-los do estado unstaged"). Então, vamos usar esse conselho para retirar o arquivo benchmarks.rb:

    git reset HEAD benchmarks.rb
    benchmarks.rb: locally modified
    git status
     On branch master
     Changes to be committed:
       (use "git reset HEAD <file>..." to unstage)
    
           modified:   README.txt
    
     Changes not staged for commit:
       (use "git add <file>..." to update what will be committed)
       (use "git checkout -- <file>..." to discard changes in working directory)
    
           modified:   benchmarks.rb
    
    
O comando é um pouco estranho, mas funciona. O arquivo benchmarks.rb está modificado, mas, novamente fora da área de seleção.

### Desfazendo um Arquivo Modificado
E se você perceber que não quer manter suas modificações no arquivo benchmarks.rb? Como você pode facilmente desfazer isso — revertê-lo para o que era antes de fazer o último commit (ou do inicio do clone, ou seja la como você o conseguiu no seu diretório de trabalho)? Felizmente, git status diz a você como fazer isso, também. Na saída do último exemplo, a área de trabalho se parecia com isto:

     Changes not staged for commit:
       (use "git add <file>..." to update what will be committed)
       (use "git checkout -- <file>..." to discard changes in working directory)
    
           modified:   benchmarks.rb
    
    
Ele diz explicitamente como descartar as modificações que você fez (pelo menos, as novas versões do Git, 1.6.1 em diante, fazem isso — se você tem uma versão mais antiga, uma atualização é altamente recomendável para ter alguns desses bons recursos de usabilidade). Vamos fazer o que ele diz:

     git checkout -- benchmarks.rb
     git status
     On branch master
     Changes to be committed:
       (use "git reset HEAD <file>..." to unstage)
    
           modified:   README.txt
    
    
Você pode ver que as alterações foram revertidas. Perceba também que esse comando é perigoso: qualquer alteração que você fez nesse arquivo foi desfeita — você acabou de copiar outro arquivo sobre ele. Nunca use esse comando a menos que você tenha certeza absoluta que não quer o arquivo. Se você só precisa tirá-lo do caminho, vamos falar sobre stash e branch no próximo capítulo; geralmente essas são maneiras melhores de agir.

Lembre-se, qualquer coisa que foi incluída com um commit no Git quase sempre pode ser recuperada. Até mesmo commits que estavam em branches que foram apagados ou commits que foram sobrescritos com um commit --amend podem ser recuperados (consulte o Capítulo 9 para recuperação de dados). No entanto, qualquer coisa que você perder que nunca foi commitada, provavelmente nunca mais será vista novamente.   


## Trabalhando com Remotos
Para ser capaz de colaborar com qualquer projeto no Git, você precisa saber como gerenciar seus repositórios remotos. Repositórios remotos são versões do seu projeto que estão hospedados na Internet ou em uma rede em algum lugar. Você pode ter vários deles, geralmente cada um é somente leitura ou leitura/escrita pra você. Colaborar com outros envolve gerenciar esses repositórios remotos e fazer o push e pull de dados neles quando você precisa compartilhar trabalho. Gerenciar repositórios remotos inclui saber como adicionar repositório remoto, remover remotos que não são mais válidos, gerenciar vários branches remotos e defini-los como monitorados ou não, e mais. Nesta seção, vamos cobrir essas habilidades de gerenciamento remoto.

### Exibindo Seus Remotos
Para ver quais servidores remotos você configurou, você pode executar o comando git remote. Ele lista o nome de cada remoto que você especificou. Se você tiver clonado seu repositório, você deve pelo menos ver um chamado origin — esse é o nome padrão que o Git dá ao servidor de onde você fez o clone:

     git clone git://github.com/schacon/ticgit.git
     cd ticgit
     git remote

Você também pode especificar -v, que mostra a URL que o Git armazenou para o nome do remoto:

     git remote -v

Se você tem mais de um remoto, o comando lista todos. Por exemplo, faça um teste com o repositório Grit.

     cd grit
     git remote -v
     
Isso significa que podemos puxar contribuições de qualquer um dos usuários muito facilmente. Mas note que somente o remoto origin é uma URL SSH, sendo o único pra onde eu posso fazer o push.

### Adicionando Repositórios Remotos
Eu mencionei e dei algumas demonstrações de adição de repositórios remotos nas seções anteriores, mas aqui está como fazê-lo explicitamente. Para adicionar um novo repositório remoto no Git com um nome curto, para que você possa fazer referência facilmente, execute git remote add [nomecurto] [url]:

     git remote
     git remote add pb git://github.com/paulboone/ticgit.git
     git remote -v
 
Agora você pode usar a string pb na linha de comando em lugar da URL completa. Por exemplo, se você quer fazer o fetch de todos os dados de Paul que você ainda não tem no seu repositório, você pode executar git fetch pb:

     git fetch pb 
     
O branch master de Paul é localmente acessível como pb/master — você pode fazer o merge dele em um de seus branches, ou fazer o check out de um branch local a partir deste ponto se você quiser inspecioná-lo.

### Fazendo o Fetch e Pull de Seus Remotos
Como você acabou de ver, para pegar dados dos seus projetos remotos, você pode executar:

     git fetch [nome-remoto]
     
Esse comando vai até o projeto remoto e pega todos os dados que você ainda não tem. Depois de fazer isso, você deve ter referências para todos os branches desse remoto, onde você pode fazer o merge ou inspecionar a qualquer momento. (Vamos ver o que são branches e como usá-los mais detalhadamente no Capítulo 3.)

Se você clonar um repositório, o comando automaticamente adiciona o remoto com o nome origin. Então, git fetch origin busca qualquer novo trabalho que foi enviado para esse servidor desde que você o clonou (ou fez a última busca). É importante notar que o comando fetch traz os dados para o seu repositório local — ele não faz o merge automaticamente com o seus dados ou modifica o que você está trabalhando atualmente. Você terá que fazer o merge manualmente no seu trabalho quando estiver pronto.

Se você tem um branch configurado para acompanhar um branch remoto (veja a próxima seção e o Capítulo 3 para mais informações), você pode usar o comando git pull para automaticamente fazer o fetch e o merge de um branch remoto no seu branch atual. Essa pode ser uma maneira mais fácil ou confortável pra você; e por padrão, o comando git clone automaticamente configura seu branch local master para acompanhar o branch remoto master do servidor de onde você clonou (desde que o remoto tenha um branch master). Executar git pull geralmente busca os dados do servidor de onde você fez o clone originalmente e automaticamente tenta fazer o merge dele no código que você está trabalhando atualmente.

### Pushing Para Seus Remotos
Quando o seu projeto estiver pronto para ser compartilhado, você tem que enviá-lo para a fonte. O comando para isso é simples: git push [nome-remoto] [branch]. Se você quer enviar o seu branch master para o servidor origin (novamente, clonando normalmente define estes dois nomes para você automaticamente), então você pode rodar o comando abaixo para enviar o seu trabalho para o sevidor:

     git push origin master
     
Este comando funciona apenas se você clonou de um servidor que você têm permissão para escrita, e se mais ninguém enviou dados no meio tempo. Se você e mais alguém clonarem ao mesmo tempo, e você enviar suas modificações após a pessoa ter enviado as dela, o seu push será rejeitado. Antes, você terá que fazer um pull das modificações deste outro alguém, e incorporá-las às suas para que você tenha permissão para enviá-las. Veja o Capítulo 3 para mais detalhes sobre como enviar suas modificações para servidores remotos.

### Inspecionando um Remoto
Se você quer ver mais informação sobre algum remoto em particular, você pode usar o comando git remote show [nome-remoto]. Se você rodar este comando com um nome específico, como origin, você verá algo assim:

     git remote show origin

Ele lista a URL do repositório remoto assim como as branches sendo rastreadas. O resultado deste comando lhe diz que se você está na branch master e rodar git pull, ele automaticamente fará um merge na branch master no remoto depois que ele fizer o fetch de todas as referências remotas. Ele também lista todas as referências remotas que foram puxadas.

Este é um simples exemplo que você talvez encontre por aí. Entretanto, quando se usa o Git pra valer, você pode ver muito mais informação vindo de git remote show:

     git remote show origin
     
Este comando mostra qual branch é automaticamente enviado (pushed) quando você roda git push em determinados branches. Ele também mostra quais branches remotos que estão no servidor e você não tem, quais branches remotos você tem e que foram removidos do servidor, e múltiplos branches que são automaticamente mesclados (merged) quando você roda git pull.

### Removendo e Renomeando Remotos
Se você quiser renomear uma referência, em versões novas do Git você pode rodar git remote rename para modificar um apelido de um remoto. Por exemplo, se você quiser renomear pb para paul, você pode com git remote rename:

     git remote rename pb paul
     git remote
 
É válido mencionar que isso modifica também os nomes dos branches no servidor remoto. O que costumava ser referenciado como pb/master agora é paul/master.

Se você quiser remover uma referência por qualquer razão — você moveu o servidor ou não está mais usando um mirror específico, ou talvez um contribuidor não está mais contribuindo — você usa git remote rm:

     git remote rm paul
     git remote
     

## Submódulos

Freqüentemente enquanto você está trabalhando em um projeto, você precisa usar um outro projeto dentro dele. Talvez seja uma biblioteca desenvolvida por terceiros ou que você está desenvolvendo separadamente e usando em vários projetos pai. Um problema comum surge nestes cenários: você quer tratar os dois projetos em separado mas ainda ser capaz de usar um dentro do outro.

Aqui vai um exemplo. Digamos que você está desenvolvendo um site e criando Atom feeds. Em vez de criar seu próprio gerador de Atom, você decide usar uma biblioteca. Provavelmente você terá que incluir esse código de uma biblioteca compartilhada, como um instalação CPAN ou Ruby gem, ou copiar o código fonte na árvore do seu projeto. O problema com a inclusão da biblioteca é que é difícil de personalizar livremente e muitas vezes difícil de fazer o deploy dela, porque você precisa ter certeza de que cada cliente tem essa biblioteca disponível. O problema com a inclusão do código no seu projeto é que é difícil de fazer o merge de qualquer alteração que você faz quando existem modificações do desenvolvedor da biblioteca.

Git resolve esses problemas usando submódulos. Submódulos permitem que você mantenha um repositório Git como um subdiretório de outro repositório Git. Isso permite que você faça o clone de outro repositório dentro do seu projeto e mantenha seus commits separados.

**ATENÇÃO:** Use submdulos com cuidado para não perder alterações quando estiver trabalhando com Branchs e Tags

### Começando com Submódulos

Digamos que você quer adicionar a biblioteca Rack (um servidor de aplicação web em Ruby) ao seu projeto, manter suas próprias alterações nela, mas continuar fazendo o merge do branch principal. A primeira coisa que você deve fazer é fazer o clone do repositório externo dentro do seu subdiretório. Você adiciona projetos externos como submódulos com o comando git submodule add:

	$ git submodule add git://github.com/chneukirchen/rack.git rack
	Initialized empty Git repository in /opt/subtest/rack/.git/
	remote: Counting objects: 3181, done.
	remote: Compressing objects: 100% (1534/1534), done.
	remote: Total 3181 (delta 1951), reused 2623 (delta 1603)
	Receiving objects: 100% (3181/3181), 675.42 KiB | 422 KiB/s, done.
	Resolving deltas: 100% (1951/1951), done.

Agora você tem um projeto do Rack no subdiretório rack dentro do seu projeto. Você pode ir nesse subdiretório, fazer alterações, adicionar seus próprios repositórios remotos para fazer o push de suas modificações, fazer o fetch e o merge do repositório original, e outras coisas. Se você execurar git status logo depois de adicionar o submódulo, você verá duas coisas:

	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#      new file:   .gitmodules
	#      new file:   rack
	#

Primeiro você percebe o arquivo .gitmodules. Esse é um arquivo de configuração que guarda o mapeamento entre a URL do projeto e o subdiretório local que você usou:

	$ cat .gitmodules
	[submodule "rack"]
		  path = rack
		  url = git://github.com/chneukirchen/rack.git
		  
Se você tem vários submódulos, você terá várias entradas nesse arquivo. É importante notar que esse arquivo está no controle de versão como os outros, como o seu arquivo .gitignore. É feito o push e pull com o resto do seu projeto. É como as outras pessoas que fazem o clone do projeto sabem onde pegar os projetos dos submódulos.

O outro ítem na saída do git status é sobre o rack. Se você executar git diff nele, você vê uma coisa interessante:

	$ git diff --cached rack
	diff --git a/rack b/rack
	new file mode 160000
	index 0000000..08d709f
	--- /dev/null
	+++ b/rack
	@@ -0,0 +1 @@
	+Subproject commit 08d709f78b8c5b0fbeb7821e37fa53e69afcf433

Apesar de rack ser um subdiretório no seu diretório de trabalho, Git vê ele como um submódulo e não rastreia seu conteúdo quando você não está no diretório. Em vez disso, Git o grava como um commit especial desse repositório. Quando você altera e faz commit nesse subdiretório, o projeto-pai nota que o HEAD mudou e grava o commit que você está atualmente; dessa forma, quando outros fizerem o clone desse projeto, eles podem recriar o mesmo ambiente.

Esse é um ponto importante sobre submódulos: você os salva como o commit exato onde eles estão. Você não pode salvar um submódulo no master ou em outra referência simbólica.

Quando você faz o commit, você vê algo assim:

	$ git commit -m 'first commit with submodule rack'
	[master 0550271] first commit with submodule rack
	 2 files changed, 4 insertions(+), 0 deletions(-)
	 create mode 100644 .gitmodules
	 create mode 160000 rack

Note o modo 160000 para a entrada do rack. Esse é um modo especial no Git que basicamente significa que você está salvando um commit como um diretório em vez de um subdiretório ou um arquivo.

Você pode tratar o diretório rack como um projeto separado e atualizar seu projeto-pai de vez em quando com uma referência para o último commit nesse subprojeto. Todos os comandos do Git funcionam independente nos dois diretórios:

	$ git log -1
	commit 0550271328a0038865aad6331e620cd7238601bb
	Author: Scott Chacon <schacon@gmail.com>
	Date:   Thu Apr 9 09:03:56 2009 -0700

		first commit with submodule rack
	$ cd rack/
	$ git log -1
	commit 08d709f78b8c5b0fbeb7821e37fa53e69afcf433
	Author: Christian Neukirchen <chneukirchen@gmail.com>
	Date:   Wed Mar 25 14:49:04 2009 +0100

    Document version change


### Fazendo Clone de um Projeto com Submódulos

Aqui você vai fazer o clone de um projeto com um submódulo dentro. Quando você recebe um projeto como este, você tem os diretórios que contêm os submódulos, mas nenhum dos arquivos ainda:

	$ git clone git://github.com/schacon/myproject.git
	Initialized empty Git repository in /opt/myproject/.git/
	remote: Counting objects: 6, done.
	remote: Compressing objects: 100% (4/4), done.
	remote: Total 6 (delta 0), reused 0 (delta 0)
	Receiving objects: 100% (6/6), done.
	$ cd myproject
	$ ls -l
	total 8
	-rw-r--r--  1 schacon  admin   3 Apr  9 09:11 README
	drwxr-xr-x  2 schacon  admin  68 Apr  9 09:11 rack
	$ ls rack/
	$
	
O diretório rack está lá, mas vazio. Você precisa executar dois comandos: git submodule init para inicializar seu arquivo local de configuração, e git submodule update para buscar todos os dados do projeto e recuperar o commit apropriado conforme descrito em seu projeto-pai:

	$ git submodule init
	Submodule 'rack' (git://github.com/chneukirchen/rack.git) registered for path 'rack'
	$ git submodule update


## Sequências úteis de comandos no GIT

Segue abaixo algumas sequências úteis de comandos para serem usadas no dia a dia.

### Configuração Global de usuário e e-mail

	git config --global user.name "Seu Nome"
	git config --global user.email seu-email@seu-provedor.com

### 1. Inicializando um repositório do Zero

	cd diretório-desejado
	git init
	echo "# Titulo do meu Repositório" >  README.md
	git add .
	git commit -m 'versão Inicial do meu projeto'

### 2. Associando a um repositório remoto e compartilhando os ativos

	git remote add origin https://github.com/seu-usuario/seu-repositorio.git
	git push -u origin master
	
### 3. Definindo o que deve ser ignorado 

	echo "*.class" > .gitignore	
	echo "*.key" >> .gitignore	
	echo "*.log" >> .gitignore	
	echo "*.jar" >> .gitignore	
	
### 4. Removendo arquivos do controle de versão

O exemplo abaixo é apenas didático. Supondo que exista o arquivo lixo.txt

	git add lixo.txt 
	rm lixo.txt
	git rm lixo.txt 
	
### 5. Remover apenas da área de seleção

Manter o arquivo no seu disco rígido mas parar de monitorar com o Git

	git rm --cached meu-arquivo.algo
	
### 6. Modificando o ultimo commit (usando opção amend)

	git commit -m 'initial commit'
	git add arquivo-esquecido
	git commit --amend
	
### 7. Sobreescrevendo tudo da área local com o conteúdo de repositório remoto

	git fetch --all
	git reset --hard origin/master
	
### 8. Atualizando com alterações remotas e fazendo upload das alterações locais

	git pull origin master
	git add -A . 
	git commit  -m "Meu comentário sobre as atualizações que estou fazendo no remoto" ; 
	git push -u origin master

### 9. Exibindo o Status 

	git status

### 10. Exibindo o LOG de alterações 

	git log
	
