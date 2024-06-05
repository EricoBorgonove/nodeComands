# Introdução
Para grandes aplicações, devemos fazer uso de arquivos auxiliares que nos ajudarão no processo de desenvolvimento de software. Nessa sessão veremos alguns.

# .env
Crie na raiz do seu projeto um arquivo chamado ``.env`` one você poderá colocar variáveis do seu ambiente, como acessos de bancos de dados, chaves de API e etc. Para utilizar esse arquivo faremos uso de um módulo chamado ``dotenv``. Dotenv é um módulo de dependência que carrega variáveis de ambiente de um arquivo ``.env`` para ``process.env``.

````sh
npm install dotenv
````

``.env``
````
BASE_API=https://api.themoviedb.org/3/
API_KEY=1dee164e8b8a3c4cfeb5bb3f0db3e470
````

``index.js``
````js
// ...
require('dotenv').config()
// ...
````

Agora, em qualquer lugar da aplicação, você passa a ter acesso a um objeto com os valores salvos neste arquivo. 

``IndexController.js``
````js
console.log(process.env.BASE_API)
````

# .gitignore
É do conhecimento comum que os valores que são sensíveis ou dependem do ambiente do código não devem ser comprometidos com o controle de versão. Então, não se preocupe, pois não vamos fazer isso. Para resolver essa questão, vamos utilizar o famoso .gitignore. Portanto, na raiz do seu projeto crie um arquivo chamado ``.gitignore``. Todos os arquivos e pastas que estiverem neste arquivo, serão ignorados do git, não irão ser commitados, feitos push ou pull.

 ``.gitignore``
 ````
 .env
node_modules
 ````
 
 Dessa forma nosso arquivo .env não será enviado para o git, protegendo portanto nossas senhas e informações sensíveis. 
 
 > **ATENÇÃO**
 > 
 > Como o arquivo .env e a pasta ``node_modules`` não irão para o seu git, em todo ambiente de trabalho seu você deverá criar o arquivo .env e baixar as dependências do seu projeto com o npm install para que a pasta node_modules seja criada.

# Axios
O axios é um módulo para fazer requisições HTTP tanto do backend quanto do frontend. Documentação e exemplos de uso podem ser encontradas no [repositório oficial](https://www.npmjs.com/package/axios).

````js
const axios = require('axios');

axios.get('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .then(function () {
    // always executed
  });
````
