- [Como a web funciona?](#como-a-web-funciona)
  - [Visão cliente e servidor](#visão-cliente-e-servidor)
- [HTML](#html)
  - [Mãos na massa](#mãos-na-massa)
    - [Utilizando HTML5](#utilizando-html5)
- [CSS](#css)
  - [Sintaxe](#sintaxe)
  - [Incluindo CSS na página](#incluindo-css-na-página)
    - [Inline](#inline)
    - [Interno](#interno)
    - [Externo](#externo)
    - [Seletores](#seletores)
      - [Classes](#classes)
      - [IDs](#ids)
  - [Propriedades Mais Utilizadas](#propriedades-mais-utilizadas)
    - [Tamanhos e Espaçamentos](#tamanhos-e-espaçamentos)
    - [Backgrounds](#backgrounds)
    - [Tipografia](#tipografia)
    - [Display](#display)
  - [Saiba Mais](#saiba-mais)
- [JavaScript](#javascript)
  - [Inserindo JS na página](#inserindo-js-na-página)
    - [Inserindo códigos na própria página (inline)](#inserindo-códigos-na-própria-página-inline)
    - [Relacionando um arquivo externo na página](#relacionando-um-arquivo-externo-na-página)
- [Trabalhando com HTML, CSS e JavaScript](#trabalhando-com-html-css-e-javascript)
- [Bootstrap](#bootstrap)
  - [Componentes mais comuns](#componentes-mais-comuns)
    - [alert](#alert)
    - [badges](#badges)
    - [buttons](#buttons)
    - [cards](#cards)
    - [carousel](#carousel)
    - [collapse](#collapse)
    - [forms](#forms)
    - [input-group](#input-group)
    - [modal](#modal)
    - [tooltips](#tooltips)
  - [Entendendo os Grids](#entendendo-os-grids)
- [jQuery](#jquery)
  - [Iniciarlizar o jQuery](#iniciarlizar-o-jquery)
  - [Eventos](#eventos)
  - [Eventos com Ações](#eventos-com-ações)
    - [Esconder um elemento](#esconder-um-elemento)
    - [Exibir um elemento](#exibir-um-elemento)
    - [Adicionar classe ao elemento](#adicionar-classe-ao-elemento)
  - [Lista de métodos e eventos do jQuery](#lista-de-métodos-e-eventos-do-jquery)
  - [Utilizando o Ajax do jQuery](#utilizando-o-ajax-do-jquery)

# Como a web funciona?
Como a Web funciona oferece uma visão simplificada do que acontece quando você vê uma página em um navegador, no seu computador ou telefone.

## Visão cliente e servidor
Computadores conectados à web são chamados clientes e servidores. 
* **Clientes** são os típicos dispositivos conectados à internet dos usuários da web (por exemplo, seu computador conectado ao seu Wi-Fi ou seu telefone conectado à sua rede móvel) e programas de acesso à Web disponíveis nesses dispositivos (geralmente um navegador como Firefox ou Chrome).
* **Servidores** são computadores que armazenam páginas, sites ou aplicativos. Quando o dispositivo de um cliente quer acessar uma página, uma cópia dela é baixada do servidor para a máquina do cliente para ser apresentada no navegador web do usuário.

Ao acessar um site, você, o cliente, está acessando um servidor que responde a requisição normalmente com uma página em HTML, que pode ter CSS e JavaScript dentro dela.

# HTML
HTML significa Hypertext Markup Language. Ele permite que os usuários criem e estruturem seções, parágrafos, cabeçalhos e links para páginas da internet ou aplicações.

O HTML não é uma linguagem de programação, isso significa que não pode ser usado para criar funcionalidades dinâmicas. Entretanto, o HTML possibilita a organização e formatação de documentos, similar ao Microsoft Word.

Ao trabalhar com HTML simplesmente codificamos estruturas (tags e atributos) para marcar a página de um site. Por exemplo, podemos criar um parágrafo colocando o texto entre as tags ``<p>`` e ``</p>``.

````html
<p>Assim você cria um parágrafo com HTML.</p>
<p>Você pode criar vários!</p>
````

Documentos HTML são arquivos com as extensões .html ou .htm. Eles podem ser visualizados com qualquer navegador (como Google Chrome, Safari, ou Mozilla Firefox). O navegador faz a leitura do arquivo e renderiza seu conteúdo para visualização dos usuários.

A maioria dos elementos HTML utilizam as sintaxe de abertura e fechamento como ``<tag>`` e ``</tag>``.

Abaixo temos um exemplo de como os elementos HTML podem ser estruturados:

````html
<div>
    <h1>Cabeçalho principal</h1>
    <h2>Subtítulo de impacto</h2>
    <p>Parágrafo um</p>
    <img src="/" alt="Image">
    <p>Parágrafo dois com <a href="https://example.com">hyperlink</a></p>
</div>
````

O elemento superior é uma divisão (``<div></div>``) que pode ser utilizada para marcar seções de conteúdo maiores.
Contém um cabeçalho (``<h1></h1>``), subtítulo (``<h2></h2>``), dois parágrafos (``<p></p>``), e uma imagem (``<img>``).
O segundo parágrafo inclui um link (``<a></a>``) com um atributo href que contém a URL de destino.
A tag de imagem também possui dois atributos: src para o caminho da imagem e alt para a descrição da imagem.

## Mãos na massa

Vamos criar um projeto novo e então criar um arquivo HTML dentro desse projeto. A partir daí editaremos este arquivo utilizando o VSCode.

````sh
cd ~/Projetos
############# Entrando na pasta dos projetos

mkdir AulaHtml
############# Criando uma pasta chamada AulaHtml

cd AulaHtml
############# Entrando na pasta recém criada

code .
############# Abrindo o VSCode exatamente na pasta recém criada
````

Dentro do VSCode crie um arquivo chamado ``index.html`` e coloque o conteúdo abaixo dentro dele.

````html
<html>
    <h1>Este é meu primeiro HTML</h1>
</html>
````

Veja [neste site](https://www.w3schools.com/html/) vários exemplos de tags que você pode utilizar no HTML. 

### Utilizando HTML5
Para utilizar HTML5 basta inicializarmos nosso HTML seguindo o seguinte padrão:
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
    
</body>
</html>
````

Para que você não precise sempre decorar como inicializar o HTML, você pode utilizar o [Emmet](https://code.visualstudio.com/docs/editor/emmet). O Emmet já está disponíel no VSCode por padrão. Para utilizá-lo você deve fazer o [snippet](http://www.linhadecodigo.com.br/artigo/1940/snippets-o-que-sao-como-e-quando-utiliza-los.aspx) ``html:5`` e apertar o tab. Então o Emmet irá criar o esqueleto para você. 

# CSS

O Cascading Style Sheets (CSS) é uma linguagem utilizada para definir a apresentação (aparência) de documentos que adotam para o seu desenvolvimento linguagens de marcação (como XML, HTML e XHTML e etc..). O CSS define como serão exibidos os elementos contidos no código de um documento e sua maior vantagem é efetuar a separação entre o formato e o conteúdo de um documento.

## Sintaxe

Para escrever código CSS é necessário seguir uma regra. A regra é uma declaração que possui uma sintaxe própria bem simples que define a forma com que o estilo será aplicado aos nossos elementos HTML. Você pode ver a regra a seguir:

````css
seletor {
  propriedade: valor;
}
````

Exemplo

````css
body {
  background-color: #000;
}
````

## Incluindo CSS na página

Existem três formas para incluir o código CSS em seu projeto

### Inline

A primeira forma de aplicar CSS a uma página é utilizando o atributo style em elementos do HTML:

````html
<p style="color: blue">
  Parágrafo com fonte azul.
</p>

<p>
  Esse outro parágrafo não é azul, a não ser que exista <span style="color: red">CSS em outro lugar</span>.
</p>
````

### Interno

A segunda forma é utilizar a tag style dentro do head da página HTML:

````html
<head>
  <style type="text/css">
    seletor { 
      propriedade: valor; 
    }
  </style>
</head>
````

### Externo

E a última - porém a mais utilizada - maneira de aplicar CSS é criar um ou mais arquivos com extensão .css e incluí-los na estrutura head do HTML:

````html
<head>
  <link rel="stylesheet" type="text/css" href="/style.css">
</head>
````

### Seletores

Em HTML e CSS, há a possibilidade de aplicar estilos através de 'class' e 'id'. 

#### Classes
As classes são uma forma de identificar um grupo de elementos. Através delas, pode-se atribuir formatação a VÁRIOS elementos de uma vez. Exemplo:

````css
.classe1 {
  background-color: blue;
}
````

````html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <title></title>
    <meta charset="utf-8">
  </head>
  <body>
    <div class="classe1">Div1</div>
    <div class="classe1">Div2</div>
    <div class="classe1">Div3</div>
    <div class="">Div4</div>
    <div class="">Div5</div>
  </body>
</html>
````

#### IDs
As ids são uma forma de identificar um elemento, e devem ser ÚNICAS para cada elemento. É como se fossem impressões digitais de nossos dedos ou RGs. Através delas, pode-se atribuir formatação a um elemento em especial. Exemplo:

````css
#idUm {
  background: blue;
}
#idDois {
  background: yellow;
}
````

````html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <title></title>
    <meta charset="utf-8">
  </head>
  <body>
    <div id="idUm">Div1</div>
    <div id="idDois">Div2</div>
    <div id="">Div3</div>
    <div id="">Div4</div>
  </body>
</html>
````

## Propriedades Mais Utilizadas

### Tamanhos e Espaçamentos
````css
.classe {
    width: 50px; /* Largura */
    height: 50px; /* Altura */
    border: 1px solid gray; /* Borda */
    padding: 10px; /* Espaçamento interno */
    margin: 15px; /* Espaçamento externo */
}
````

### Backgrounds
````css
div {
  background-color: gray; /* Background como cor */
  background-image: url("/img/bg.png"); /* Background como imagem */
}
````

### Tipografia
````css
div {
  font-family: "Times New Roman", Times, serif; /* Mudar a fonte */
  font-size: 14px; /* Tamanho da fonte */
  font-weight: bold; /* Fonte negrita */
  text-decoration: underline; /* Fonte subilinhada */
  font-style: italic; /* Fonte itálica */
  text-align: center; /* Centralizar texto */
}
````

### Display
````css
div {
  display: block; /* Blocos */
  display: inline-block; /* Blocos em linha */
  display: none; /* Não exibir */
}
````

## Saiba Mais
Saiba mais sobre CSS [neste site](https://tableless.github.io/iniciantes/manual/css/index.html), como seletores complexos, outras propriedades e etc.

# JavaScript

JavaScript, neste contexto, é uma linguagem de programação client-side. Ela é utilizada para controlar o HTML e o CSS para manipular comportamentos na página. Existem três camadas básicas no desenvolvimento para Web: a informação que fica com o HTML, a formatação, que fica com o CSS e o comportamento, que fica com o JavaScript.

````html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <title>Título</title>
    <meta charset="utf-8">
  </head>
  <body>
 
    <!-- Ter o costume de colocar código JavaScript no final do body -->
    <script type="text/javascript">
      alert('Hello World!');
    </script>
  </body>
</html>
````

## Inserindo JS na página

Para adicionar códigos JavaScript à uma página devemos usar a tag ``<script>``, podendo fazer essa inserção de duas formas:

###  Inserindo códigos na própria página (inline)

````html

<script type="text/javascript">
  alert('Olá mundo!');
</script>

````

### Relacionando um arquivo externo na página

````html
<script type="text/javascript" src="/js/app.js"></script>
<script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
</script>
````

# Trabalhando com HTML, CSS e JavaScript

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
       #label-anoNascimento {
        display: block;
        font-weight: bold;
        font-family: sans-serif;
        margin: 10px 0px 5px;
       } 

       #anoNascimento {
        width: 200px;
        border: 1px solid #aaa;
        padding: 5px 1px;
        border-radius: 5px;
       }

       #botao {
        padding: 5px 15px;
        margin-left: 10px;
        background-color: antiquewhite;
        border: 1px solid #988872;
        border-radius: 5px;
       }

       #botao:hover {
        background-color: rgb(196, 173, 143);   
       }
    </style>
</head>
<body>

    <label id="label-anoNascimento">Digite o ano do seu nascimento:</label>
    <input type="text" id="anoNascimento">

    <button id="botao" onclick="calcularIdade()">Calcular Idade</button>
    

    <script>
        function calcularIdade() {
            var anoNascimento = document.querySelector("#anoNascimento").value;
            var idade = 2021 - anoNascimento;
            alert("Você tem " + idade + " anos");
        }
    </script>
</body>
</html>
````

# Bootstrap

Bootstrap é um framework web com código-fonte aberto para desenvolvimento de componentes de interface e front-end para sites e aplicações web usando HTML, CSS e JavaScript, baseado em modelos de design para a tipografia, melhorando a experiência do usuário em um site amigável e responsivo.

Visite a [documentação oficial](https://getbootstrap.com/docs/4.6/getting-started/introduction/).

Neste curso, nesse momento, utilizeramos o CDN do Bootstrap para sua utilização. Utilizaremos também o Bootstrap 4, visto que este usa jQuery e o jQuery nos será util para aprendizado. 

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" crossorigin="anonymous">
</head>
<body>
    <h1>Meu Primeiro Bootstrap</h1>
    
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js" crossorigin="anonymous"></script>
</body>
</html>
````

## Componentes mais comuns
### alert
````html
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Sucesso!</strong> Seu usuário foi cadastrado com sucesso!
  <button type="button" class="close" data-dismiss="alert" aria-label="Close">
    <span aria-hidden="true">&times;</span>
  </button>
</div>
````

### badges
````html
<span class="badge badge-success">New</span>
````

### buttons
````html
<button type="button" class="btn btn-primary">Salvar</button>
````

### cards
````html
<div class="card">
  <h5 class="card-header">Cabeçalho do Cartão</h5>
  <div class="card-body">
    <h5 class="card-title">Título</h5>
    <p class="card-text">Texto do meu cartão</p>
    <a href="#" class="btn btn-primary">Salvar</a>
  </div>
</div>
````

### carousel 
````html
<div id="carouselExampleSlidesOnly" class="carousel slide" data-ride="carousel">
  <div class="carousel-inner">
    <div class="carousel-item active">
        <img src="https://via.placeholder.com/800x500" class="d-block w-100" alt="...">
    </div>
    <div class="carousel-item">
      <img src="https://via.placeholder.com/800x500" class="d-block w-100" alt="...">
    </div>
    <div class="carousel-item">
      <img src="https://via.placeholder.com/800x500" class="d-block w-100" alt="...">
    </div>
  </div>
</div>
````

### collapse
````html
<p>
  <a class="btn btn-primary" data-toggle="collapse" href="#collapseExample" role="button" aria-expanded="false" aria-controls="collapseExample">
    Abrir 1
  </a>
  <button class="btn btn-primary" type="button" data-toggle="collapse" data-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
    Abrir 2
  </button>
</p>
<div class="collapse" id="collapseExample">
  <div class="card card-body">
    Texto escondido
  </div>
</div>
````

### forms
````html
<form>
  <div class="form-group">
    <label for="exampleInputEmail1">Email</label>
    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
    <small id="emailHelp" class="form-text text-muted">Mensagem de ajuda para o campo email.</small>
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">Senha</label>
    <input type="password" class="form-control" id="exampleInputPassword1">
  </div>
  <div class="form-group form-check">
    <input type="checkbox" class="form-check-input" id="exampleCheck1">
    <label class="form-check-label" for="exampleCheck1">Salvar</label>
  </div>
  <button type="submit" class="btn btn-primary">Entrar</button>
</form>
````

### input-group
````html
<div class="input-group mb-3">
  <div class="input-group-prepend">
    <span class="input-group-text" id="basic-addon1">@</span>
  </div>
  <input type="text" class="form-control" placeholder="Username" aria-label="Usuário" aria-describedby="basic-addon1">
</div>
````

### modal
````html
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
  Abrir Modal
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Título do Modal</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        Corpo do Modal
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Fechar</button>
        <button type="button" class="btn btn-primary">Salvar</button>
      </div>
    </div>
  </div>
</div>
````

### tooltips
````html
<button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="top" title="Tooltip on top">
  Informação extra em cima
</button>

<script>
$(function () {
  $('[data-toggle="tooltip"]').tooltip()
})
</script>
````

## Entendendo os Grids
O Bootstrap possui um sistema de grids que permitem fácil responsividade dos seus componentes. 

Por exemplo, abaixo um código que disponibiliza três colunas, mas se acessadas pelo celular aparece apenas uma.

````html
<div class="container">
  <div class="row">
    <div class="col-md-4">
      Primeira coluna de três
    </div>
    <div class="col-md-4">
      Segunda coluna de três
    </div>
    <div class="col-md-4">
      Terceira coluna de três
    </div>
  </div>
</div>
````

Para entendermos o sistema de grids do Bootstrap, precisamos entender que o Bootstrap divide seus grids em 12 colunas. Portanto uma coluna de tamanho 4, como a que usamos no exemplo acima ``col-md-4`` ocupará sempre 1/3 do container. Assim como uma coluna tamanho 6 ``col-md-6`` ocupará sempre 1/2 do container. O ``md``no meio da classe indica qual tamanho de tela corresponde aos tamanho da coluna. Abaixo uma tabela explicativa:

Tamanho | Extra Pequeno < 576px  | Pequeno >= 576px | Médio >= 768px | Grande >= 992px | Extra Grande >= 1200px
----- | ------ | ----- | ----- | ----- | ----- 
Max container width | Nenhum (auto) | 540px | 720px | 960px | 1140px 
Class prefix | ``.col-``| ``.col-sm-`` | ``.col-md-`` | ``.col-lg-`` | ``.col-xl-``



- **Número de Colunas:** 12
- **Tamanho do Gutter:** 30px (15px de cada lado)
- **Aninhado?** Sim
- **Ordenação de Colunas?** Sim

Para mais informações sobre o sistema de grids, visite o [site oficial](https://getbootstrap.com/docs/4.6/layout/grid/). 

# jQuery

O jQuery disponiliza uma forma prática, porém ultrapassada, de nós manipularmos o DOM do HTML que está sendo interpretado pelo nosso navegador. O jQuery vem sendo cada vez menos utilizado, porém, [pesquisas recentes](https://trends.builtwith.com/javascript/jQuery) mostram que ele ainda domina [boa parte](https://trends.google.com.br/trends/explore?geo=BR&q=jquery,%2Fg%2F11c0vmgx5d,%2Fm%2F012l1vxv,%2Fg%2F11c6w0ddw9) das pesquisas relacionadas a desenvolvimento Web. Portanto, em nosso curso, ainda faremos uso dele. 

## Iniciarlizar o jQuery
Para utilizar o jQuery você poderá baixá-lo ou utilizar um CDN. Coloque o seguinte código logo antes do fechamento da tag body do seu HTML

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
      
      <script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
  </body>
</html>
````

Agora poderemos fazer uso do jQuery. Para utilizar o jQuery você pode usar o objeto ``jQuery`` ou, melhor, simplesmente um ``$``. Como o jQuery é um manipulador do DOM, é uma boa prática fazer uso do jQuery apenas quando toda a página for carregada, ou seja, quando ela estiver ``pronta`` (``ready``). Faça o seguinte código e teste:

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
      
      <script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>

      <script>
        $(document).ready(function() {
          alert("jQuery funcionou");
        });
      </script>
  </body>
</html>
````

## Eventos

Para adicionar eventos no JavaScript com jQuery é fácil, basta seguir a sintaxe a seguir:

````html
<button id="exibirAlerta">Clique aqui para exibir o alerta</button>

<script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
<script>
  $(document).ready(function() {
    $("#exibirAlerta").click(function() {
      alert("Você clicou no botão exibir alerta");
    });
  });
</script>
````

## Eventos com Ações

### Esconder um elemento
````html
<button id="sumirParagrafo">Clique aqui para sumir com o parágrafo</button>
<p id="paragrafo">Este parágrafo tem que sumir ao clicar no botão acima.</p>

<script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
<script>
  $(document).ready(function() {
    $("#sumirParagrafo").click(function() {
      $("#paragrafo").hide();
    });
  });
</script>
````

### Exibir um elemento
````html
<button id="aparecerParagrafo">Clique aqui para aparecer o parágrafo</button>
<p id="paragrafo" style="display: none">Este parágrafo tem que aparecer ao clicar no botão acima.</p>

<script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
<script>
  $(document).ready(function() {
    $("#aparecerParagrafo").click(function() {
      $("#paragrafo").show();
    });
  });
</script>
````

### Adicionar classe ao elemento
````html
<style>
  .vermelho {
    color: #ff0000;
  }
</style>

<button id="mudarACor">Clique aqui para mudar a cor do parágrafo</button>
<p id="paragrafo">Este parágrafo tem que mudar a cor para vermelho.</p>

<script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
<script>
  $(document).ready(function() {
    $("#mudarACor").click(function() {
      $("#paragrafo").addClass("vermelho");
    });
  });
</script>
````

## Lista de métodos e eventos do jQuery

- [Eventos](https://www.w3bai.com/pt/jquery/jquery_ref_events.html)
- [Efeitos](https://www.w3bai.com/pt/jquery/jquery_ref_effects.html)
- [Alterações no HTML e no CSS](https://www.w3bai.com/pt/jquery/jquery_ref_html.html)


## Utilizando o Ajax do jQuery

AJAX significa Asynchronous JavaScript and XML, ou JavaScript e XML Assíncronos, em bom português. Ele é um conjunto de técnicas de desenvolvimento voltado para a web que permite que aplicações trabalhem de modo assíncrono, processando qualquer requisição ao servidor em segundo plano.

Qualquer aplicação que use AJAX pode enviar e receber dados do servidor sem precisar recarregar a página inteira.

Exemplo:
````html
<html>
  <script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
  <script>
    $(document).ready(function() {
      var cep = "69099280";

      $.getJSON("https://viacep.com.br/ws/"+ cep +"/json/", function(dados) {
        console.log(dados);
        // console.log(dados.logradouro);
      });
    });
  </script>
</html>
````
