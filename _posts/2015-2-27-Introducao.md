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

Você não quer que sua mudança/atualização/correção de bug que ainda está instável, insegura e sem revisão bagunce o código principal, não é mesmo? Para isso utiliza-se um *branch*. Idealmente um *branch* é um conjunto de alterações que fazem sentido de estarem juntas. Por exemplo: implementação de uma nova funcionalidade, correção de um bug, melhoramento de um módulo, etc. Tecnicamente falando, um *branch* nada mais é do que um ponteiro para um *commit*. Criar um *branch* é muito fácil:

	git branch <nome-do-branch>


Para listar os *branchs* é mais fácil ainda:

	git branch


E para trocar sua área de trabalho de um *branch* para outro:

	git checkout <nome-do-branch>
	

Se quiser trocar para um novo *branch *(isto é, criar um novo e trocar):

	git checkout -b <nome-do-branch>
	

Importante lembrar algumas coisas:

1. Geralmente o primeiro e principal *branch* de todos os projetos no Git é o *master*. Isso é apenas uma convenção seguida pela maioria, mas nada lhe impede de excluir o *master* e usar outro *branch* como principal mas não recomendo.
2. Sempre que criar um *branch* novo, este terá como base o último *commit* (chamado de *HEAD*) do *branch* que você está no momento.  Isso é a mesma coisa que dizer: sempre que criar um *branch* novo, este será uma cópia exata do *branch* que você está no momento. **A menos que se especifique qual *branch* será a base:**

Assim:

	git branch <nome-do-branch> <nome-do-branch-base>

Ou:

	git checkout -b <nome-do-branch> <nome-do-branch-base>


##### 2. Fazer suas alterações

Agora que já tem um *branch* específico para o que você quer fazer, é hora de fazer suas alterações no projeto. Pode mexer e alterar a vontade sem medo de ~~ser feliz~~ quebrar a build. Toda mudança será revisada depois. Vale notar que fazer alterações não necessariamente precisa vir depois de criar ou mudar pro *branch*, **desde que você esteja na base certa**. Ou seja, não importa em qual branch eu esteja enquanto faço as alterações, mas importa o estado dos arquivos que eu altero. Alguns exemplos:

