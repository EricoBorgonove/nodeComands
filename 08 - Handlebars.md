# Conceito

Quando estamos desenvolvendo uma aplicação web, é comum que queiramos exibir determinados dados obtidos de alguma fonte (seja um banco de dados, uma API, uma lista, etc). Para essa exibição, normalmente utilizamos de páginas HTML para que sejam renderizadas no navegador.

Porém, a criação de páginas HTML é, muitas vezes, algo improdutivo e ineficiente, principalmente quando precisamos trabalhar com grandes quantidades de dados ou até utilizar recursos das linguagens de programação (for, if, case, etc) nas páginas HTML. Para estes casos, podemos utilizar as template engines (ou view engines).

Basicamente, uma template engine serve para facilitar a criação de páginas HTML e tornar o envio e exibição de informações para estas páginas um processo mais simples e organizado.

[Saiba Mais](https://www.treinaweb.com.br/blog/o-que-e-template-engine)

# Handlebars

Handlebars é um processador de templates (template engine) que gera a tua página HTML dinamicamente, poupando-te o tempo de fazeres atualizações manuais. 

## Instalação

````sh
npm i express-handlebars
````

## Configuração Inicial

Crie uma pasta chamada ``views`` em seu projeto. Dentro dessa pasta, crie um arquivo chamado ``index.handlebars``

``index.handlebars``
````html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Esse é um arquivo do Handlebars</h1>
</body>
</html>
````

O conteúdo do ``index.js`` deve fazer referência a nova template engine que iremos utilizar.

``index.js``
````js
const express = require('express')
const { engine } = require('express-handlebars')

const app = express()

app.engine('handlebars', engine())
app.set('view engine', 'handlebars')

app.get('/', (req, res) => {
    res.render('index', { layout: false })
});

app.listen(8080, () => {
    console.log(`Server running`)
})
````
Agora, ao acessar ``http://localhost:8080/``, você deverá ter na tela um HTML com uma mensagem ``Esse é um arquivo do Handlebars``.

# Layouts
Geralmente nós criamos aplicações em que os componentes são repetidos, principalmente os componentes de footer, menu, header e etc. No Handlebars é possível fazer uso de layouts onde os componentes repetidos podem ser reaproveitados.

Dentro da pasta ``views`` crie uma pasta chamada ``layouts``, dentro dessa pasta crie um arquivo chamado ``main.handlebars``, esse vai ser o nosso layout padrão.

``main.handlebars``
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    {{{body}}}
</body>
</html>
````

Todo o conteúdo de ``{{{body}}}`` será preenchido pela view Handlebars. Agora vamos atualizar a view index.

``index.handlebars``
````html
<h1>Esse é um arquivo do Handlebars</h1>
````

Agora nossa rota não precisa mais fazer referência que não está usando layout.

``index.js``
````js
app.get('/', (req, res) => {
    res.render('index')
});
````

Ao acessar ``http://localhost:8080/`` vemos que o mesmo conteúdo é mostrado, mas agora fazendo uso de um layout. 

# Passagem de Variáveis
Frequentemente você irá precisar passar variáveis do NodeJS para as views. Para fazer isso, precisamos passar um objeto no segundo parâmetro do método ``render``, da seguinte forma:

``index.js``
````js
app.get('/', (req, res) => {
    let usuario = {
        nome: 'Adéliton',
        idade: 30
    }

    res.render('index', {
        user: usuario
    })
});
````

Agora, dentro de ``index.handlebars`` a gente passará a ter acesso a uma variável chamanda ``user``, pois ela foi enviada do backend. 

``index.handlebars``
````html
{{> login-form}}
<h1>Esse é um arquivo do Handlebars</h1>
<p>Você está visualizando informações do usuário: {{ user.nome }} - Idade: {{ user.idade}}</p>
````

Perceba que a viarávei ``user`` não foi declarada no HTML, mas sim no backend. 

# Partials
Partials são componentes do Handlebars que podem ser reaproveitados de forma que o código HTML seja simplificado. Por exemplo, um menu que geralmente contém muito código HTML, pode virar um Partial e ser incluído em uma view de forma mais prática.

Para fazer uso de partials, precisamos criar uma pasta ``partials`` dentro da pasta ``views`` em nosso projeto. Dentro da pasta partials, vamos criar um arquivo chamado ``login-form.handlebars``.

``login-form.handlebars``
````html
<div>
    <input type="text" placeholder="Email">
    <input type="password" placeholder="Senha">

    <button>Fazer Login</button>
    <button>Cadastrar-se</button>
</div>
````

Agora, toda vez que você precisar desse formulário de login, você poderá incluir dentro da sua view através da sintaxe ``{{> NOME_DO_PARTIAL}}``.

``index.handlebars``
````html
{{> login-form}}
<h1>Esse é um arquivo do Handlebars</h1>
````

# Condicionais
Você pode precisar fazer uso de condicionais para renderização do HTML. Para fazer isso dentro do handlebars você precisará da sintaxe ``{{# if}} {{/ if}}``.

``index.js``
````js
app.get('/', (req, res) => {
    res.render('index', {
        auth: false
    })
});
````

``index.handlebars``
````html
<h1>Esse é um arquivo do Handlebars</h1>

{{# if auth }}
    <p>Você está logado</p>
{{ else }}
    <p>Você não está logado</p>
{{/ if }}
````

# Laços de Repetição
É possível criar componentes de forma dinâmica com um array através de laços de repetição. A sintaxe usada é o ``{{# each}} {{/ each}}``.

``index.js``
````js
app.get('/', (req, res) => {
    let users = [
        { nome: "Joao", idade: 18 },
        { nome: "Maria", idade: 21 },
        { nome: "Roberto", idade: 25 }
    ]

    res.render('index', {
        users: users
    })
});
````

``index.handlebars``
````html
<h1>Esse é um arquivo do Handlebars</h1>

<table>
    <tr>
        <th>Nome</th>
        <th>Idade</th>
    </tr>
    
    {{# each users }}
        <tr>
            <td>{{ this.nome }}</td>
            <td>{{ this.idade }}</td>
        </tr>
    {{/ each }}
</table>
````

# With
O with do handlebars possibilita uma maneira fácil de acessar o conteúdo de um objeto no frontend. Altere o conteúdo do ``index.js`` para enviar um objeto com alguns atributos.

``index.js``
````js
app.get('/', (req, res) => {
    let user = {
        nome: 'Adeliton',
        idade: 30,
        sexo: 'Masculino',
        cidade: 'Manaus',
        uf: 'AM',
        pais: 'Brasil'
    }

    res.render('index', {
        user: user
    })
});
````

Agora, através do with, vamos fazer uso desse objeto dentro do handlebars.

``index.handlebars``
````html
<h1>Esse é um arquivo do Handlebars</h1>

<table>
    <tr>
        <th>Nome</th>
        <th>Idade</th>
        <th>Sexo</th>
        <th>Cidade</th>
        <th>UF</th>
        <th>País</th>
    </tr>
    <tr>
        {{# with user }}
            <td>{{ nome }}</td>
            <td>{{ idade }}</td>
            <td>{{ sexo }}</td>
            <td>{{ cidade }}</td>
            <td>{{ uf }}</td>
            <td>{{ pais }}</td>
        {{/ with}}
    </tr>
</table>
````

Com o with você não precisar colocar o nome completo do objeto (``{{user.nome}}``, ``{{user.idade}}``), base você acessar o atributo como se fossem variáveis (``{{nome}}``, ``{{idade}}``).

# Custom Helpers
Custom Helpers são funções que você pode utilizar para melhorar a exibição de elementos JavaScript no seu frontend, assim você retira a regra de negócio do frontend e deixa-a apenas no backend.

Crie uma pasta chamada ``helpers`` na raiz do seu projeto. Dentro dela crie um arquivo chamado ``handlebars.js``.

``handlebars.js``
````js
const helpers = {
    upperCase(content) {
        return content.toUpperCase()
    }
}

module.exports = helpers
````

Agora altere a rota para o seguinte conteúdo.
``index.js``
````js
app.get('/', (req, res) => {
    let user = "Adeliton"

    res.render('index', {
        user: user
    })
});
````

Inclua, no arquivo index.js, o nosso módulo de helper que acabamos de criar.
``index.js``
````js
const helpers = require('./helpers/handlebars')

/* ... */

app.engine('handlebars', engine({
    helpers: helpers
}))
````

Agora, nos arquivos handlebars, passamos a ter acesso a um helper chamado ``upperCase``

``index.handlebars``
````html
<p>{{upperCase user }}</p>
````

## Helpers de scripts
``helpers/handlebars.js``
````js
module.exports = {
    section: function(name, options) {
        if (!this._sections) {
            this._sections = {}
        }
        
        this._sections[name] = options.fn(this)
        return null
    }
}
````

``views/layouts/main.handlebars``
````html
    <!-- -->
    {{{ _sections.scripts }}}
</body>
````

``views/index.handlebars``
````html
{{#section 'scripts'}}
    <script>
        alert('ok')
    </script>
{{/section}}
````

# Desativar bloqueio de ProtoProperies
``index.js``
````js
app.engine('handlebars', engine({
    helpers: helpers,
    runtimeOptions: {
        allowProtoPropertiesByDefault: true,
        allowProtoMethodsByDefault: true,
    },
}))
````
