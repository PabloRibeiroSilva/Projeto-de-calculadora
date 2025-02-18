<html>

<head>
    <title>
        Imersão Dev - Aula 02
    </title>
</head>

<body>
    <div class="container">
        <h1 class="page-title">
            Calculadora
        </h1>
        <img src="https://www.alura.com.br/assets/img/imersoes/dev-2021/logo-imersao-calculadora.svg" class="page-logo"
            alt="">
    <a href="https://alura.com.br/" target="_blank">
        <img src="https://www.alura.com.br/assets/img/home/alura-logo.svg" alt="" class="alura-logo">
    </a>
      
      <div class="espaçamento"></div>
      
  <div class="calculadora">
  <div class="tela" id="tela"></div>
  <div class="botoes">
    <div class="contas">
      <div>&divide;</div>
      <div>&times;</div>
      <div>-</div>
      <div>+</div>
    </div>
    <div class="painel-numeros">
      <div class="numeros">
        <div>7</div>
        <div>8</div>
        <div>9</div>
      </div>
      <div class="numeros">
        <div>4</div>
        <div>5</div>
        <div>6</div>
      </div>
      <div class="numeros">
        <div>1</div>
        <div>2</div>
        <div>3</div>
      </div>
      <div class="numeros">
        <div>0</div>
        <div>.</div>
        <div id="limpar">C</div>
      </div>
    </div>
    <div class="igual" id="resultado">=</div>
  </div>
</div>
</div>
  
</body>

</html>

var input = document.getElementById('tela'),
  numero = document.querySelectorAll('.numeros div'),
  conta = document.querySelectorAll('.contas div'),
  resultado = document.getElementById('resultado'),
  limpar = document.getElementById('limpar'),
  resultadoEstaMostrado = false;

// adiconando evento de clique nos botões dos numeros
for (var i = 0; i < numero.length; i++) {
  numero[i].addEventListener("click", function(e) {

    // variaveis do texto na tela e o ultimo caractere 
    var textoNaTela = input.innerHTML;
    var ultimoChar = textoNaTela[textoNaTela.length - 1];

    // se o resultado ainda não foi mostrado continua adicionando
    if (resultadoEstaMostrado === false) {
      input.innerHTML += e.target.innerHTML;
    } else if (resultadoEstaMostrado === true && ultimoChar === "+" || ultimoChar === "-" || ultimoChar === "×" || ultimoChar === "÷") {
      // se o resultado ja foi mostrado e o usuario aperta um botão de conta continuam adicionando na tela para a próxima operação
      resultadoEstaMostrado = false;
      input.innerHTML += e.target.innerHTML;
    } else {
      //se o resultado ja foi mostrado e o usuario apertar um numero limpa a tela e começa uma nova operação
      resultadoEstaMostrado = false;
      input.innerHTML = "";
      input.innerHTML += e.target.innerHTML;
    }

  });
}

// adiconando evento de clique nos botões das contas
for (var i = 0; i < conta.length; i++) {
  conta[i].addEventListener("click", function(e) {

    // variaveis do texto na tela e o ultimo caractere 
    var textoNaTela = input.innerHTML;
    var ultimoChar = textoNaTela[textoNaTela.length - 1];

    // se o ultimo caractere mostrado for uma conta, substitui pela que foi clicada
    if (ultimoChar === "+" || ultimoChar === "-" || ultimoChar === "×" || ultimoChar === "÷") {
      var newString = textoNaTela.substring(0, textoNaTela.length - 1) + e.target.innerHTML;
      input.innerHTML = newString;
    } else if (textoNaTela.length == 0) {
      //se a primeira tecla pressionada for uma conta, avisa o usuario para colocar um numero primeiro
      alert("coloque um numero primeiro");
    } else {
      //senão apenas adiciona a conta pressionada na tela
      input.innerHTML += e.target.innerHTML;
    }

  });
}

// adiconando evento de clique no botão igual
resultado.addEventListener("click", function() {

  // texto que será processado
  var inputString = input.innerHTML;

  // fazendo uma lista dos numeros que serão processados
  var numeros = inputString.split(/\+|\-|\×|\÷/g);

  // fazendo uma lista das contas que serão processadas
  var contas = inputString.replace(/[0-9]|\./g, "").split("");

  // fazendo as contas uma de cada vez em ordem, primeiro divisão depois multiplicação, subtração e adição
  var divide = contas.indexOf("÷");
  while (divide != -1) {
    numeros.splice(divide, 2, numeros[divide] / numeros[divide + 1]);
    contas.splice(divide, 1);
    divide = contas.indexOf("÷");
  }

  var multiply = contas.indexOf("×");
  while (multiply != -1) {
    numeros.splice(multiply, 2, numeros[multiply] * numeros[multiply + 1]);
    contas.splice(multiply, 1);
    multiply = contas.indexOf("×");
  }

  var subtract = contas.indexOf("-");
  while (subtract != -1) {
    numeros.splice(subtract, 2, numeros[subtract] - numeros[subtract + 1]);
    contas.splice(subtract, 1);
    subtract = contas.indexOf("-");
  }

  var add = contas.indexOf("+");
  while (add != -1) {
    numeros.splice(add, 2, parseFloat(numeros[add]) + parseFloat(numeros[add + 1]));
    contas.splice(add, 1);
    add = contas.indexOf("+");
  }

  input.innerHTML = numeros[0]; // mostrando resultado na tela

  resultadoEstaMostrado = true; // dizendo que o resultado está sendo mostrado
});

