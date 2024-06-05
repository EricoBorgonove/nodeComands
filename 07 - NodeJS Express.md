# Conceito

Express é um popular framework web estruturado, escrito em JavaScript que roda sobre o ambiente node.js em tempo de execução. Express é o framework Node mais popular e a biblioteca subjacente para uma série de outros frameworks do Node. O Express oferece soluções para:

- Gerenciar requisições de diferentes verbos HTTP em diferentes URLs.
- Integrar "view engines" para inserir dados nos templates.
- Definir as configurações comuns da aplicação web, como a porta a ser usada para conexão e a localização dos modelos que são usados para renderizar a resposta.
- Adicionar novos processos de requisição por meio de "middleware" em qualquer ponto da "fila" de requisições.

O Express é bastante minimalista, no entanto, os desenvolvedores têm liberdade para criar pacotes de middleware específicos com o objetivo de resolver problemas específicos que surgem no desenvolvimento de uma aplicação. Há bibliotecas para trabalhar com cookies, sessões, login de usuários, parâmetros de URL, dados em requisições POST, cabeçalho de segurança e tantos outros. Você pode achar uma lista de pacotes de middleware mantidos pela equipe Express em Express Middleware (juntamente com uma lista de pacotes populares desenvolvidos por terceiros).

# Configuração Inicial

``index.js``
````js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Olá Mundo!!')
})

app.listen(port, () => {
  console.log(`App rodando na porta:${port}`)
})
````

Após a criação desse arquivo e execução dele no terminal com ``node``, abra no seu navegador o endereço ``http://localhost:3000``.

## Enviando arquivo html

``index.js``
````js
const express = require('express')
const path = require('path')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Olá Mundo!!')
})

app.get('/html', (req, res) => {
  res.sendFile(path.resolve('index.html'))
})

app.listen(port, () => {
  console.log(`App rodando na porta:${port}`)
})
````

Agora, adicionando uma nova rota, podemos acessar ``http://localhost:3000/html``

# Rotas

Todo container web precisa ser capaz de responder adequadamente a uma requisição de usuário. Essa resposta depende do caminho digitado no navegador (URL). Cada caminho irá direcionar o usuário para uma página específica ou executar uma operação específica no servidor. Esse gerenciamento dos caminhos, ou rotas, disponíveis na aplicação é chamado de roteamento.

````js
app.get('/', (req, res) => {
  res.send('Olá Mundo!!')
}) // Essa rota ficará disponível através da requisição http://localhost:3000/


app.get('/html', (req, res) => {
  res.sendFile(path.resolve('index.html'))
}) // Essa rota ficará disponível através da requisição http://localhost:3000/html
````

## Acessando parâmetros nas rotas
``index.js``
````js
app.get('/user/:user', (req, res) => {
  const user = req.params.user

  res.send("Você está visualizando as informações do usuário: " + user);
})
````

Dessa forma você consegue acessar através da URL ``http://localhost:3000/user/1``

# Nodemon

Através do Nodemon é possível nós fazermos alterações em nosso código sem precisar reiniciar o servidor para ver as alterações em funcionamento.

````sh
npm install nodemon
````

Adicionar o script do nodemon no arquivo ``package.json``
````json
{
  "scripts": {
    "dev": "nodemon index.js"
  }
}
````

Agora você pode executar o seguinte comando:

````sh
npm run dev
````

# Servindo arquivos estáticos

Os arquivos estáticos são todos os arquivos que não precisarão de processamento pelo ``NodeJS``, onde seja, arquivos css, js (no frontend), imagens, robots.txt e etc. Esses arquivos precisarão ficar em uma pasta, para melhor organização. Essa pasta comumente é chamada de ``public``. 

Então vamos primeiramente criar um arquivo CSS pra testes

``public/style.css``
````css
body {
  background-color: black;
  color: white;
}
```` 

``index.js``
````js
const express = require('express')
const path = require('path')
const app = express()
const port = 3000

/* Código abaixo identifica a pasta de arquivos estáticos */
app.use(express.static('public'))

app.get('/', (req, res) => {
  res.send('Olá Mundo!!')
})

