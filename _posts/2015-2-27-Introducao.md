---
layout: post
title: Controle de versão e compartilhamento de projetos com GitHub
---

![GitHub](http://clinicalresearch.files.wordpress.com/2014/09/github2.jpg?w=468)

Hoje vou falar um pouco sobre uma metodologia de controle de versão e compartilhamento de projetos usando o Git e GitHub.

### O Problema

Você está trabalhando em algo (que envolva arquivos, geralmente o desenvolvimento de algum tipo de software, mas qualquer outro projeto que seja essencialmente edição de arquivos) numa equipe. Algumas necessidades surgem:

1. Precisamos todos compartilhar os arquivos de forma fácil, atualizável e dinâmica;
2. Precisamos manter versões dos arquivos (ou do projeto como todo) para marcar releases ou descobrir falhas, bugs e erros no projeto;
3. Precisamos manter o controle do que é alterado por cada membro da equipe afim de evitar que falhas sejam introduzidas;
4. Entretanto, precisamos ter um ambiente que permita liberdade criativa removendo o medo de introduzir falhas.


### A Solução

Antes de apresentar a solução proposta, preciso definir alguns conceitos (brevemente):


#### Software de Controle de Versão

É um software que auxilia usuários a manter versões dos seus arquivos em um determinado projeto. Esse sistema pode ser local, ou em um servidor centralizado, que permite a colaboração de várias pessoas em um só projeto e mantém o projeto longe da insegurança de um disco local pessoal.


#### Git

O Git é um software de controle de versão muito utilizado atualmente e muito poderoso. Ele pode ser usando apenas localmente mas o brilho dele está na utilização em servidores remotos. Também permite facilmente a experimentação de mudanças de forma separada do "desenvolvimento natural" do projeto com sua funcionalidade de *branching* (mais sobre isso mais tarde).  Se quiser um rápido tutorial hands-on, vá nesse link (in english): [http://try.github.com/](http://try.github.com/)


#### GitHub

O [GitHub](http://www.github.com) é uma empresa que oferece o serviço de armazenamento na nuvem de repositórios git junto com funcionalidades de inspeção, socialização e colaboração em uma interface web. Você pode criar uma conta e quantos repositórios públicos quiser gratuitamente. Para repositórios privados você precisa adquirir um plano pago, que começa a $7 por mês.


#### Setup

Usando a tecnologia Git e os recursos fornecidos pelo GitHub, nossa vida de desenvolvedor se torna muito mais fácil. Não vou mentir para vocês, aprender a usar o GitHub não é trivial mas de pouquinho em pouquinho você irá perceber como essa ferramenta é útil. Então vamos começar pelo início: você e mais alguns amigos resolveram fazer um projeto em conjunto. Não vão querer ficar trocando arquivo pelo Dropbox (ou pior: pen-driver), né?


##### 1. Criar conta no GitHub

O passo mais simples de todos. Vá para [github.com](https://github.com/), escolha um username, coloque seu e-mail e escolha uma senha, confirme pelo e-mail e pronto!


##### 2. Instalação

Se seu ambiente é Windows, baixe e instale o [GitHub for Windows](https://windows.github.com/). Você terá uma interface gráfica e o mais importante: uma linha de comando git. Pessoalmente, eu não uso a aplicação de interface gráfica pois a linha de comando e a interface web já me fornecem tudo que preciso de maneira mais rápida, prática e leve que a aplicação gráfica.

Se seu ambiente é Mac, também há o [GitHub for Mac](https://mac.github.com/). Baixe apenas se quiser a aplicação gráfica, pois o OS X 10.9 já inclui o git na sua linha de comando (Terminal).

Se seu ambiente é Linux, provavelmente já tem git instalado e não há aplicação gráfica para você.


##### 3. Criar ou *forkar* um repositório

Há duas formas de fazer isso. (Texto a escrever)

 

#### Workflow

Okay, já tenho meu projeto *forkado* (termo abrasileirado que acabei de inventar – vem de *fork*), *clonado* (baixado) na minha máquina e estou pronto para contribuir para o projeto. Como já falei anteriormente, há diversas formas de se fazer isso, então vou aqui apresentar uma das mais comuns e mais utilizadas principalmente em projetos open-source.


##### 1. Criar um *branch*

Você não quer que sua mudança/atualização/correção de bug que ainda está instável, insegura e sem revisão bagunce o código principal, não é mesmo? Para isso utiliza-se um *branch*. Idealmente um *branch* é um conjunto de alterações que fazem sentido de estarem juntas. Por exemplo: implementação de uma nova funcionalidade, correção de um bug, melhoramento de um módulo, etc. Tecnicamente falando, um *branch* nada mais é do que um ponteiro para um *[commit](#commit)*. Criar um *branch* é muito fácil:

    git branch <nome-do-branch>


Para listar os *branchs* é mais fácil ainda:

    git branch


E para trocar sua área de trabalho de um *branch* para outro:

    git checkout <nome-do-branch>
    

Se quiser trocar para um novo *branch *(isto é, criar um novo e trocar):

    git checkout -b <nome-do-branch>
    

Importante lembrar algumas coisas:

1. Geralmente o primeiro e principal *branch* de todos os projetos no Git é o *master*. Isso é apenas uma convenção seguida pela maioria, mas nada lhe impede de excluir o *master* e usar outro *branch* como principal mas não recomendo.
2. Sempre que criar um *branch* novo, este terá como base o último *[commit](#commit)* (chamado de *HEAD*) do *branch* que você está no momento.  Isso é a mesma coisa que dizer: sempre que criar um *branch* novo, este será uma cópia exata do *branch* que você está no momento. **A menos que se especifique qual *branch* será a base:**

Assim:

    git branch <nome-do-branch> <nome-do-branch-base>

Ou:

    git checkout -b <nome-do-branch> <nome-do-branch-base>


##### 2. Fazer suas alterações

Agora que já tem um *branch* específico para o que você quer fazer, é hora de fazer suas alterações no projeto. Pode mexer e alterar a vontade sem medo de ~~ser feliz~~ quebrar a build. Toda mudança será revisada depois. Vale notar que fazer alterações não necessariamente precisa vir depois de criar ou mudar pro *branch*, **desde que você esteja na base certa**. Ou seja, não importa em qual branch eu esteja enquanto faço as alterações, mas importa o estado dos arquivos que eu altero. Alguns exemplos:

1. Quero apenas incluir novos arquivos. Logo, não importa qual a base/*branch* que você está pois nenhum arquivo já existente será modificado.
2. Modifiquei um arquivo enquanto estava no *branch* **X**. Mas notei que a mudança que fiz na verdade pertence ao *branch* **Y**. Então temos dois casos: se o arquivo modificado está igual nos dois *branchs* **X** e **Y** (sem contar suas modificações) você pode trocar de *branch* sem nenhum problema, pois ao fazer o *checkout* (comando para mudar de um branch para o outro) o *git* vai processar que os dois arquivos são iguais e não precisará tocar neles. Mas se o arquivo é diferente nos dois *branchs* então ao fazer o *checkout* o *git* precisa editar o arquivo. Mas êpa! Você também modificou o arquivo! Então, para evitar que suas modificações sejam perdidas, o *git* te dá uma bela mensagem de *conflito* no arquivo.

##### 3. Verificar e selecionar suas alterações

Chega um momento nas suas alterações que você deseja salva-las no seu repositório. Mas antes disso, temos que ter certeza de que o que vamos salvar é realmente o que queremos que seja modificado no repositório. Isso é importante pois é muito comum alguém modificar vários arquivos, gerar outros automáticamente (binários, executáveis, temporários) e depois incluir tudo junto no repositório, tornando-o uma pasta cheia de lixo cujo *[commit](#commit)s* não fazem muito sentido pois são muito grandes e cheio de inutilidades. O primeiro passo é fazer o seguinte comando:

    git status

E você terá algo do tipo:

![git status](http://media.mediatemple.netdna-cdn.com/wp-content/uploads/2011/06/git1_4_git-status.gif)

A primeira coisa que o comando informa é em qual *branch* você está. Se não está no *branch* certo talvez seja a hora de mudar (fazer o *checkout*). Se você adicionou arquivos novos eles aparecerão como ***Untracked files***. Tecnicamente isso quer dizer que não há informações desses arquivos no último *[commit](#commit)* (do seu *branch* atual). Se você modificou arquivos que existem no último *[commit](#commit)* (seja alterar o conteúdo do arquivo ou deletar o arquivo completamente) eles aparecerão como ***Changes not staged for commit***. Ou seja, há mudanças no arquivo mas se você fizer o *[commit](#commit)* agora essas mudanças não serão salvas no repositório. Isso oferece uma grande chance de revisar e incluir no *[commit](#commit)* apenas o suficiente e necessário que você quer salvar e nada a mais. Para adicionar mudanças (seja essas mudanças um arquivo novo, alteração ou exclusão do arquivo) ao próximo *[commit](#commit)* utiliza-se o comando:

    git add <arquivo(s)>
    
Note que &lt;arquivo(s)&gt; pode ser o caminho para um arquivo, um diretório ou um *fileglob*. Exemplos:

    gid add src/Main.java 		# Adiciona o arquivo src/Main.java
    git add res/				# Adiciona toda a pasta res, sub-pastas e arquivos. Tenha certeza do que está fazendo.
    git add *.java				# Adiciona todos os arquivos java em qualquer pasta ou sub-pasta.
    git add *filesystem*		# Adiciona qualquer arquivo que contenha "filesystem" no seu caminho, ou seja, qualquer arquivo que tenha "filesystem" no seu nome ou no nome de alguma pasta pai.
	
Execute o comando *status* novamente para checar o andamento da sua seleção. Na verdade, use o *status* sempre que estiver em dúvida. Agora que você adicionou algumas mudanças, esses arquivos aparecerão em ***Changes to be committed*** ("mudanças a serem *commitadas*" no bom e velho pt_BR ~~HUEHUE3~~). Esses serão os arquivos modificados no seu próximo *[commit](#commit)*. Note que o comando **add** não produz nenhuma saída (exceto se nenhum arquivo for encontrado). Se quiser que seja exibido quais arquivos estão sendo de fato *add*icionados use o parâmetro **-v** (v de *verbose*). Por exemplo:

![git add -v](http://snag.gy/PF9OT.jpg)

Okay, sabemos quais arquivos serão modificados, **o que** exatamente será modificado nesses arquivos? E eis que lhe apresento um poderoso comando:

    git diff
    
Esse comando mostrará exatamente o que foi modificado. Na verdade, ele mostrará o que há de *diff*erente. Se nenhum parâmetro for passado ele mostrará o que mudou e que esteja **Unstaged for commit**. Então, se estiver em dúvida se deve fazer o *add* ou não de algum(ns) arquivo, e não lembrar o que mudou neles, use esse comando para confirmar. Esse comando também pode ser usado com vários parâmetros diferentes parar atender as mas diversas necessidades. Por exemplo:

    git diff --staged
    
Mostra do *diff* das mudanças que você fez e *add*icionou. Ou seja, o que será salvo no seu próximo *[commit](#commit)*. Costumo sempre usar esse comando antes de fazer meu *[commit](#commit)*.

    git diff <branch1>..<branch2>
    
Mostra o que há de *diff*erente entre os dois branch. Mais especificamente, mostra o que mudou no *branch* 2 a partir do *branch* 1.

    git diff <branch1>..
    
Mesma coisa que comando anterior, mas como o *branch* 2 não foi definido é considerado o *branch* que você está atualmente. Uso isso para comparar mudanças do meu *branch* com o *master*, por exemplo. Note que esse comando leva em conta todos os *commits* entre os dois *branchs* e não apenas as mudanças locais comparada com o último *[commit](#commit)*, que é o caso dos dois primeiros comandos *diff* apresentados. Lembra que eu falei que um *branch* nada mais é do que um ponteiro para um *[commit](#commit)*? Então isso quer dizer que esse mesmo comando vale para *commits*:

    git diff 672d5ba..92fac12
    
Mostra a diferença entre esses dois *commits*. Note que todo *[commit](#commit)* é unicamente identificado por um código *hash*, hexadecimal, de 40 dígitos. Mas você geralmente pode também referência-lo pelos 7 primeiros dígitos desse mesmo código, que é o exemplo acima.

O commando *diff* também permite que você selecione quais os arquivos você deseja ver o *diff* adicionalmente aos parâmetros já citados, e usando as mesmas regras de arquivos do commando *add*. Por exemplo:

    git diff master.. *.java 
    
Mostra o que meu *branch* atual tem de *diff*erente do meu *branch master*, mas mostrando apenas os arquivos que terminam em **java**.

Agora que já verificamos as mudanças (*git status*), selecionamos o que queremos salvar (*git add*), e já conferimos realmente o que estaremos salvando (*git diff --staged*), é hora de salvar/gravar/*commit*ar.

##### <a name="commit"></a>4. Salvando as mudanças

Já falamos algumas vezes sobre *commit*. Mas afinal, o que é isso? Um *commit* nada mais é do que um estado do seu projeto. Ou seja, uma referência com nome (*hash*), descrição (comentários), data e nome do autor (e outras informações que não importam agora), para uma versão (estado) de todos os seus arquivos de um projeto. A vantagem é que você pode facilmente mudar de uma versão para outra, ver o que mudou em cada versão (ou numa lista de versões) e até comparar versões (ou lista de versões). Mas antes de tudo, precisamos criar um commit. Para isso temos o comando:

    git commit

Uma tela parecida com essa irá será mostrada (a menos que seu editor padrão seja outro):

![git commit](http://i.stack.imgur.com/DSfuw.png)

Esse é o editor de texto [VIM](http://www.vim.org/). A primeira linha estará em branco e é onde você irá inserir seu comentário sobre esse *commit*. O que vai no comentário cabe a você e a sua equipe, mas sugiro que seja algo descritivo o suficiente para, pelo menos, ter uma ideia do que se trata o *commit*. Toda linha começada por # será ignorada. Haverá um pequeno resumo, muito parecido com o comando *status*, sobre o que você está prestes a *commit*ar. Dê uma última conferida se está no *branch* certo e se as mudanças corretas estão no ***Changes to be commited*** - nem a mais, nem a menos. Para inserir seu comentário, primeiro você tem que mudar o editor para o modo *inserção* pressionando a tecla "**i**". Você notará que o canto inferior esquerdo da janela mudou para:

![insert mode tip](http://snag.gy/Fb5oA.jpg)

Agora você pode digitar seu comentário sobre o *commit*. Quando terminar aperte **ESC** para sair do modo *inserção* e digite "**:wq \<ENTER\>**" (isso mesmo, dois-pontos w q) para salvar e sair (ou **ZZ** - maiúsculo). Se quiser cancelar o *commit*, basta deixar a mensagem vazia (ignorando linhas que começam com #). Feito isso, seu *commit* está criado e você receberá como saída algo do tipo:

![commit created](http://snag.gy/HFsYN.jpg)

Isso é um resumo do seu *commit* recém feito. Contém o nome do *branch*, os primeiros 7 dígitos do *hash* (identificador único do *commit*), o comentário e quantos arquivos e mudanças tiveram. Assim como todo comando do *git*, o comando *commit* também possui alguns parâmetros úteis. Se você não gostou do *VIM*, temos o parâmetro **-m** que permite pular a parte do editor colocando o comentário na linha de comando. Por exemplo:

    git commit -m "Incluindo arquivos de teste de integração."
    
Isso irá gerar o *commit* sem precisar abrir o *VIM*. Pessoalmente evito usar esse parâmetro pois, apesar de remover um passo no workflow, visualizar o resumo do *commit* e o *branch* atual nas informações no *VIM* podem evitar que mudanças indesejadas sejam introduzidas no repositório ou num *branch* errado. Outro parâmetro é o **-a** que permite pular a etapa anterior de **add** e incluir toda mudança feita *em arquivos já existentes no repositório*. O que o **-a** faz é executar um **add** antes do commit. E você pode combinar os dois, por exemplo:

    git commit -am "Nova feature de colorir background."

Novamente, evito usar o **-a** pois pode colocar mudanças indesejáveis no *commit*. Mas isso também pode ser evitado usando **status** e **diff** antes do **-a**.

Agora essas mudanças estão salvas no seu repositório local. Mas por enquanto apenas isso. Se você quer ter a segurança de back-up ou compartilhar esse *commit* com outros você precisa enviar o *commit* (ou os *commit*s) para um repositório remoto.

##### 5. Upando para seu repositório remoto

Seu repositório local nada mais é do que uma cópia de um repositório que está hospedado em algum lugar da internet (no GitHub, por exemplo), ou vice-versa. Não há nenhuma diferença entre esses repositórios exceto o local em que estão guardados (e talvez as modificações locais feitas depois da última sincronização). Isso quer dizer que se o repositório online sumir por alguma razão, seu repositório local pode ser totalmente usado para uma nova cópia do repositório remoto.

Se você só possui uma estação de trabalho e é o único que faz mudanças no seu repositório remoto (o que é bastante provável já que colaboradores provavelmente faram mudanças nos próprios repositórios *fork*ados de um principal) então de forma geral você só precisará fazer upload das suas mudanças locais para o seu repositório remoto. Há uma padronização no *git* de chamar o repositório remoto, que foi *fork*ado de outro ou iniciado do zero, de **origin**. Mas especificamente, o **origin** é o repositório usado quando você fez o *clone* para sua máquina. E é para ele que vamos mandar nossos novos *commits*. Se quiser mais informações sobre os repositórios remotos temos o comando:

    git remote

Mas não vamos entrar em detalhes sobre ele agora. Essa etapa é bastante simples. Só queremos mandar pro nosso *origin* todos os *commits* e *branchs* que criamos localmente mas não existem ainda no servidor remoto. Para isso temos o comando:

    git push <repositório> <branch>
    
Se o nome do *branch* for omitido, por default será usado o *branch* que você está atualmente (a menos que você modifique o comportamento default). Logo, se fizemos alterações localmente, criamos nossos *commits* no *branch* "implBackground", por exemplo, basta fazermos isso:

    git push origin implBackground

E teremos algo do tipo como output:

![git push output](http://snag.gy/CuSY3.jpg)

Isso mostra o resumo de dados enviados, o endereço do repositório, e qual *commit* foi atualizado para *commit* em cada *branch*. Se você atualizou vários *branchs* e não quer usar o mesmo comando com nomes de *branchs* diferentes, use o parâmetro **--all**:

    git push origin --all
    
Isso fará o *push* de todos os *branchs* que foram atualizados localmente. Agora seus *commits* já estão disponíveis no seu repositório remoto (GitHub, por exemplo) e podem ser visualizadas e utilizadas por qualquer um (se o repositório for público) ou por colaboradores com as devidas permissões.


##### 6. Colaborando com o projeto

Assumindo que seu repositório remoto foi *fork*ado de um outro repositório, você provavelmente vai querer que suas modificações façam parte do projeto e contribua de alguma forma. Usando o GitHub isso é feito através de um **Pull Request**, que nada mais é do que uma solicitação de inclusão (*merge*) de um determinado número de mudanças (*commits*/*branch*) em algum outro *branch* específico, geralmente o *master*. Recapitulando: você fez uma cópia (*fork*) do repositório principal (*upstream*) na sua conta remota (*origin*) do GitHub, depois baixou (*clone*) seu repositório para sua máquina, fez as mudanças necessárias, criou registrou as mudanças em um ou mais *commits* em um *branch* novo, mandou essas mudanças (*commits*/*branch*) para o seu repositório remoto (*origin*) e agora vai abrir um **Pull Request** para que essas mudanças façam parte do projeto principal. Fazer isso é bem simples, basta abrir a página do GitHub do seu repositório remoto (*origin*) e você terá uma opção de visualizar um *branch*:

![selecionador de branch](http://snag.gy/px5QD.jpg)

Basta selecionar o *branch* que você criou e modificou e clicar no botão ao lado:

![Compare, review, create a pull request button](http://snag.gy/TPDeq.jpg)

Nessa janela você poderá revisar os *commits* que serão incluídos, as mudanças que eles representam nos arquivos e até comentários feitos nos *commits*. Aqui você pode também mudar o repositório e o *branch* que está comparando antes de criar o **pull request** de fato. Depois de revisar as mudanças para ter certeza que escolheu o *branch* certo clique em **"Create pull request"**:

![Create pull request](http://snag.gy/ZfdQp.jpg)