// adiconando evento de clique no botão limpar
limpar.addEventListener("click", function() {
  input.innerHTML = "";
})

var input = document.getElementById('tela'),
  numero = document.querySelectorAll('.numeros div'),
  conta = document.querySelectorAll('.contas div'),
  resultado = document.getElementById('resultado'),
  limpar = document.getElementById('limpar'),
  resultadoEstaMostrado = false;

// adiconando evento de clique nos botões dos numeros
for (var i = 0; i < numero.length; i++) {
  numero[i].addEventListener("click", function(e) {

    // variaveis do texto na tela e o ultimo caractere 
    var textoNaTela = input.innerHTML;
    var ultimoChar = textoNaTela[textoNaTela.length - 1];

    // se o resultado ainda não foi mostrado continua adicionando
    if (resultadoEstaMostrado === false) {
      input.innerHTML += e.target.innerHTML;
    } else if (resultadoEstaMostrado === true && ultimoChar === "+" || ultimoChar === "-" || ultimoChar === "×" || ultimoChar === "÷") {
      // se o resultado ja foi mostrado e o usuario aperta um botão de conta continuam adicionando na tela para a próxima operação
      resultadoEstaMostrado = false;
      input.innerHTML += e.target.innerHTML;
    } else {
      //se o resultado ja foi mostrado e o usuario apertar um numero limpa a tela e começa uma nova operação
      resultadoEstaMostrado = false;
      input.innerHTML = "";
      input.innerHTML += e.target.innerHTML;
    }

  });
}

// adiconando evento de clique nos botões das contas
for (var i = 0; i < conta.length; i++) {
  conta[i].addEventListener("click", function(e) {

    // variaveis do texto na tela e o ultimo caractere 
    var textoNaTela = input.innerHTML;
    var ultimoChar = textoNaTela[textoNaTela.length - 1];

    // se o ultimo caractere mostrado for uma conta, substitui pela que foi clicada
    if (ultimoChar === "+" || ultimoChar === "-" || ultimoChar === "×" || ultimoChar === "÷") {
      var newString = textoNaTela.substring(0, textoNaTela.length - 1) + e.target.innerHTML;
      input.innerHTML = newString;
    } else if (textoNaTela.length == 0) {
      //se a primeira tecla pressionada for uma conta, avisa o usuario para colocar um numero primeiro
      alert("coloque um numero primeiro");
    } else {
      //senão apenas adiciona a conta pressionada na tela
      input.innerHTML += e.target.innerHTML;
    }

  });
}

// adiconando evento de clique no botão igual
resultado.addEventListener("click", function() {

  // texto que será processado
  var inputString = input.innerHTML;

  // fazendo uma lista dos numeros que serão processados
  var numeros = inputString.split(/\+|\-|\×|\÷/g);

  // fazendo uma lista das contas que serão processadas
  var contas = inputString.replace(/[0-9]|\./g, "").split("");

  // fazendo as contas uma de cada vez em ordem, primeiro divisão depois multiplicação, subtração e adição
  var divide = contas.indexOf("÷");
  while (divide != -1) {
    numeros.splice(divide, 2, numeros[divide] / numeros[divide + 1]);
    contas.splice(divide, 1);
    divide = contas.indexOf("÷");
  }

  var multiply = contas.indexOf("×");
  while (multiply != -1) {
    numeros.splice(multiply, 2, numeros[multiply] * numeros[multiply + 1]);
    contas.splice(multiply, 1);
    multiply = contas.indexOf("×");
  }

  var subtract = contas.indexOf("-");
  while (subtract != -1) {
    numeros.splice(subtract, 2, numeros[subtract] - numeros[subtract + 1]);
    contas.splice(subtract, 1);
    subtract = contas.indexOf("-");
  }

  var add = contas.indexOf("+");
  while (add != -1) {
    numeros.splice(add, 2, parseFloat(numeros[add]) + parseFloat(numeros[add + 1]));
    contas.splice(add, 1);
    add = contas.indexOf("+");
  }

  input.innerHTML = numeros[0]; // mostrando resultado na tela

  resultadoEstaMostrado = true; // dizendo que o resultado está sendo mostrado
});

// adiconando evento de clique no botão limpar
limpar.addEventListener("click", function() {
  input.innerHTML = "";
})
