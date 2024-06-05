# O que é um ORM?
Object-Relational Mapping (ORM), em português, mapeamento objeto-relacional, é uma técnica para aproximar o paradigma de desenvolvimento de aplicações orientadas a objetos ao paradigma do banco de dados relacional. O uso da técnica de mapeamento objeto-relacional é realizado através de um mapeador objeto-relacional que geralmente é a biblioteca ou framework que ajuda no mapeamento e uso do banco de dados.

# Sequelize
O Sequelize é um ORM(Object/Relational Mapper) baseado em Promise para Node.js, e suporta os dialetos PostgreSQL, MySQL, MariaDB, SQLite e MSSQL e recursos a transação, relacionamentos, replicação de leitura e muito mais.

Ele possui um mecanismo de migração (migration) muito poderoso que pode transformar um esquema existente de banco de dados em uma nova versão e também fornece mecanismos de sincronização de banco de dados que podem criar estrutura de banco de dados especificando a estrutura do modelo.

O Sequelize esta disponível via NPM e sua instalação pode ser feita executando o comando no Node.js:  ``npm install sequelize``.

## Dialeto MYSQL
Para utilização do sequelize com o dialeto do mysql é necessário instalar o módulo ``npm install mysql2``. 

## Sequelize Cli
O Sequelize possui um utilitário de linha de comando chamado Sequelize CLI que auxilia em diversas atividades ligadas aos models da nossa aplicação, incluindo funcionalidades para nos ajudar com migrations.

Esse utilitário permite que você gere automaticamente models, que você crie as tabelas no banco e que você crie e execute migrations automaticamente. 

Ao invés de o instalarmos no nosso projeto, vamos instalá-lo de forma global ``npm install -g sequelize-cli``. 

A partir da instalação global, você deve ter acesso a um comando chamado: ``sequelize``, faça um teste usando ``sequelize --version``

# Configurações Iniciais

Na raiz do seu projeto, execute o comando abaixo: 
````
sequelize init
````

Ao fazer esse comando, algumas pastas e arquivos são criados no seu projeto.

``config/config.json``

Esse arquivo contém as credenciais de acesso ao seu banco de dados, como host, user, password e etc.

``migrations``

Nesta pasta ficarão suas migrações. 

> **Migrations** - Assim como você usa sistemas de controle de versão, como o Git, para gerenciar alterações em seu código-fonte, você pode usar migrações para acompanhar as alterações no banco de dados. Com as migrações, você pode transferir seu banco de dados existente para outro estado e vice-versa: essas transições de estado são salvas em arquivos de migração, que descrevem como chegar ao novo estado e como reverter as alterações para voltar ao estado antigo.
> Uma migração no Sequelize é um arquivo javascript que exporta duas funções, up e down, que ditam como realizar a migração e desfazê-la. 

``models``

Nesta pasta ficarão suas models, que serão as classes que farão mapeamento do seu banco de dados. 

``seeders``

Nesta pasta ficarão suas seeders, que são componentes que popularão seu banco de dados com registros.

# Utilizando dotend para credenciais do banco de dados

Para colocarmos nossas credencnais no arquivo ``.env`` do nosso projeto e retirar do arquivo ``config/config.json``, precisamos seguir os seguintes passos. Primeiro editando o arquivo ``.env``.

``.env``
````
DB_USER=root
DB_PASSWORD=root
DB_NAME=nome_do_banco
DB_HOST=localhost
DB_PORT=3306
DB_DIALECT=mysql
````

**Renomeie** o arquivo ``config.json`` para ``config.js`` e coloque o seguinte conteúdo:

``config.js``
````js
require('dotenv').config();

module.exports = {
    development: {
        username: process.env.DB_USER,
        password: process.env.DB_PASSWORD,
        database: process.env.DB_NAME,
        host: process.env.DB_HOST,
        port: process.env.DB_PORT,
        dialect: process.env.DB_DIALECT,
        logging: console.log
    },
    test: {
        username: process.env.DB_USER,
        password: process.env.DB_PASSWORD,
        database: process.env.DB_NAME,
        host: process.env.DB_HOST,
        port: process.env.DB_PORT,
        dialect: process.env.DB_DIALECT,
        logging: console.log
    },
    production: {
        username: process.env.DB_USER,
        password: process.env.DB_PASSWORD,
        database: process.env.DB_NAME,
        host: process.env.DB_HOST,
        port: process.env.DB_PORT,
        dialect: process.env.DB_DIALECT
    }
};
````

Agora precisamos fazer o sequlize reconhecer que gostaríamos de usar as configurações do arquivo ``config.js`` ao invés do padrão ``config.json``.

Para isso, vamos criar um arquivo para configurar essa opção na raiz do nosso projeto.

``.sequelizerc``
````js
const path = require('path');
 
module.exports = {
  'config': path.resolve('config', 'config.js')
}
````

