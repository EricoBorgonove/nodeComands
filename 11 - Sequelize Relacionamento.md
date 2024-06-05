# Introdução
O Sequelize suporta as associações padrão: One-To-One (Um para um), One-To-Many (Um para muitos) e Many-To-Many (Muitos para muitos).

Para isso, o Sequelize fornece quatro tipos de associações que devem ser combinadas para criá-las:

* A associação HasOne (Tem um - na model pai para a model filha)
* A associação BelongsTo (Pertence a um - na model filha para a model pai)
* A associação HasMany (Tem muitos - na model pai para as models filhas)
* A associação BelongsToMany (Pertence a muitos - na model pai para a model filha com tabelas pivot)

# Chaves Estrageiras
Para a criação de chaves estrangeiras, precisamos entender como é feito dentro da migration.

````js
pessoaId: {
  type: Sequelize.INTEGER,
  references: {
    model: {
      tableName: 'pessoas'
    },
    key: 'id',
    onUpdate: 'RESTRICT',
    onDelete: 'RESTRICT'
  },
  allowNull: true
},
````

Esse é o padrão estabelecido para a criação de chaves estrangeiras pelo sequelize: ``tabelaId``

# Relacionamentos Um para Um
## hasOne
O relacionamento na model pai para a model filho, considerando que tenha apenas um filho.
````js
class Pessoa extends Model {
    static associate(models) {
      this.hasOne(models.Telefone, {
        as: 'telefone'
      })
    }
  }
````

Esse relacionamento irá considerar que na tabela ``telefones`` tenha um relacionamento para a tabela ``pessoas`` através de uma coluna foreign key chamada ``pessoaId``.

Agora você conseguirá acessar a informação através de: 
````js
const pessoa = await Pessoa.findByPk(1, {
    include: 'telefone'
})

console.log(pessoa.telefone)
````

## belongsTo
O relacionamento na model filho para a model pai
````js
class Telefone extends Model {
    static associate(models) {
      this.belongsTo(models.Pessoa, {
        as: 'pessoa'
      })
    }
  }
````
Esse relacionamento irá considerar que na tabela ``telefones`` tenha um relacionamento para a tabela ``pessoas`` através de uma coluna foreign key chamada ``pessoaId``.

Agora você conseguirá acessar a informação através de: 
````js
const telefone = await Telefone.findByPk(1, {
    include: 'pessoa'
})

console.log(telefone.pessoa)
````

## hasMany
O relacionamento na model pai para a model filho, considerando que a model pai poderá ter vários registros filhos
````js
class Pessoa extends Model {
    static associate(models) {
      this.hasMany(models.Telefone, {
        as: 'telefones'
      })
    }
  }
````
Esse relacionamento irá considerar que na tabela ``telefones`` tenha um relacionamento para a tabela ``pessoas`` através de uma coluna foreign key chamada ``pessoaId``. Sendo que uma pessoa poderá ter vários telefones. 

Agora você conseguirá acessar a informação através de: 
````js
const pessoa = await Pessoa.findByPk(1, {
    include: 'telefones'
})

console.log(pessoa.telefones)
````

## belongsToMany
O relacionamento na model pai para a model filho, considerando que entre as models há um pivot, ou seja, um relacionamento N:M.
````js
class Pessoa extends Model {
    static associate(models) {
      this.belongsToMany(models.Departamento, {
        through: 'pessoaDepartamento',
        as: 'departamentos'
      })
    }
  }
````
Esse relacionamento irá considerar que haverão três tabelas: ``pessoas``, ``departamentos`` e ``pessoaDepartamento``, permitindo que uma pessoa possa estar em vários departamentos e um departamento pode ter várias pessoas. 

Agora você conseguirá acessar a informação através de: 
````js
const pessoa = await Pessoa.findByPk(1, {
    include: 'departamentos'
})

console.log(pessoa.departamento)
````
