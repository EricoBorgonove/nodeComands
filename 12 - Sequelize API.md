# Introdução

As APIs são um conjunto de padrões que fazem parte de uma interface e que permitem a criação de plataformas de maneira mais simples e prática para desenvolvedores. A partir de APIs é possível criar softwares, aplicativos, programas e plataformas diversas. Por exemplo, apps desenvolvidos para celulares Android e iPhone (iOS) são criados a partir de padrões definidos e disponibilizados pelas APIs de cada sistema operacional.

# JSON

JSON é basicamente um formato leve de troca de informações/dados entre sistemas. Mas JSON significa JavaScript Object Notation, ou seja, só posso usar com JavaScript correto? Na verdade não e alguns ainda caem nesta armadilha.

O JSON além de ser um formato leve para troca de dados é também muito simples de ler. Mas quando dizemos que algo é simples, é interessante compará-lo com algo mais complexo para entendermos tal simplicidade não é? Neste caso podemos comparar o JSON com o formato XML.

````json
{
    "mensagem": {
        "para": "João",
        "de": "Maria",
        "titulo": "Lembrete",
        "conteudo": "Não se esqueça do nosso encontro no final de semana"
    }
}
````

# Rotas

Para gerenciar nossas rotas é indicado que criamos um arquivo diferente do já criado anteriormente. Vamos chamar esse arquivo, por exemplo, de ``apiRoutes.js``.

``apiRoutes.js``
````js
const { Router } = require('express')
const router = Router()

router.get('/', (req, res) => {
    res.send({
        success: true
    })
})

module.exports = router
````

Agora precisaremos incluir essas rotas no nosso arquivo de configuração ``index.js``.

``index.js``
 ````js
 const apiRoutes = require('./apiRoutes')
 
 // ...
 
 app.use('/api', apiRoutes)
 ````
 
 Agora acessando a rota ``http://localhost:8080/api`` pelo Postman ou pelo Insomnia devemos receber como retorno o json:
 ````json
 {
    "success": true
}
 ````

# CRUD de Pessoas
Aproveitando o CRUD de pessoas, vejamos os passos para fazermos funcionar para nossa API. Para isso vamos criar um novo PessoaController dentro de uma pasta ``api`` na pasta ``controllers``. 

## Listar Pessoas (R)
``api/PessoaController.js``
````js
const { Pessoa } = require('../../models/index')

module.exports = class PessoaController {
    static async index(req, res) {
        const pessoas = await Pessoa.findAll()
        res.send(pessoas)
    }
}
````

``apiRoutes.js``
````js
const { Router } = require('express')
const PessoaController = require('./controllers/api/PessoaController')
const router = Router()

router.get('/pessoas', PessoaController.index)
````

A partir de agora podemos acessar ``http://localhost:8080/api/pessoas`` e então devemos conseguir visualizar um array de objetos de pessoas.

### Visualizar uma Pessoa (R)
``api/PessoaController.js``
````js
    static async show(req, res) {
        const pessoa = await Pessoa.findByPk(req.params.id)
        res.send(pessoa)
    }
````

``apiRoutes.js``
````js
router.get('/pessoas/:id', PessoaController.show)
````

A partir de agora podemos acessar ``http://localhost:8080/api/pessoas/1`` e visualizar os dados da pessoa de id 1.

## Criar Pessoas (C)
``api/PessoaController.js``
````js
    static async create(req, res) {
        const pessoa = await Pessoa.create({
            nome: req.body.nome,
            email: req.body.email,
            data_nascimento: req.body.data_nascimento,
            salario: req.body.salario
        })

        res.send(pessoa)
    }
````

``apiRoutes.js``
````js
router.post('/pessoas', PessoaController.create)
````

A partir de agora podemos fazer um POST na rota ``http://localhost:8080/api/pessoas`` com o body (raw):
````json
{
	"nome": "Mateus Silva",
	"data_nascimento": "09/10/2000",
	"email": "mateus@mateus.com",
	"salario": "3400"
}
````

E deve ser retornado para a gente uma pessoa criada e seu respectivo ID. 

## Atualizar Pessoas (U)
``api/PessoaController.js``
````js
    static async update(req, res) {
        const pessoa = await Pessoa.findByPk(req.params.id)
        const result = await pessoa.update({
            nome: req.body.nome,
            email: req.body.email,
            data_nascimento: req.body.data_nascimento,
            salario: req.body.salario
        })

        res.send(result)
    }
````

``apiRoutes.js``
````js
router.put('/pessoas/:id', PessoaController.update)
````

