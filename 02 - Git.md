[Table of Contents](#table-of-contents)
- [Introdução](#introdução)
- [Instalação do git](#instalação-do-git)
  - [Instalação no Windows](#instalação-no-windows)
  - [Instalação no Linux](#instalação-no-linux)
- [Configuração Inicial](#configuração-inicial)
- [Inicialização](#inicialização)
- [Nosso Primeiro Commit](#nosso-primeiro-commit)
  - [git status](#git-status)
  - [git add](#git-add)
  - [git commit](#git-commit)
- [Gitkraken](#gitkraken)
- [Trabalhando com repositórios remotos](#trabalhando-com-repositórios-remotos)
  - [git clone](#git-clone)
  - [git pull](#git-pull)
  - [git push](#git-push)

# Introdução

Git é um sistema de controle de versão de arquivos. Através deles podemos desenvolver projetos na qual diversas pessoas podem contribuir simultaneamente no mesmo, editando e criando novos arquivos e permitindo que os mesmos possam existir sem o risco de suas alterações serem sobrescritas.

# Instalação do git

## Instalação no Windows
Para a instalação do git no Windows, sugerimos o instalador do [git-scm.com](https://git-scm.com/downloads). Após realizar o download do executável, basta instalar como qualquer outro programa para Windows, seguindo o padrão ``Next, Next, Install``.

## Instalação no Linux
Para a instalação do git no Linux é ainda mais fácil. Basta você atualizar as listas dos repositórios e depois realizar a instalação. Faça os seguintes comandos no terminal ``CTRL + SHIT + T``:

````sh
####### instalação do git no Linux Ubuntu
sudo apt update
sudo apt install git
````

# Configuração Inicial
Devemos configurar nosso usuário e nosso email para a utilização do git. Para isso basta executarmos os comandos abaixo após a instalação
````sh
git config --global user.name "Meu Nome"
git config --global user.email "meu.email@email.com"
````

# Inicialização
Para utilizar os comandos do git, você precisa inicializar o git dentro do seu projeto. Considerando que você utiliza Linux Ubuntu no nosso curso, faça os comandos abaixo no seu terminal. 

````sh
####### acesse o diretório do seu usuário no linux (o til é um atalho para a pasta do usuário logado)
cd ~

####### vamos criar uma pasta para colocarmos todos os nossos projetos dentro dela
mkdir Projetos

####### ao usar o comando ls, verificamos que nossa pasta foi criada
ls -la

####### agora vamos entrar na nossa pasta recem criada
cd Projetos

####### vamos criar uma nova pasta que será a pasta que colocaremos nosso projeto desta aula
mkdir MeuPrimeiroGit

####### após criar a nova pasta, vamos entrar nela
cd MeuPrimeiroGit

####### para começarmos a utilizar o git, devemos inicializá-lo na pasta do nosso projeto
git init
````

Ao executar esses comandos o git criará uma pasta oculta chamada ``.git`` dentro do seu projeto. Para uso normal do git você não precisará conhecer a fundo o funcionamento desta pasta.

# Nosso Primeiro Commit
Vamos criar um arquivo dentro do posso projeto. Vamos continuar usando comandos do Linux antes de utilizarmos uma IDE, pois o conhecimento desses comandos será muito importante no decorrer do nosso curso. 

````sh
####### certifico se estou dentro da pasta do meu projeto
####### a resposta do comando abaixo tem que se algo similar a /home/meu_usuario/Projetos/MeuPrimeiroGit
####### se a resposta for algo diferente disso, você deve entrar na pasta novamente
pwd

cd ~
cd Projetos/MeuPrimeiroGit
####### ou simplesmente
cd ~/Projetos/MeuPrimeiroGit
####### você pode usar o tab para ir completando seu comando

####### vamos utilizar um editor de texto por linha de comando para criar um arquivo chamado teste.txt
nano teste.txt
````

O nano é um editor de texto do Linux que também pode ser usado no Windows através da instalação do ``Git Bash``. 

A tela do editor de texto nano é bem simples. Escreva qualquer texto e salve o arquivo. Para salvar o arquivo você deve utilizar as teclas ``CTRL + O`` e para sair você deve utilizar o ``CTRL + X``. 

Pronto, fazendo isso você tem um arquivo chamado ``teste.txt`` dentro do diretório do seu projeto. Para confirmar utilize o ls
````sh
ls -l
````

Apenas criando o arquivo você ainda não fez o git reconhecer a criação dele. Para o git a criação do arquivo somente é confirmada através do ``commit``. Mas antes vamos listar os arquivos pendentes de commit através do ``status``

## git status

````sh
git status
````

O retorno desse comando deve dizer que o arquivo teste.txt está com status Untracked, ou seja, ele ainda não está sendo rastreado pelo git. 

## git add

Para fazer o commit do arquivo você deve primeiro dizer para o git rastreá-lo. Adicione o arquivo aos arquivos reconhecidos pelo git através do comando add.

````sh
git add teste.txt
````

Durante o desenvolvimento de software é comum você adicionar dezenas de arquivos de uma só vez. Para que você não precise adicionar arquivo por arquivo, você pode usar o add para adicionar todos os arquivos que precisam ser rastreados.

````sh
git add .
####### dessa forma todos os arquivos que estão untracked serão enviados para o stage
````

Vamos verificar o status do nosso git através do comando git status novamente.
````sh
git status
````

Você deve receber a mensagem que um novo arquivo foi adicionado
````diff
+ new file: teste.txt
````

Agora vamos, de fato, fazer o nosso commit

## git commit

````sh
git commit -m "Este é o meu primeiro commit"
````

A partir de agora o git registrou que seu usuário fez um commit e que este commit adiciona um arquivo chamado teste.txt. Vamos visualizar o que fizemos em uma interface.

# Gitkraken
O Gitkraken é um cliente de interface para o git no Windows, Linux e Mac. Para instalá-lo basta realizar o download do instalador através do [site oficial](https://www.gitkraken.com/).

A instalação é bem simples. Padrão ``Next, Next, Install``.

Após a instalação você deve abrir o repositório do seu projeto indo em ``File > Open Repo > Open Repository > Pasta do Seu Projeto``. 

Observe que seu commit está listado, assim como os arquivos e as linhas que seu commit alterou/adicionou/excluiu. O Gitkraken ajuda muito a utilização do git visto que seus componentes são bem didáticos e intuitivos. Porém, para este curso, aprenderemos a como realizar todos os comandos do git por linha de comando, visto que nem sempre teremos acesso a um Gitkraken. 

# Trabalhando com repositórios remotos
Os repositórios remotos são utilizados quando os desenvolvedores precisam compartilhar o seu trabalho com outros desenvolvedores do time. O repositório é o local onde o sistema de controle de versão mantém o rastreamento de todas as alterações realizadas no projeto. 

Quando se faz necessário compartilhar o trabalho realizado com todos os outros desenvolvedores utiliza-se um repositório remoto para receber e disponibilizar os artefatos produzidos pelos desenvolvedores. 

Exemplo de serviços na núvem de repositórios: ``Github``, ``Gitlab``, ``Bitbucket``...

Este repositório, por exemplo, está hospedado no Github e pode ser clonado para seu ambiente de desenvolvimento. 

## git clone
````sh
cd ~/Projetos/
####### Primeiramente vamos entrar na nossa pasta de projetos

git clone https://github.com/flexpeak/curso-ifpk-turma01.git
####### Recebe um repositório inteiro hospedado na URL. Como é um repositório privado, você será solicitado de um usuário e senha
````

A partir de agora o projeto já está baixado no seu ambiente de desenvolvimento. Faça o download do [VSCode](https://code.visualstudio.com/) para fazer as alterações no projeto.

Após você concluir as alterações que você deseja, não esqueça de você deve trackear os arquivos e fazer o commit.

````sh
####### Comandos que deverão ser feitos após alterações nos arquivos
git add .
git commit -m "Alteração de código"
````

Você pode abrir o repositório no Gitkraken para ter uma visualização das alterações no seu repositório git.

Após fazer o commit é necessário você enviar suas alterações para o repositório remoto. No momento as alterações estão apenas no seu computador.

## git pull
Antes de enviar seu código para o servidor remoto é sempre uma boa prática atualizar o repositório no seu computador com as últimas alterações do repositório no remoto. Para fazer isso, basta você utilizar o comando ``git pull``

````sh
git pull
####### Atualiza todas as branches com as alterações do remoto

git pull origin master
####### Atualia apenas a branch master apenas do remoto origin
````

## git push
Agora podemos enviar nossas alterações para o repositório remoto através do comando ``git push``.
````sh
git push
####### Envia todas as branches para o remoto

git push origin master
####### Envia apenas a branch master para o remoto origin
````
