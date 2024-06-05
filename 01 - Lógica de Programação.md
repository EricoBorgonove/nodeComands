Tabela de Conteúdo
===================
- [Tabela de Conteúdo](#tabela-de-conteúdo)
- [Introdução](#introdução)
  - [Ferramentas de Desenvolvedor do Google Chrome](#ferramentas-de-desenvolvedor-do-google-chrome)
- [Programação Procedural](#programação-procedural)
  - [Operações Matemáticas](#operações-matemáticas)
  - [Cálculo de Idade com JavaScript](#cálculo-de-idade-com-javascript)
  - [Variáveis](#variáveis)
  - [Tipos de Variáveis](#tipos-de-variáveis)
  - [Interagindo com o Usuário](#interagindo-com-o-usuário)
    - [alert](#alert)
    - [confirm](#confirm)
    - [prompt](#prompt)
  - [Criando Nossas Próprias Funções](#criando-nossas-próprias-funções)
  - [Estruturas de Decisão](#estruturas-de-decisão)
  - [Trabalhando com Arrays](#trabalhando-com-arrays)
  - [Estruturas de Repetição](#estruturas-de-repetição)
    - [for](#for)
    - [while](#while)
    - [do... while](#do-while)
    - [Métodos da Classe Array](#métodos-da-classe-array)
- [Lógica de Programação Orientada a Opjetos](#lógica-de-programação-orientada-a-opjetos)
  - [Classes, Objetos e Atributos](#classes-objetos-e-atributos)
  - [Encapsulamento](#encapsulamento)
  - [Herança](#herança)
    - [Exemplo de classe vendedor com comissão](#exemplo-de-classe-vendedor-com-comissão)
  - [Classes Especiais JavaScript](#classes-especiais-javascript)
    - [Método Push](#método-push)
- [Projeto Prático - Programa Escolar](#projeto-prático---programa-escolar)

# Introdução
A base da ciência da computação e da programação é o algoritmo. Quando falamos em programar, falamos, basicamente, em construir um algoritmo. Todo programa de um computador é montado por algoritmos que resolvem problemas matemáticos lógicos com objetivos específicos.
Algoritmo é um conjunto das regras e procedimentos lógicos perfeitamente definidos que levam à solução de um problema em um número finito de etapas.
Vamos montar um algoritmo de um personagem tentando chegar até sua casa:
1. Inicia a caminhada.
2. Decide se vai pelo caminho mais curto ou mais longo.
3. Se for pelo caminho mais curto, precisará passar por uma ponte quebrada.
4. Se cair da ponte, repete a tentativa de passagem. Até conseguir passar.
5. Chega a casa.

Neste algoritmo de exemplo encontramos conceitos importantes da programação.
## Ferramentas de Desenvolvedor do Google Chrome
Os navegadores modernos possuem um console de desenvolvedor. O console é uma ferramenta incrível. Seja para executar um código on the fly, inspecionar ou interagir com elementos de uma página, ou até mesmo para conferir se há mensagens de erros.

No nosso curso faremos uso do console de desenvolvedor do Google Chrome para brincarmos com nosso código. Para ativar o console de desenvolvedor do Google Chrome você deve ir em ``Opções > Mais Ferramentas > Ferramentas do Desenvolvedor``. Ou pressionar as teclas de atalho ``CTRL + SHIFT + J`` ou ainda simplesmente a tecla ``F12``. No console é possível executarmos código **JavaScript**.

````js
56 + 43
````

Ao pressionar ``ENTER`` o console executa o código escrito. Para digitar em uma nova linha é recomendado o uso do ``SHIFT + ENTER``.

Para um playground mais completo, você pode utilizar o [JsBin](http://jsbin.com/?js,console). É recomendado o JsBin para testes maiores. 

# Programação Procedural

## Operações Matemáticas

Com o JavaScript é possível executarmos diversos tipos de operações matemáticas:

````js
34 + 11 // Soma
8 - 3 // Subtração
81 / 9 // Divisão
4 * 3 // Multiplicação
3 > 2 // Maior
7 < 10 // Menor
19 >= 8 // Maior Igual
34 <= 34 // Menor Igual
(9 - 3) * 4 // Alterar a Ordem de Operações
````

## Cálculo de Idade com JavaScript

No console do Google Chrome, faça um programa que calcule a idade que cada integrante da sua família terá até o fim deste ano.

````js
2021 - 1992 // Minha idade
2021 - 1995 // Idade da minha irmã
2021 - 1987 // Idade do meu irmão
2021 - 1964 // Idade do meu pai
2021 - 1973 // Idade da minha mãe
````

Porém temos um problema. Este nosso sistema só funciona para o ano de 2021. Supondo que hoje seja 01 de Janeiro de 2022, precisamos atualizá-lo. Mas temos outro problema: temos que alterar cinco vezes nosso código com a mesma informação. Para solucionar isso precisamos transformar o ano em uma variável. 

## Variáveis

Uma variável é um espaço na memória do computador destinado a um dado que é alterado durante a execução do algoritmo. Para criar uma variável no JavaScript devemos usar o ``var`` ou o ``let``. Exemplos:

````js
var meuNome;
let idade;
let meuNumero = 5;
var endereco = "Rua 123, 1 - Centro - Manaus/AM"; 
let 1exemplo; // Uncaught SyntaxError: Invalid or unexpected token
````

## Tipos de Variáveis

1. **Strings** — Uma String nada mais é que texto puro.
2. **Numbers** — São os números, seja eles integer, float, double etc.
3. **Booleans** — São os operadores booleanos (true ou false)
4. **Arrays** — É uma estrutura de dado para armazenar uma coleção de valores, sendo eles de qualquer tipo.
5. **Objects** — Conjunto de atributos aninhados a uma variável denomina-se um objeto.
6. **Functions** — Em JavaScript é possível declarar uma variável como uma função, podendo fazer operações e retornando o valor para a variável de declaração. Obs: muito utilizado no paradigma de programação funcional.

Portanto agora podemos transformar o ano atual é uma variável:

````js
var anoAtual = 2021;
anoAtual - 1992 // Minha idade
anoAtual - 1995 // Idade da minha irmã
anoAtual - 1987 // Idade do meu irmão
anoAtual - 1964 // Idade do meu pai
anoAtual - 1973 // Idade da minha mãe
````

Agora, considerando que hoje seja 01 de Janeiro de 2022, basta alterarmos o valor da variável ``anoAtual`` e nosso código voltará a funcionar.

## Interagindo com o Usuário

### alert
O alert é uma das mais simples caixas de diálogo, com uma aparência simples e intuitiva elas são muito usadas em validações de formulários e/ou bloqueio de ações do browser.

Sua principal função é mostrar ao usuário uma mensagem e um botão de confirmação de que o usuário tenha visto a mensagem. Para chamar essa função, basta utilizarmos o código ``alert()``, que receberá uma string(mensagem que será exibida ao usuário).

````js
alert("Eu sou um alert!");
````

### confirm
A função de confirmação é um pouco diferente da função alert em Javascript, dessa vez são exibidos dois botões, um de OK e outro de CANCELAR, separados por valores true (verdadeiro) e false (falso).

````js
confirm('Deseja realmente deletar este registro?'))
````

### prompt
O prompt é um pouco diferente do alert() e do confirm(), pois ele necessita que o usuário insira algum valor, ou seja, precisa de uma interação direta do usuário para que ele funcione.

Para chamarmos a função utilizamos o prompt(), o qual irá receber uma string(mensagem) que será exibida, normalmente em forma de pergunta, ao usuário. A função sempre irá retornar um valor, tudo que o usuário digitar no campo input será convertido em valor e será retornado na função.

````js
var idade = prompt("Digite sua idade: ");
````

Agora que sabemos solicitar dados do usuário, vamos pedir para o usuário digitar o ano de nascimento:

````js
var anoAtual = 2021;
var anoNascimento = prompt("Digite o seu ano de nascimento: ");
anoAtual - anoNascimento;
````

## Estruturas de Decisão 
Imagina se além de mostrarmos a idade atual do integrante da nossa família, precisarmos também mostrar se ele é maior de idade. Para isso precisaremos usar as estruturas de decisão ``if`` e ``else``. 
````js
var anoNascimento = prompt("Digite o seu ano de nascimento: ");
var idade = anoAtual - anoNascimento;
alert("Sua idade em " + anoAtual + " é " + idade + " anos.");
if (idade >= 18) {
  alert("Você é maior de idade");
} else {
  alert("Você é menor de idade");
}
````
Há ainda o ``else if``, que funciona como o else, porém adiciona uma checagem.

````js
if (idade >= 18) {
  alert("Você é menor de idade");
} else if (idade >= 1) {
  alert("Você é menor de idade");
} else {
  alert("Você é apenas um bebê");
}
````

# Exercícios

1. Crie 5 variáveis de cada tipo abaixo:
- Number
- String
- Boolean
2. Escreva um programa que receba dois valores do usuário, some eles e exiba a soma final.
3. Escreva um programa que receba o valor do lado de um quadro em cm e calcule o perímetro do quadrado.
4. Escreva um programa que receba um número inteiro e calcule o quadrado desse número.
5. Escreva um programa que receba um valor em horas e que calcule quantos segundos há nesse valor.
6. Escreva um programa que receba a idade de uma pessoa e classifique ela como: Criança (0 a 10 anos), Adolescente (11 a 15 anos), Jovem (16 a 18 anos), Adulto (19 a 60 anos) e Idoso (61 anos ou mais)
7. Escreva um programa que receba a velocidade do carro em km/h e calcule a multa recebida pelo motorista. A regra é a segunte, o limite da via é 60 km/h, para cada km excedido o motorista irá receber R$ 3,99 de multa.
8. Escreva um programa que receba a quantidade de litros que um motorista abasteceu o carro dele e calcule o valor que ele irá pagar. Ele poderá escolher entre álcool e gasolina. O valor do álcool é R$ 4,01 por litro e o valor da gasolina é R$ 5,99 por litro.
9. Escreva um programa que receba dois valores. Após isso, o usuário deverá escolher se deseja somar, subtrair, dividir ou multiplicar esses valores. O resultado final deverá ser exibido. 
10. Escreva um programa que faça uma pergunta para o usuário e dê 5 alternativas. O usuário deverá escolher uma alternativa e você deverá dizer se a alternativa está certa ou errada. 

## Criando Nossas Próprias Funções

Vamos transformar o nosso sistema de cálculo de idade em uma função. Assim nós podemos reutilizar nosso código sem precisar rescrevê-lo.

````js
function calcularIdade() {
  var anoAtual = 2021;
  var anoNascimento = prompt("Digite o seu ano de nascimento: ");
  var idade = anoAtual - anoNascimento;
  alert("Sua idade em " + anoAtual + " é " + idade + " anos.");
}

calcularIdade();
````
Para que nossa função não fique defasada, podemos adicionar o ano atual como parâmetro opcional.
````js
function calcularIdade(anoAtual = 2021) {
  var anoNascimento = prompt("Digite o seu ano de nascimento: ");
  var idade = anoAtual - anoNascimento;
  alert("Sua idade em " + anoAtual + " é " + idade + " anos.");
}
````
Alterando a chamada do nosso programa, agora é possível utilizarmos o seguinte código para calcular a idade de todos da nossa família
````js
calcularIdade() // Minha idade
calcularIdade() // Idade da minha irmã
calcularIdade() // Idade do meu irmão
calcularIdade() // Idade do meu pai
calcularIdade() // Idade da minha mãe
````

## Estruturas de Decisão na função
````js
function calcularIdade(anoAtual = 2021) {
  var anoNascimento = prompt("Digite o seu ano de nascimento: ");
  var idade = anoAtual - anoNascimento;
  alert("Sua idade em " + anoAtual + " é " + idade + " anos.");
  if (idade >= 18) {
    alert("Você é maior de idade");
  } else {
    alert("Você é menor de idade");
  }
}
````
Vamos suporte que nosso programa chamou a atenção de grandes investidores do mercado e eles querem comprá-lo para calcular a idade da família deles. Precisaremos fazer algumas alterações no nosso código. Principalmente pelo fato de não sabermos quantas vezes a função ``calcularIdade()`` será chamada, pois depende da quantidade de integrantes da familía do investidor. Para isso precisaremos trabalhar com ``arrays``. 

## Funções com retorno de valores
````js
function calculaIdade(anoNascimento) {
  return 2021 - anoNascimento;
}

var idade = calculaIdade(1992);
alert(idade);
````

## Trabalhando com Arrays

Com o Array é possível armazenar um conjunto de quaisquer valores javascript, como números, caracteres, textos ou uma mistura deles. Imagine o array como um gaveteiro onde você pode adicionar ou retirar gavetas e cada gaveta comtém o objeto que quiser, vamos criar aqui um gaveteiro onde a primeira gaveta contém o valor 10, a segunda 20 e a terceira 30.
````js
var  gaveteiro = [10, 20, 30];
````
Se eu precisar saber o valor de um único gaveteiro, eu posso chamar o gaveteiro pela sua numeração, que chamamos de ``indice`` ou ``index``, em inglês. No caso do Javascript (e de grande parte das linguagens de programação web), o array começa com o índice 0.
````js
alert(gaveteiro[0]); // 10
alert(gaveteiro[2]); // 30
alert(gaveteiro[3]); // undefined
````

Portanto temos uma única variável com diversos valores. Ideal para se trabalhar com dados em que não se sabe a quantidade de informação que estará contida. Alterando nosso programa, vamos primeiramente ter um array com o ano de nascimento de todos os integrantes da nossa família.
````js
var minhaFamilia = [1992, 1995, 1987, 1964, 1973];
````
Agora precisaremos percorrer o array para calcular a idade de cada integrante da nossa família. Para isso precisaremos utilizar os ``Comandos de Repetição``.

## Estruturas de Repetição

### for 
A instrução for cria um loop que consiste em três expressões opcionais, dentro de parênteses e separadas por ponto e vírgula, seguidas por uma declaração ou uma sequência de declarações executadas em sequência.
````js
for (var i = 0; i < 9; i++) {
   console.log(i);
}
````
### while
A declaração while cria um laço que executa uma rotina especifica enquanto a condição de teste for avaliada como verdadeira. A condição é avaliada antes da execução da rotina.
````js
var n = 0;
while (n < 3) {
  console.log(n);
  n++;
}
````
### do... while
A declaração do...while cria um laço que executa uma declaração até que o teste da condição for falsa (false). A condição é avaliada depois que o bloco de código é executado, resultando que uma declaração seja executada pelo menos uma vez.
````js
var n = 3;
do {
  console.log(n);
  n++;
} while (n < 3);
````
### Métodos da Classe Array
Ao criar um array no JavaScript, esse array vai automaticamente um objeto da class Array. Portanto, como um objeto de uma classe, é possível utilizarmos propriedades e métodos que nos auxiliam no nosso trabalho com arrays. 
````js
typeof minhaFamilia; // object
````
Um dos métodos da classe Array é o ``forEach``. Para trabalhar com arrays, o método forEach é um dos mais indicados. Veja a sintaxe abaixo:
````js
var minhaFamilia = [1992, 1995, 1987, 1964, 1973];

minhaFamilia.forEach(function(value, index) {
    console.log("Index da iteração: " + index); 
    console.log("Valor da iteração: " + value);
});
````
Para cada valor do array há uma iteração. 
Agora nós podemos adicionar nossa verificação de idade dentro de cada iteração do array. Da seguinte forma:
````js
var minhaFamilia = [1992, 1995, 1987, 1964, 1973];

minhaFamilia.forEach(function(value, index) {
    var anoAtual = 2021;
    var idade = anoAtual - value;
    console.log(idade);
});
````
Podemos adicionar a verificação se o integrante da família é maior de idade ou não. 
````js
var minhaFamilia = [1992, 1995, 1987, 1964, 1973];

minhaFamilia.forEach(function(value, index) {
    var anoAtual = 2021;
    var idade = anoAtual - value;
    alert("Sua idade em " + anoAtual + " é " + idade + " anos.");
    if (idade >= 18) {
      alert("Você é maior de idade");
    } else {
      alert("Você é menor de idade");
    }
});
````
Agora fica mais fácil adicionar um integrante à família. 

# Lógica de Programação Orientada a Opjetos
A maioria das linguagens modernas são fundamentadas em um ideal (também chamado paradigma) de codificação que possibilita a escrita de um código mais "humano", de manutenção mais fácil e que também possibilite um alto nível de reaproveitamento de código, o que certamente nos dá maior velocidade no processo de desenvolvimento. Esse paradigma é conhecido como Paradigma Orientado a Objetos ou simplesmente Orientação a Objetos.
## Classes, Objetos e Atributos
Imagine que você comprou um carro recentemente e decide modelar esse carro usando programação orientada a objetos. O seu carro tem as características que você estava procurando: um motor 2.0 híbrido, azul escuro, quatro portas, câmbio automático etc. Ele também possui comportamentos que, provavelmente, foram o motivo de sua compra, como acelerar, desacelerar, acender os faróis, buzinar e tocar música. Podemos dizer que o carro novo é um **objeto**, onde suas características são seus **atributos** (dados atrelados ao objeto) e seus comportamentos são **ações ou métodos**.

Seu carro é um objeto seu, mas na loja onde você o comprou existiam vários outros, muito similares, com quatro rodas, volante, câmbio, retrovisores, faróis, dentre outras partes. Observe que, apesar do seu carro ser único (por exemplo, possui um registro único no Departamento de Trânsito), podem existir outros com exatamente os mesmos atributos, ou parecidos, ou mesmo totalmente diferentes, mas que ainda são considerados carros. Podemos dizer então que seu objeto pode ser **classificado** (isto é, **seu objeto pertence à uma classe**) como um carro, e que seu carro nada mais é que uma **instância dessa classe chamada "carro"**.

Assim, abstraindo um pouco a analogia, uma classe é um conjunto de características e comportamentos que definem o conjunto de objetos pertencentes à essa classe. Repare que a classe em si é um conceito abstrato, como um molde, que se torna concreto e palpável através da criação de um objeto. Chamamos essa criação de instanciação da classe, como se estivéssemos usando esse molde (classe) para criar um objeto.

Exemplo de classe com JavaScript

````js
class Carro {
  constructor(modelo) {
    this.modelo = modelo;
    this.velocidade = 0;
    this.farolAceso = false;
  }
  
  acelerar() {
    this.velocidade = 60;
  }

  acenderFarol() {
    this.farolAceso = true;
  }
}
````
Para utilizarmos essa classe, precisamos criar uma instância dela, ou seja, um objeto.
````js
var meuCarro = new Carro("Ford Ka");
console.log(meuCarro.velocidade);
meuCarro.acelerar();
console.log(meuCarro.velocidade);
````
Edite o código de tal forma que tenha os métodos ``desligarFarol()`` e ``frear()``.
<details> 
  <summary>Clique para visualizar o resultado</summary>

  ````js
  class Carro {
    constructor(modelo) {
      this.modelo = modelo;
      this.velocidade = 0;
      this.farolAceso = false;
    }
    
    acelerar() {
      this.velocidade = 60;
    }

    acenderFarol() {
      this.farolAceso = true;
    }

    desligarFarol() {
      this.farolAceso = false;
    }

    frear() {
      this.velocidade = 0;
    }
  }
  ````
</details>

## Encapsulamento
Ainda usando a analogia do carro, sabemos que ele possui atributos e métodos, ou seja, características e comportamentos. Os métodos do carro, como acelerar, podem usar atributos e outros métodos do carro como o tanque de gasolina e o mecanismo de injeção de combustível, respectivamente, uma vez que acelerar gasta combustível. 

No entanto, se alguns desses atributos ou métodos forem facilmente visíveis e modificáveis, como o mecanismo de aceleração do carro, isso pode dar liberdade para que alterações sejam feitas, resultando em efeitos colaterais imprevisíveis. Nessa analogia, uma pessoa pode não estar satisfeita com a aceleração do carro e modifica a forma como ela ocorre, criando efeitos colaterais que podem fazer o carro nem andar, por exemplo.

Dizemos, nesse caso, que o método de aceleração do seu carro não é visível por fora do próprio carro. Na POO, um atributo ou método que não é visível de fora do próprio objeto é chamado de "privado" e quando é visível, é chamado de "público".

No nosso exemplo, como o usuário não altera a velocidade diretamente, podemos colocar o atributo ``velocidade`` como privado. O mesmo serve para o atributo ``farolAceso``. Adicionamos mais métodos privados.

````js
class Carro {
  #velocidade;
  #farolAceso;

  constructor(modelo) {
    this.modelo = modelo;
    this.#velocidade = 0;
    this.#farolAceso = false;
  }
  
  acelerar() {
    if (this.#estaParado()) {
      this.#velocidade = 60;
    } else {
      alert("O carro já está em movimento");
    }
  }

  acenderFarol() {
    this.#farolAceso = true;
  }

  desligarFarol() {
    this.#farolAceso = false;
  }

  frear() {
    if (this.#estaParado()) {
      alert("O carro já está parado");
    } else {
      this.#velocidade = 0;
    } 
  }

  #estaParado() {
    return this.#velocidade == 0;
  }
}
````
## Herança
No nosso exemplo, você acabou de comprar um carro com os atributos que procurava. Apesar disso ser único, existem outros objetos com algumas ações e atributos que se assemelham com os do seu carro. Como no caso de uma moto. A moto e o carro aceleram e ligam o farol, portanto os métodos e atributos podem ser reaproveitados. Este é o barato da orientação a objetos!

Para isto devemos utilizar o ``extends``. 

````js
class MeioDeTransporte {
  #velocidade;
  #farolAceso;

  constructor(modelo) {
    this.modelo = modelo;
    this.#velocidade = 0;
    this.#farolAceso = false;
  }
  
  acelerar() {
    if (this.#estaParado()) {
      this.#velocidade = 60;
    } else {
      alert("O carro já está em movimento");
    }
  }

  acenderFarol() {
    this.#farolAceso = true;
  }

  desligarFarol() {
    this.#farolAceso = false;
  }

  frear() {
    if (this.#estaParado()) {
      alert("O carro já está parado");
    } else {
      this.#velocidade = 0;
    } 
  }

  #estaParado() {
    return this.#velocidade == 0;
  }
}

class Carro extends MeioDeTransporte {

}

class Moto extends MeioDeTransporte {

}

var meuCarro = new Carro("Ford Ka");
meuCarro.acelerar();

var minhaMoto = new Moto("Honda");
minhaMoto.acelerar();

````

### Exemplo de classe vendedor com comissão
````js
class Vendendor{
  
  constructor () {
    this.vendas = [];
  }
  
  adicionarVenda(valor) {
    this.vendas.push(valor);
  }
  
  informaNivel() {
    this.#calculaVendas();
    
    if (this.vendasTotal <= 1000) {
      alert("Nivel 1")
    } else {
      alert ("Nivel 2")
    }
  }
  
  mereceCarro() {
    this.#calculaVendas();
    
    if (this.vendasTotal >= 2000) {
      alert("Merece o carro");
    } else {
      alert("Não merece o carro");
    }
  }
  
  #calculaVendas() {
    var meuObjeto = this;
    this.vendasTotal = 0;
    this.vendas.forEach(function (valor) {
      meuObjeto.vendasTotal = meuObjeto.vendasTotal+ valor;
    });   
  }
}

var joao = new Vendendor();
joao.adicionarVenda(200);
joao.adicionarVenda(350);
joao.adicionarVenda(250);
joao.adicionarVenda(650);

joao.informaNivel();
joao.mereceCarro();

console.log(joao)
````


## Classes Especiais JavaScript
Quando criamos um array no JavaScript, como fizemos com o array ``minhaFamilia``, estamos na verdade instanciando um objeto da classe ``Array``. É por isso que é possível utilizarmos métodos especiais para trabalhar com o array, como fizemos com o ``forEach``. 

Uma lista completa dos métodos e dos atributos que podemos utilizar da classe Array pode ser encontrada [Neste Site](https://www.w3schools.com/jsref/jsref_obj_array.asp).

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/String/substring

Da mesma forma, quando criamos um objeto no JavaScript, estamos na verdade instanciando um objeto da classe ``Object``. Como podemos ver no seguinte exemplo:

````js
var pessoa = {
  nome: "Adéliton Fernandes", 
  sexo: "Masculino",
  idade: 29
};

pessoa.nome;
console.log(pessoa.constructor.name); // "Object"
````

### Método Push
Outro método bastante importante da classe Array é o push. Este método adiciona novos itens no final de um array. Veja o exemplo abaixo:
````js
var minhaFamilia = [1992, 1995, 1987, 1964, 1973];
minhaFamilia.push(2001);
console.log(minhaFamilia); // (6) [1992, 1995, 1987, 1964, 1973, 2001]
````

# Projeto Prático - Programa Escolar

**Nossa História de Usuário:**

> Como gerente de uma escola do ensino médio quero salvar o nome, a idade e as notas bimestrais dos meus alunos, para que, no final, eu possa saber o nome do aluno que obteve a maior média e o nome do aluno mais novo, para que eu possa premiá-los no final.

**Requisitos Técnicos:**
* Você deve utilizar Programação Orientada a Objetos
* Suas classes devem utilizar encapsulamento correto
* Seu código deve ser possível cadastrar um número indefinido de alunos

# Projeto Prático - Controle de Estoque

````js
/*
Criar um sistema de controle de estoque para a Casas Bahia.

Notebook -> Marca, Modelo, Ano, Preço, Estoque, Quantidade de RAM
Geladeira -> Marca, Modelo, Ano, Preço, Estoque, Frost Free
Televisão -> Marca, Modelo, Ano, Preço, Estoque, Smart ou Não
Maquina de Lavar -> Marca, Modelo, Preço, Estoque, Capacidade
*/

adicionarEstoque()
retirarDoEstoque()
estoqueAtual()
````

````js
// noprotect

class Produto {
  marca;
  modelo;
  preco;
  #estoque = 0;
  #ano;

  constructor(marca, modelo, preco) {
    this.marca = marca;
    this.modelo = modelo;
    this.preco = preco;
  }

  getAno(ano) {
    return this.#ano;
  }

  setAno(ano) {
    this.#ano = ano;
  }
  
  adicionarEstoque() {
    this.#estoque++;
  }
  
  retirarDoEstoque() {
    this.#estoque--;
  }
  
  estoqueAtual() {
    return this.#estoque;
  }
}

class Notebook extends Produto {
  quantidadeRam;
}

class Televisao extends Produto {
  isSmart = false;
}

class Geladeira extends Produto {
  frostFree = false;
}

class MaquinaDeLavar extends Produto {
  capacidade;
}

var produtos = [];
while(confirm("Deseja cadastrar um notebook?")) {
  var marca = prompt("Digite a marca");
  var modelo = prompt("Digite o modelo");
  var preco = parseFloat(prompt("Digite o preco"));
  var quantidadeRam = prompt("Digite a quantidade de RAM");
  
  var produto = new Notebook(marca, modelo, preco);
  produto.quantidadeRam = 10;
  produto.adicionarEstoque();
  produtos.push(produto);
}

produtos.forEach((produto) => {
  var quantidade = produto.estoqueAtual();
  if (quantidade == 0) {
    alert("O produto " + produto.marca + " está sem estoque");
  }
});
````