A partir de agora podemos fazer um PUT na rota ``http://localhost:8080/api/pessoas/1`` com o body (raw):
````json
{
	"nome": "Maurício Matar",
	"data_nascimento": "13/01/1990",
	"email": "mauricio@mauricio.com",
	"salario": "9500"
}
````

E deve ser retornado para a gente uma pessoa atualizada e seu respectivo ID.

## Excluir Pessoas (D)
``api/PessoaController.js``
````js
    static async delete(req, res) {
        const pessoa = await Pessoa.findByPk(req.params.id)
        await pessoa.destroy()

        res.send(true)
    }
````

``apiRoutes.js``
````js
router.delete('/pessoas/:id', PessoaController.delete)
````

A partir de agora podemos fazer um DELETE na rota ``http://localhost:8080/api/pessoas/1`` e o registro 1 deverá ser excluído. 

# Padronização nos Retornos
## Códigos HTTP
* Respostas de informação (100-199),
* Respostas de sucesso (200-299),
* Redirecionamentos (300-399)
* Erros do cliente (400-499)
* Erros do servidor (500-599).

## Códigos mais comuns
### 200 OK
Estas requisição foi bem sucedida. O significado do sucesso varia de acordo com o método HTTP.

### 401 Unauthorized
Embora o padrão HTTP especifique "unauthorized", semanticamente, essa resposta significa "unauthenticated". Ou seja, o cliente deve se autenticar para obter a resposta solicitada.

### 403 Forbidden
O cliente não tem direitos de acesso ao conteúdo portanto o servidor está rejeitando dar a resposta. Diferente do código 401, aqui a identidade do cliente é conhecida.

### 404 Not Found
O servidor não pode encontrar o recurso solicitado. Este código de resposta talvez seja o mais famoso devido à frequência com que acontece na web.

### 500 Internal Server Error
O servidor encontrou uma situação com a qual não sabe lidar.

## Exemplo de uso nos Controllers
``api/PessoaController.js``
````js
    static async index(req, res) {
        try {
            const pessoas = await Pessoa.findAll()
            res.status(200).json({
                data: pessoas
            })
        } catch (e) {
            res.status(500).json({
                error: e.message
            })
        }
    }
````

# Token JWT
JWT (JSON Web Token) é um método RCT 7519 padrão da indústria para realizar autenticação entre duas partes por meio de um token assinado que autentica uma requisição web. Esse token é um código em Base64 que armazena objetos JSON com os dados que permitem a autenticação da requisição.

````sh
npm i jsonwebtoken bcrypt
````

## Criação da model e migration de Usuários
````sh
sequelize model:generate --name=User --attributes=name:STRING,email:STRING,password:STRING
````

## Execução da migration
````sh
sequelize db:migrate
````

## Criação da seed
````sh
sequelize seed:generate --name=User
````

## Código da Seed 
``seeds/XXXXX-User.js``
````js
'use strict';
const { User } = require('../models')
const bcrypt = require('bcrypt')

module.exports = {
  async up (queryInterface, Sequelize) {
    const salt = await bcrypt.genSalt(12)
    const passwordHash = await bcrypt.hash('admin', salt)
    await User.create({
      name: 'Administrador',
      email: 'admin@admin.com',
      password: passwordHash
    });
  },

  async down (queryInterface, Sequelize) {
    await User.findOne({ where: {
      email: 'admin@admin.com'
    }}).destroy()
  }
};
````

## Execução da seed
````sh
sequelize db:seed:all
````

## Rota e resposta de Autenticação da API
``index.js``
````js
app.post('/api/login', async (req, res) => {
    const email = req.body.email
    const password = req.body.password
    const user = await User.findOne({ where: {
        email: email
    }, raw: true })

    if (user) {
        if (bcrypt.compareSync(password, user.password)) {
            jwt.sign({id: user.id}, "@$key@$", (err, token) => {
                if (err) {
                    res.status(500).json({ error: "Erro ao gerar o JWT" })
                }

                res.status(200).json({
                    success: true,
                    token: token
                })
            })
        }
    } else {
        res.status(401).json({success: false})
    } 
})
````

## Middleware para verificação de token
``index.js``
````js
const middlewareValidarJWT = (req, res, next) => {
    const token = req.headers["authorization"]
    jwt.verify(token, "@$key@$", (err, userInfo) => {
        if (err) {
            res.status(403).end()
            return
        }
        req.userInfo = userInfo
        next()
    });
};
````

## Utilizando a middleware de verificação de token
``index.js``
````js
app.use('/api', middlewareValidarJWT, apiRoutes)
````

# CORS
Para resolver o erro do CORS, faça o código abaixo.

``index.js`
````js
const cors = require('cors')
// ...
app.use(cors())
````