Como a pasta de model foi criada antes dessa nossa configuração, devemos editar a linha 9 do arquivo ``models/index.js`` para puxar nosso arquivo de configuração corretamente.

``ANTES: models/index.js``
````js
const config = require(__dirname + '/../config/config.json')[env];
````

``COMO TEM QUE FICAR: models/index.js``
````js
const config = require(__dirname + '/../config/config.js')[env];
````

# Criando banco de dados

Para criar o banco de dados dentro do mysql e confirmar que as configurações foram feitas com sucesso, execute o seguinte comando:
``
sequelize db:create
``

Se aparecer a mensagem ``Database created``, tudo funcionou corretamente. 

# Criando Migration

O comando para criação de migration é:

``
sequelize migration:generate --name create-pessoas
``

Onde ``pessoas`` é o nome da tabela que você quer criar. Fazendo isso a migration é criada na sua pasta de migrations com a função ``up`` e função ``down``. A função up será executada ao executar a migration, já a down será executada quando a migration for desfeita. 

O conteúdo da migration deverá ser:

````js
'use strict';

module.exports = {
  async up (queryInterface, Sequelize) {
    await queryInterface.createTable('pessoas', {
      id: {
        type: Sequelize.INTEGER,
        autoIncrement: true,
        allowNull: false,
        primaryKey: true
      },
      nome: {
        type: Sequelize.STRING(150),
        allowNull: false
      },
      email: {
        type: Sequelize.STRING(150),
        allowNull: false
      },
      data_nascimento: {
        type: Sequelize.DATEONLY,
        allowNull: true
      },
      createdAt: {
        type: Sequelize.DATE,
        defaultValue: Sequelize.literal('CURRENT_TIMESTAMP')
      },
      updatedAt: {
        type: Sequelize.DATE,
        defaultValue: Sequelize.literal('CURRENT_TIMESTAMP')
      },
    })
  },

  async down (queryInterface, Sequelize) {
    await queryInterface.dropTable('pessoas');
  }
};
````

