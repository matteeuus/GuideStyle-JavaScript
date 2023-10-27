# GuideStyle-JavaScript

## Sumário


1. [Referências](#Referências)
2. [Objetos](#Objetos)
3. [Arrays](#Arrays)
4. [Strings](#Strings)
5. [Functions](#Functions)
6. [Variaveis](#Variaveis)


## Tipos de variaveis primitivas

 <a name="types--primitives"></a><a name="1.1"></a>
  - [1.1](#types--primitives) Ao acessar um tipo primitivo você trabalha diretamente com o seu valor.

    - `string`
    - `number`
    - `boolean`
    - `null`
    - `undefined`
    - `symbol`
    - `bigint`

    <br/>

    <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex) Ao acessar um tipo complexo você trabalha diretamente com o seu valor.

    - `object`
    - `array`
    - `function`

    <br/>
    
      ## Referências

    <a name="references--prefer-const"></a><a name="2.1"></a>
  - [2.1](#references--prefer-const) Use `const` para todas as suas referências e evite usar `var`. [`prefer-const`](https://eslint.org/docs/rules/prefer-const), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign)

    > Isso evita possíveis bugs e não vai atrapalhar a compreensão do desenvolvedor e de terceiros

    ```javascript
    // Ruim
    var a = 1;
    var b = 2;

    // Bom
    const a = 1;
    const b = 2;
    ```
    
    <a name="references--disallow-var"></a><a name="2.2"></a>
  - [2.2](#references--disallow-var) Use  `const` para todas as suas referências e evite usar `var`. [`no-var`](https://eslint.org/docs/rules/no-var)

    ```javascript
    // Ruim
    var count = 1;
    if (true) {
      count += 1;
    }

    // Bom, agora usando o let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

    <a name="references--block-scope"></a><a name="2.3"></a>
  - [2.3](#references--block-scope) Veja que tanto o `let` quanto o `const` tem o escopo de bloco, enquanto o `var` tem seu escopo em sua função.

    ```javascript
    // const e let existem apenas nos blocos em que estão definidos.
    {
      let a = 1;
      const b = 1;
      var c = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    console.log(c); // Prints 1
    ```

    Você pode ver que a e b vão fazer um ReferenceError, enquanto c contém um número. Isso ocorre porque a e b tem um escopo de bloco, enquanto c tem um escopo de função.

    ## Objetos

  <a name="objects--no-new"></a><a name="3.1"></a>
  - [3.1](#objects--no-new) Use sintaxe para criação de objetos. [`no-new-object`](https://eslint.org/docs/rules/no-new-object)

    ```javascript
    // Ruim
    const item = new Object();

    // Boom
    const item = {};
    ```

    <a name="es6-object-shorthand"></a><a name="3.5"></a>
  - [3.2](#es6-object-shorthand) Use o método de objeto. [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand)

    ```javascript
    // Ruim
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // Boom
    const atom = {
      value: 1,

     <a name="objects--quoted-props"></a><a name="3.8"></a>
  - [3.3](#objects--quoted-props) Cite propiedades validas. [`quote-props`](https://eslint.org/docs/rules/quote-props)

    > Obiviamente usamos pela facilidade de leitura mas ele tambem melhora a forma de fazer a sintaxe.

    ```javascript
    // Ruim
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // Boom
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```
      addValue(value) {
        return atom.value + value;
      },
    };
    ```

    <a name="objects--prototype-builtins"></a>
  - [3.4](#objects--prototype-builtins) Não chame `Object.prototype` de forma literal, como `hasOwnProperty`, `propertyIsEnumerable`, e `isPrototypeOf`. [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

    > Métodos como esse podem ser ocultados pelas propriedades do objeto - `{ hasOwnProperty: false }` - ou o objeto pode ser um objeto nulo (`Object.create(null)`).`Object.prototype.hasOwnProperty.call`.

    ```javascript
    // Ruim
    console.log(object.hasOwnProperty(key));

    // Bom
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // Bem melhor
    const has = Object.prototype.hasOwnProperty;
    console.log(has.call(object, key));

    // Ótimo
    console.log(Object.hasOwn(object, key));

    /* Esse */
    import has from 'has';
    console.log(has(object, key));
    /* Ou esse */
    console.log(Object.hasOwn(object, key));
    ```

    <a name="objects--rest-spread"></a>
  - [3.5](#objects--rest-spread) Uma das melhores formas de usar uma sintaxe é usando objetos [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign). Use a sintaxe do rest para um novo objeto. [`prefer-object-spread`](https://eslint.org/docs/rules/prefer-object-spread)

    ```javascript
    // Muito ruim
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); 
    delete copy.a;

    // Ruim
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 });

    // Boom
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 };
    const { a, ...noA } = copy;
    ```

    ## Arrays

  <a name="arrays--literals"></a><a name="4.1"></a>
  - [4.1](#arrays--literals) Use a sintaxe para a criação de arrays. [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor)

    ```javascript
    // Ruim
    const items = new Array();

    // Boom
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  - [4.2](#arrays--push) Use [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) para adicionar itens a um array.

    ```javascript
    const someStack = [];

    // Ruim
    someStack[someStack.length] = 'alacazuba';

    // Bom
    someStack.push('alacazuba');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  - [4.3](#es6-array-spreads) Usando array spreads `...` podemos copiar arrays.

    ```javascript
    // Ruim
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // Bom
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a>
  <a name="arrays--from-iterable"></a><a name="4.4"></a>
  - [4.4](#arrays--from-iterable) Para converter um objeto para um array, use spreads `...` ao invés de [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

    ```javascript
    const foo = document.querySelectorAll('.foo');

    // Bom
    const nodes = Array.from(foo);

    // Muito bom
    const nodes = [...foo];
    ```

  <a name="arrays--from-array-like"></a>
  - [4.5](#arrays--from-array-like) Use [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) Para converter um objeto que tem uma semelhança a um arry para um array verdadeiro.

    ```javascript
    const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

    // Ruim
    const arr = Array.prototype.slice.call(arrLike);

    // Bom
    const arr = Array.from(arrLike);
    ```

  <a name="arrays--mapping"></a>
  - [4.6](#arrays--mapping) Use [`Array.from`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from) em vez de `...`, para evitar a criação de um array não desejado (intermediário).

    ```javascript
    // Ruim
    const baz = [...foo].map(bar);

    // Bom
    const baz = Array.from(foo, bar);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  - [4.7](#arrays--callback-return) Não tem problema em omitir um retorno se a função estiver em outro retorno. [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

    ```javascript
    // Boom
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // Bom
    [1, 2, 3].map((x) => x + 1);

    // Ruim
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
    });

    // Bom
    [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
      const flatten = acc.concat(item);
      return flatten;
    });

    // Bom
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // Bom
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

  <a name="arrays--bracket-newline"></a>
  - [4.8](#arrays--bracket-newline) Usando a quebra de linha depois de abrir colchets () do array e antes de abrir, se o array tiver múltiplas linhas.

    ```javascript
    // Ruim
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // Bom
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];
    ```
## Strings

  <a name="strings--quotes"></a><a name="6.1"></a>
  - [6.1](#strings--quotes) Use aspas  `''` para as strings. [`quotes`](https://eslint.org/docs/rules/quotes)

    ```javascript
    // Ruim
    const name = "Capt. Janeway";

    // Ruim
    const name = `Capt. Janeway`;

    // Bom
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  - [6.2](#strings--line-length) Strings podem fazer com que a linha passe de 100.

    > Strings quebradas são difíceis de tornar o código menos pesquisável.

    ```javascript
    // Ruim
    const errorMessage = 'Este é um erro muito longo que foi gerado por conta da \do Batman. Quando você para para pensar em como o Batman teve alguma coisa a ver \com isso você não chegaria a lugar nenhum \rápido.';

    // Ruim
    const errorMessage = 'Este é um erro muito longo que foi lançado porque ' +'do Batman. Quando você para para pensar em como o Batman teve alguma coisa a ver' +'com isso, você não chegaria a lugar nenhum rápido.';

    // Bom
    const errorMessage = 'Este é um erro super longo que foi lançado por causa do Batman. Quando você para para pensar em como o Batman teve algo a ver com isso, você não chegaria a lugar nenhum rapidamente.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  - [6.3](#es6-template-literals) Ao fazer uma strings, use strings de modelo. [`prefer-template`](https://eslint.org/docs/rules/prefer-template) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > As strings de modelo fazem com que uma sintaxe fique legível.

    ```javascript
    // Ruim
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // Ruim 
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // Ruim
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // Bom
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  - [6.4](#strings--eval) Nenca use `eval()` em uma string, isso abre muitas vulnerabilidades. [`no-eval`](https://eslint.org/docs/rules/no-eval)

  <a name="strings--escaping"></a>
  - [6.5](#strings--escaping) Não descarte de forma desnecessária os caracteres da string. [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

    > As barras invertidas prejudicam a legibilidadde.

    ```javascript
    // Ruim
    const foo = '\'this\' \i\s \"quoted\"';

    // Bom
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

    ## Functions

  <a name="functions--declarations"></a><a name="7.1"></a>
  - [7.1](#functions--declarations) Use expressoões de função nomeadas em vez de declaração. [`func-style`](https://eslint.org/docs/rules/func-style), [`func-names`](https://eslint.org/docs/latest/rules/func-names)

    ```javascript
    // Ruim
    function foo() {
      // ...
    }

    // Ruim
    const foo = function () {
      // ...
    };

    // Bom
    const short = function longUniqueMoreDescriptiveLexicalFoo() {
      // ...
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  - [7.2](#functions--iife) Colocando expressões em função gera um parênteses. [`wrap-iife`](https://eslint.org/docs/rules/wrap-iife)

    ```javascript
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  - [7.3](#functions--in-blocks) Não declare uma função em um bloco não funcional (`if`, `while`, etc). Ao inves disso, atribua a função a uma variável. [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  - [7.4](#functions--note-on-blocks) Defina `block` como uma lista.

    ```javascript
    // Ruim
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // Bom
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
  - [7.5](#functions--arguments-shadow) Não nomeie um parâmetro `arguments`, isso terá precedência sobre o `arguments` objeto forneciso a cada função.

    ```javascript
    // Ruim
    function foo(name, options, arguments) {
      // ...
    }

    // Bom
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  - [7.6](#es6-rest) Não use `arguments`, opte por usar syntax `...` [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

    >  `...`  é direto sobre quais argumentos serão usados

    ```javascript
    // Ruim
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // Bom
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  - [7.7](#es6-default-parameters) Use o padrão da sintaxe.

    ```javascript
    // Muito ruim
    function handleThings(opts) {
      opts = opts || {};
      // ...
    }

    // Ruim
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // Bom
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) É bom evitar efeitos em parâmetros padrão.

    > Dificultam o entendimento

    ```javascript
    let b = 1;
    // Ruim
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) É muito importante colocar os parâmetros com padrão por último. [`default-param-last`](https://eslint.org/docs/rules/default-param-last)

    ```javascript
    // Ruim
    function handleThings(opts = {}, name) {
      // ...
    }

    // Bom
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) Never use the Function constructor to create a new function. [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > Criar uma função desta forma a string se assemelha a `eval()`, que o deixa frágil.

    ```javascript
    // Ruim
    const add = new Function('a', 'b', 'return a + b');

    // Ruim
    const subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) Espaçamento em uma função. [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    ```javascript
    // Ruim
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // Bom
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) Não altere parâmetros. [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > A manipulação de objetos pode causar variáveis ​​indesejadas.

    ```javascript
    // Ruim
    function f1(obj) {
      obj.key = 1;
    }

    // Bom
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) Não reatribua parâmetros. [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > Reatribuir parâmetros pode levar a bugs se não for feita de maneira correta.

    ```javascript
    // Ruim
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // Bom
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) Prefira o uso da sintaxe spread `...` para chamar funções variadas. [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > Você não precisa de um contexto e não consegue compor algo novo com `new` e `apply`.

    ```javascript
    // Ruim
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // Bom
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // Ruim
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // Bom
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) Funções devem ser lidadas como qualquer outra lista multilinhas, com cada item em uma linha por si só, com uma vírgula final no último item. [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
    // Ruim
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // Bom
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // Ruim
    console.log(foo,
      bar,
      baz);

    // Bom
    console.log(
      foo,
      bar,
      baz,
    );
    ```

    ## Variaveis

  <a name="variables--const"></a><a name="13.1"></a>
  - [13.1](#variables--const) Sempre use `const` ou `let` para declarar variáveis. [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

    ```javascript
    // Ruim
    superPower = new SuperPower();

    // Bom
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  - [13.2](#variables--one-const) Use `const` ou `let` como uma declaração por variável ou atribuição. [`one-var`](https://eslint.org/docs/rules/one-var)

    >  É mais fácil adicionar novas declarações de variáveis ​​dessa maneira e você nunca precisa se preocupar em trocar um `;` para `,`.
    ```javascript
    // Ruim
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // Ruim
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // Bom
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  - [13.3](#variables--const-let-group) Agrupe as `const` e suas `let`.

    > Isso é útil quando mais tarde você precisar atribuir uma variável dependendo de uma das variáveis ​​atribuídas anteriormente.

    ```javascript
    // Ruim
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // Ruim
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // Bom
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  - [13.4](#variables--define-where-used) Atribua variáveis ​​onde você precisar delas, contanto que elas estejam em um local razoável.

    > `let` e `const` têm escopo de bloco e não de função..

    ```javascript
    // Ruim
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // Bom
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```

  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  - [13.5](#variables--no-chain-assignment) Cuitado ao atribir algo a variaveis. [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)


    ```javascript
    // Ruim
    (function example() {
      let a = b = c = 1;
    }());

    console.log(a); //
    console.log(b); // 1
    console.log(c); // 1

    // Bom
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a);
    console.log(b);
    console.log(c);
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  - [13.6](#variables--unary-increment-decrement) Atribuições de variáveis ​​cria variáveis ​​globais implícitas. (`++`, `--`). [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)

    ```javascript
    // Ruim

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // Bom

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

<a name="variables--linebreak"></a>
  - [13.7](#variables--linebreak) Evite quebras de linha antes ou depois de `=` em uma tarefa. Se sua atribuição violar [`max-len`](https://eslint.org/docs/rules/max-len), coloque o valor entre parênteses. [`operator-linebreak`](https://eslint.org/docs/rules/operator-linebreak).

    > Quebras de linha ao redor de `=` podem gerar um bug e não mostrar o valor de uma atribuição.

    ```javascript
    // Ruim
    const foo =
      superLongLongLongLongLongLongLongLongFunctionName();

    // Ruim
    const foo
      = 'superLongLongLongLongLongLongLongLongString';

    // Bom
    const foo = (
      superLongLongLongLongLongLongLongLongFunctionName()
    );

    // Bom
    const foo = 'superLongLongLongLongLongLongLongLongString';
    ```

<a name="variables--no-unused-vars"></a>
  - [13.8](#variables--no-unused-vars) Cuidado com variáveis ​​não utilizadas. [`no-unused-vars`](https://eslint.org/docs/rules/no-unused-vars)

    > Variáveis ​​que são declaradas e não usadas em nenhum lugar do código um erro devido à refatoração. Essas variáveis ​​ocupam espaço no código e podem confundir.

    ```javascript
    // Ruim

    const some_unused_var = 42;

    let y = 10;
    y = 5;

    let z = 0;
    z = z + 1;

    function getX(x, y) {
        return x;
    }

    // Bom

    function getXPlusY(x, y) {
      return x + y;
    }

    const x = 1;
    const y = a + 2;

    alert(getXPlusY(x, y));

    const { type, ...coords } = data;
    ```

**[⬆ back to top](#table-of-contents)**