app.get('/html', (req, res) => {
  res.sendFile(path.resolve('index.html'))
})

app.listen(port, () => {
  console.log(`App rodando na porta:${port}`)
})
````

``index.html``
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="/style.css">
</head>
<body>
    Lorem, ipsum dolor sit amet consectetur adipisicing elit. Reprehenderit, ad.
</body>
</html>
````

Agora vamos acessar no navegador ``http://localhost:3000/html``

# Erro 404

Para fazer personalização na página de erro 404, você deve criar uma ``middleware`` que irá ser executada se nenhuma rota for entrada, por isso o código abaixo tem que ser a última linha de código, antes do ``app.listen()``

``index.js``
````js
/* Esse código sempre tem que ser a última rota. Logo antes do listen. */
app.use(function (req, res, next) {
  res.status(404).sendFile(path.resolve('404.html'))
})
````

# Módulo de Rotas
É uma boa prática nós criarmos arquivos separados para as rotas para não poluirmos o arquivo ``index.js`` com todas as notas rotas da aplicação. Por isso, em seu projeto, crie uma pasta chamada ``routes`` e, dentro dessa pasta, crie um arquivo chamado ``routes.js``.

Todas as nossas rotas deverão ficar nesse arquivo ``routes.js``.

``routes.js``
````js
const express = require('express')
const router = express.Router()
const path = require('path')


router.get('/', (req, res) => {
    res.send('Olá Mundo!!')
})

router.get('/html', (req, res) => {
    res.sendFile(path.resolve('index.html'))
})

router.get('/user/:user', (req, res) => {
    const user = req.params.user
    res.send("Você está visualizando as informações do usuário: " + user);
})

/* Esse código sempre tem que ser a última rota. Logo antes do listen. */
router.use(function (req, res, next) {
    res.status(404).sendFile(path.resolve('404.html'))
})

module.exports = router
````

``index.js``
````js
const express = require('express')
const app = express()
const port = 3000
const routes = require('./routes/routes')

app.use(express.static('public'))
app.use('/', routes)

app.listen(port, () => {
  console.log(`App rodando na porta:${port}`)
})
````

# Módulo Controller
Para que nossa aplicação tenha cada responsabilidade separada e siga um padrão mundialmente reconhecido, o MVC, precisamos retirar nossa lógica do arquivo de rotas. Para isso, crie uma pasta chamada ``controllers`` na raiz do seu projeto.  Dentro dessa pasta vamos criar um arquivo chamado ``IndexController.js``.

``IndexController.js``
````js
module.exports = class IndexController {
    static helloWorld(req, res) {
        res.send(`Você está utilizando a camada Controller`)
    }
}
````

Perceba que precisamos criar um método estático que será o método que irá responder à rota acessada. Portanto precisamos alterar o nosso arquivo de rotas para reconhecer o controller criado.

``routes.js``
````js
// ...
const IndexController = require('../controllers/IndexController')
// ...

app.get('/', IndexController.helloWorld)
````

Agora a lógica da nossa aplicação passa a ser direcionada para o controller e não mais ficará poluindo o arquivo de rotas. 

# Parâmetros no Body (POST Resquest)

Para reconhecer os parâmetros (variáveis) passadas em uma requisição do tipo POST, precisamos adicionar as linhas abaixo no nosso arquivo principal

``index.js``
````js
app.use(express.urlencoded({ extended: true })) // Aceita requisições do tipo url-encoded, ou seja, requisições de formulários e etc.
app.use(express.json()) // Aceita JSON como requisição (importante para APIs)
````

Agora os valores da requisição passam a ficar acessíveis da seguinte forma:

``IndexController.js``
````js
module.exports = class IndexController {
    static index(req, res) {
        res.send('Página Inicial')
    }

    static save(req, res) {
        console.log(req.body)
        /* Todos os valores ficam no objeto req.body */
        res.send('Valores recebidos via requisição com sucesso!')
    }
}
````

``routes.js``
````js
// ...
const IndexController = require('../controllers/IndexController')
// ...

app.get('/', IndexController.helloWorld)
app.post('/salvar',IndexController.save)
````
