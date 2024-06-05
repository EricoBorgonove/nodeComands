# Instalação do NODE e do NPM

## Instalação no Linux
````sh
cd ~
sudo apt install curl
curl -sL https://deb.nodesource.com/setup_16.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt install nodejs
node -v
npm -v
````

## Instralação no Windows
Entre no site oficial do NodeJS e baixe o pacote de instalação: [clique aqui](https://nodejs.org/en/).

Dê preferência sempre para as instalações do tipo LTS.

A instalação é simples, basta seguir o padrão Next, Next, Install. 

# NPM

O NPM é uma ferramenta do Node.js para o gerenciamento de pacotes. Ele permite instalar, desinstalar e atualizar dependências em uma aplicação por meio de uma simples instrução na linha de comando. Sempre que um projeto é criado por meio do gerenciador, é adicionado um arquivo chamado package.json, que contém a relação dos pacotes instalados no ambiente. 

Em um projeto, para fazer uso do NPM, você deve inicializá-lo com ``npm init``

## Scripts do NPM

OS scripts do NPM são um conjunto de scripts node que você pode executar. Ex:
````json
"scripts": {
  "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
  "start": "npm run dev",
  "unit": "jest --config test/unit/jest.conf.js --coverage",
  "test": "npm run unit",
  "lint": "eslint --ext .js,.vue src test/unit",
  "build": "node build/build.js"
}
````

Estes scripts são aplicações de linha de comando. Você pode rodá-los usando npm run XXXX, onde XXXX é o nome do comando. Ex:

````sh
npm run dev
````

Você pode usar qualquer nome que você quiser para um comando, e os scripts podem ser literalmente qualquer coisa que você quiser.

# Primeiro Programa NodeJS

Vamos criar um arquivo chamado ``primeiro-programa.js``.

Coloque o seguinte conteúdo nele:

````js
class Pessoa {
    nome; 

    constructor(nome) {
        this.nome = nome;
    }
}

pessoa = new Pessoa("João da Silva");

console.log(pessoa);
````

Execute o script utilizando o NodeJS

````sh
node primeiro-programa.js
````

# Módulos do NodeJS

No Node.js, um module é uma coleção de funções e objetos do JavaScript que podem ser utilizados por aplicativos externos. Descrever um trecho de código como um módulo se refere menos ao que o código é do que aquilo que ele faz — qualquer arquivo Node.js pode ser considerado um módulo caso suas funções e dados sejam feitos para programas externos.

## Criando nosso próprio módulo

Vamos criar dois arquivos, um que será um módulo e outro que utilizará este módulo. 

modulo.js
````js
module.exports = {
    subtrair(a, b) {
        console.log(a - b)
    },
}
````

index.js
````js
const modulo = require('./modulo');

modulo.subtrair(8, 3);
````

## Utilizando módulos nativos

O primeiro módulo nativo que iremos estudar é o ``path``, que é um módulo que tem funcionalidades que ajudam no tratamento de diretórios no NodeJS. 

index.js
````js
const path = require("path");

/* Descobrir a extensão de um arquivo */
console.log(path.extname("arquivo.php"));

/* Montar um caminho de diretório */
console.log(path.join("Documentos", "Imagens", "imagem.jpeg"));

/* Descobrir o caminho completo de um arquivo/pasta */
console.log(path.resolve("index.js"));
````

Conheça todos os métodos e atributos do ``path`` na documentação oficial do módulo:

[https://nodejs.org/api/path.html](https://nodejs.org/api/path.html)

> Utilize o mesmo site de documentação para criar um programa que identifica o sistema operacional do servidor node.

## Utilizando módulos externos

Módulos de terceiros são os módulos de Nó externos. Esses são os módulos Node de terceiros desenvolvidos por desenvolvedores do Node que são disponibilizados por meio do ecossistema do Node. Mas precisamos de um gerenciador de pacotes que mantenha todos os módulos para que possam ser acessados com facilidade. É aqui que o NPM entra em cena.

Vamos fazer uso do módulo ``minimist`` disponível no [npmjs.com](https://www.npmjs.com/package/minimist). Este módulo permite que a gente passe parâmetros na chamada do ``node``.

````js
// --nome=Matheus --idade=30
const minimist = require("minimist");

const args = minimist(process.argv.slice(2));

console.log(args);

const nome = args["nome"];
const idade = args["idade"];

console.log(nome);
console.log(idade);
````

> Faça uso de outro módulo externo chamado ``chalk`` - [documentação disponível aqui](https://www.npmjs.com/package/chalk) - e tente mudar as cores do terminal

# Assíncrono e Síncrono

## Síncrono
As funções síncronas bloqueiam a execução do programa até que a operação do arquivo seja realizada. Essas funções também são chamadas de funções de bloqueio.

````js
const fs = require("fs");

console.log("Início");

fs.writeFileSync("arquivo.txt", "Oi");

console.log("Fim");
````

## Assíncrono
As funções assíncronas não bloqueiam a execução do programa e cada comando é executado após o comando anterior, mesmo que o comando anterior não tenha calculado o resultado. O comando anterior é executado em segundo plano e carrega o resultado assim que termina o processamento.

````js
const fs = require("fs");

console.log("Início");

fs.writeFile("arquivo.txt", "Oi", function (err) {
  setTimeout(function () {
    console.log("Arquivo criado!");
  }, 1000);
});

console.log("Fim");
````

# Tratamento de Exceções
Erros no Node.js são tratados por meio de exceções. Uma exceção é crianda usando a palavra reservada throw:
````js
const x = "10";

if (!Number.isInteger(x)) {
  throw new Error("O valor de x não é um número inteiro");
}
````
Assim que o JavaScript executa essa linha, o fluxo normal do programa é parado e o controle é retomado pelo tratamento de exceção mais próximo.

## try catch
O jeito correto de fazer tratamento de exceções é fazendo uso do ``try catch``. Observe o código abaixo:

````js
const x = 10;

try {
  x = 2;
} catch (err) {
  console.log(`Erro: ${err}`);
}
````