Para uma lista compela dos tipos possíveis para cada coluna acesse a documentação oficial do [Sequelize](https://sequelize.org/docs/v6/core-concepts/model-basics/)

Agora precisamos executar essa migration para de fato a tabela ser criada em nosso banco de dados.
````
sequelize db:migrate
````

# Criando Seed

O comando para a criação de seed é: ``sequelize seed:generate --name pessoa-teste``, onde ``pessoa-teste`` é o nome da Seed que você está criando. Fazendo esse comando, sua seed será criada na pasta ``seeders``.

O conteúdo deverá ser o seguinte: 

````js
'use strict';

module.exports = {
  async up (queryInterface, Sequelize) {
    await queryInterface.bulkInsert('pessoas', [
      {
        nome: 'João da Silva Lima',
        email: 'joao@joao.com',
        data_nascimento: new Date('1990-01-31')
      }
    ], {});
  },

  async down (queryInterface, Sequelize) {
    await queryInterface.buldDelete('pessoas', {email: 'joao@joao.com'}, {})
  }
};
````

Para executar de fato a criação do registro, você deve executar o seguinte comando

````
sequelize db:seed --seed XXXXXXXXXXXXXX-nome-seed.js
````

Onde XXXXXXXXXX-nome-seed é o nome da seed criada, exatamente igual, com os números. 

## Exemplo de composição de uma seed
````js
return queryInterface.bulkInsert('Users', [{
      name: 'Administrador',
      email: 'admin@admin.com',
      username: 'admin',
      password: passwordHash,
      status: 'A',
      last_login: null,
      created_at: new Date(),
      updated_at: new Date()
    }]);
````

# Criando a Model

Como explicado antes, a Model é o mapeamento do seu banco de dados, com as colunas e os métodos responsáveis para fazer manipulação dele. O comando para a criação da model é:

````
sequelize model:create --name Pessoa --attributes nome:string,email:string,data_nascimento:dateonly 
````

Onde ``Pessoa`` é o nome da model. Procure seguir um padrão. Um padrão sugerido é a model começar com letra maíscula e ser no singular. Os valores ao lado de ``attributes`` são as colunas da sua tabela, que serão representadas pela model.

> **ATENÇÃO:** O comando acima também cria uma migration, como já havíamos criado anteriormente, você pode excluir essa migration criada. A ordem padrão é primeiro o comando acima, pois ele já cria a model e a migration. Foi feito de forma invertida nesse material por questões didáticas. 

``pessoa.js``
````js
'use strict';
const {
  Model
} = require('sequelize');
module.exports = (sequelize, DataTypes) => {
  class Pessoa extends Model {
    /**
     * Helper method for defining associations.
     * This method is not a part of Sequelize lifecycle.
     * The `models/index` file will call this method automatically.
     */
    static associate(models) {
      // define association here
    }
  }
  Pessoa.init({
    nome: DataTypes.STRING,
    email: DataTypes.STRING,
    data_nascimento: DataTypes.DATEONLY
  }, {
    sequelize,
    modelName: 'Pessoa',
    tableName: 'pessoas' /* NOME DA TABELA NO BANCO DE DADOS */
  });
  return Pessoa;
};
````

Agora podemos fazer manipulação dos registros utilizando a model.

# Manipulação de Registros
Para a manipulação dos registros, iremos fazer uso completo do padrão MVC. Por isso, crie um ``PessoaController.js``.

## Visualizar Todos os Registros

O método ``model.findAll()`` retorna todos os registros que estão na tabela em um array de objetos.

````js
static async index(req, res) {
    const pessoas = await Pessoa.findAll({ raw: true })

    res.render('pessoa/index', {
        pessoas: pessoas
    })
}
````

## Visualizar um Registro Específico

O método ``model.findByPk()`` retorna o registro específico com a chave primária passada como parâmetro.

````js
static async show(req, res) {
    const pessoa = await Pessoa.findByPk(1, { raw: true })

    res.render('pessoa/index', {
        pessoa: pessoa
    })
}
````

## Criar um Registro

O método ``model.create()`` recebe como parâmetro um objeto e cria um registro no banco de dados com as informações contidas no objeto.

````js
static async create(req, res) {
    const pessoa = await Pessoa.create({
        nome: "Maria Pereira da Silva",
        email: "maria@maria.com",
        data_nascimento: new Date('1980-12-24')
    })

    res.render('pessoa/index', {
        pessoa: pessoa
    })
}
````

## Atualizar um registro

O método ``model.save()`` atualiza qualquer coluna que for alterada diretamente no objeto.

````js
static async update(req, res) {
    const pessoa = await Pessoa.findByPk(1)
    pessoa.nome = "Joaquina da Silva"
    await pessoa.save()

    res.render('pessoa/index', {
        pessoa: pessoa
    })
}
````

## Excluir um registro

O método ``model.destroy()`` exclui um registro no banco de dados. 

````js
static async destroy(req, res) {
    const pessoa = await Pessoa.findByPk(1)
    await pessoa.destroy()

    res.render('pessoa/index', {
        pessoa: pessoa
    })
}
````

> Para ver outros métodos que o Sequelize traz para manipulação de dados, veja a [documentação oficial do Sequelize](https://sequelize.org/docs/v6/core-concepts/model-querying-basics/)

## Limpando caracteres e corrigindo formato de data

````js
    static async store(req, res) {
        try {
            await Pessoa.create({
                nome: req.body.nome,
                email: req.body.email,
                data_nascimento: req.body.data_nascimento.split('/').reverse().join('-'),
                salario: req.body.salario.replace(".", "").replace(",", ".")
            })
         
            res.redirect('/pessoa')
        } catch (e) {
            console.log(e)
        }
    }
````

# Getters e Setters
Sequelize permite definir getters e setters personalizados para os atributos das models.

O Sequelize também permite que você especifique os chamados atributos virtuais, que são atributos no Modelo de Sequelize que realmente não existem na tabela SQL subjacente, mas são preenchidos automaticamente pelo Sequelize. Eles são muito úteis para criar atributos personalizados que também podem simplificar seu código, por exemplo.

``models/pessoa.js``
````js
  Pessoa.init({
    nome: DataTypes.STRING,
    data_nascimento: {
      type: DataTypes.DATEONLY,
      get() {
        const rawValue = this.getDataValue('data_nascimento')
        return rawValue ? rawValue.split('-').reverse().join('/') : null
      },
      set(value) {
        const rawValue = value ? value.split('/').reverse().join('-') : null
        this.setDataValue('data_nascimento', rawValue)
      }
    },
    email: DataTypes.STRING(80),
    salario: {
      type: DataTypes.DECIMAL(10,2),
      set(value) {
        const rawValue = value ? value.replace(".", "").replace(",", ".") : null
        this.setDataValue('salario', rawValue)
      }
    }
  }, {
    sequelize,
    modelName: 'Pessoa'
  });
````

No exemplo acima os campos ``data_nascimento`` e ``salario`` fazem uso desse recurso. Um ``get`` e ``set`` e outro apenas ``set``, respectivamente. Para conseguir visualizar os registros atualizados pelo get, você deve acessá-los em forma de atributo, sem fazer utilização do ``raw``. Da seguinte forma:

````js
    static async edit(req, res) {
        const pessoa = await Pessoa.findByPk(req.params.id)
        res.render('pessoa/edit', {
            pessoa: {
                id: pessoa.id,
                nome: pessoa.nome,
                email: pessoa.email,
                data_nascimento: pessoa.data_nascimento,
                salario: pessoa.salario
            }
        })
    }
````

Ou com o findAll() (Se você estiver usando o handlebars, pode ser necessário desativar a proteção de ProtoProperies.

````js
    static async index(req, res) {
        const pessoas = await Pessoa.findAll()
        res.render('pessoa/index', {
            pessoas: pessoas
        })
    }
````