1. Quero apenas incluir novos arquivos. Logo, não importa qual a base/*branch* que você está pois nenhum arquivo já existente será modificado.
2. Modifiquei um arquivo enquanto estava no *branch* **X**. Mas notei que a mudança que fiz na verdade pertence ao *branch* **Y**. Então temos dois casos: se o arquivo modificado está igual nos dois *branchs* **X** e **Y** (sem contar suas modificações) você pode trocar de *branch* sem nenhum problema, pois ao fazer o *checkout* (comando para mudar de um branch para o outro) o *git* vai processar que os dois arquivos são iguais e não precisará tocar neles. Mas se o arquivo é diferente nos dois *branchs* então ao fazer o *checkout* o *git* precisa editar o arquivo. Mas êpa! Você também modificou o arquivo! Então, para evitar que suas modificações sejam perdidas, o *git* te dá uma bela mensagem de *conflito* no arquivo.

##### 3. Verificar e selecionar suas alterações

Chega um momento nas suas alterações que você deseja salva-las no seu repositório. Mas antes disso, temos que ter certeza de que o que vamos salvar é realmente o que queremos que seja modificado no repositório. Isso é importante pois é muito comum alguém modificar vários arquivos, gerar outros automáticamente (binários, executáveis, temporários) e depois incluir tudo junto no repositório, tornando-o uma pasta cheia de lixo cujo *commits* não fazem muito sentido pois são muito grandes e cheio de inutilidades. O primeiro passo é fazer o seguinte comando:

	git status

E você terá algo do tipo:

![git status](http://media.mediatemple.netdna-cdn.com/wp-content/uploads/2011/06/git1_4_git-status.gif)

A primeira coisa que o comando informa é em qual *branch* você está. Se não está no *branch* certo talvez seja a hora de mudar (fazer o *checkout*). Se você adicionou arquivos novos eles aparecerão como ***Untracked files***. Tecnicamente isso quer dizer que não há informações desses arquivos no último *commit* (do seu *branch* atual). Se você modificou arquivos que existem no último *commit* (seja alterar o conteúdo do arquivo ou deletar o arquivo completamente) eles aparecerão como ***Changes not staged for commit***. Ou seja, há mudanças no arquivo mas se você fizer o *commit* agora essas mudanças não serão salvas no repositório. Isso oferece uma grande chance de revisar e incluir no *commit* apenas o suficiente e necessário que você quer salvar e nada a mais. Para adicionar mudanças (seja essas mudanças um arquivo novo, alteração ou exclusão do arquivo) ao próximo *commit* utiliza-se o comando:

	git add <arquivo(s)>
	
Note que &lt;arquivo(s)&gt; pode ser o caminho para um arquivo, um diretório ou um *fileglob*. Exemplos:

	gid add src/Main.java 		# Adiciona o arquivo src/Main.java
	git add res/				# Adiciona toda a pasta res, sub-pastas e arquivos. Tenha certeza do que está fazendo.
	git add *.java				# Adiciona todos os arquivos java em qualquer pasta ou sub-pasta.
	git add *filesystem*		# Adiciona qualquer arquivo que contenha "filesystem" no seu caminho, ou seja, qualquer arquivo que tenha "filesystem" no seu nome ou no nome de alguma pasta pai.
	
Execute o comando *status* novamente para checar o andamento da sua seleção. Na verdade, use o *status* sempre que estiver em dúvida. Agora que você adicionou algumas mudanças, esses arquivos aparecerão em ***Changes to be committed*** ("mudanças a serem *commitadas*" no bom e velho pt_BR ~~HUEHUE3~~). Esses serão os arquivos modificados no seu próximo *commit*.

Okay, sabemos quais arquivos serão modificados, **o que** exatamente será modificado nesses arquivos? E eis que lhe apresento um poderoso comando:

	git diff
	
Esse comando mostrará exatamente o que foi modificado. Na verdade, ele mostrará o que há de *diff*erente. Se nenhum parâmetro for passado ele mostrará o que mudou e que esteja **Unstaged for commit**. Então, se estiver em dúvida se deve fazer o *add* ou não de algum(ns) arquivo, e não lembrar o que mudou neles, use esse comando para confirmar. Esse comando também pode ser usado com vários parâmetros diferentes parar atender as mas diversas necessidades. Por exemplo:

	git diff --staged
	
Mostra do *diff* das mudanças que você fez e *add*icionou. Ou seja, o que será salvo no seu próximo commit. Costumo sempre usar esse comando antes de fazer meu commit.

	git diff <branch1>..<branch2>
	
Mostra o que há de *diff*erente entre os dois branch. Mais especificamente, mostra o que mudou no *branch* 2 a partir do *branch* 1.

	git diff <branch1>..
	
Mesma coisa que comando anterior, mas como o *branch* 2 não foi definido é considerado o *branch* que você está atualmente. Uso isso para comparar mudanças do meu *branch* com o *master*, por exemplo. Note que esse comando leva em conta todos os *commits* entre os dois *branchs* e não apenas as mudanças locais comparada com o último *commit*, que é o caso dos dois primeiros comandos *diff* apresentados. Lembra que eu falei que um *branch* nada mais é do que um ponteiro para um *commit*? Então isso quer dizer que esse mesmo comando vale para *commits*:

	git diff 672d5ba..92fac12
	
Mostra a diferença entre esses dois *commits*. Note que todo *commit* é unicamente identificado por um código *hash*, hexadecimal, de 40 dígitos. Mas você geralmente pode também referência-lo pelos 7 primeiros dígitos desse mesmo código, que é o exemplo acima.

O commando *diff* também permite que você selecione quais os arquivos você deseja ver o *diff* adicionalmente aos parâmetros já citados, e usando as mesmas regras de arquivos do commando *add*. Por exemplo:

	git diff master.. *.java 
	
Mostra o que meu *branch* atual tem de *diff*erente do meu *branch master*, mas mostrando apenas os arquivos que terminam em **java**.

Agora que já verificamos as mudanças (*git status*), selecionamos o que queremos salvar (*git add*), e já conferimos realmente o que estaremos salvando (*git diff --staged*), é hora de salvar/gravar/*commit*ar.