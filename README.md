# GuideStyle-JavaScript

## Sumário


1. [a](#a)
2. [a](#a)
3. [a](#a)


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
  - [3.4](#objects--prototype-builtins) Não chame `Object.prototype` de forma literal, como `hasOwnProperty`, `propertyIsEnumerable`, e `isPrototypeOf`. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

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
    const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
    delete copy.a;

    // Ruim
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // Boom
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
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

    > Why? Function declarations are hoisted, which means that it’s easy - too easy - to reference the function before it is defined in the file. This harms readability and maintainability. If you find that a function’s definition is large or complex enough that it is interfering with understanding the rest of the file, then perhaps it’s time to extract it to its own module! Don’t forget to explicitly name the expression, regardless of whether or not the name is inferred from the containing variable (which is often the case in modern browsers or when using compilers such as Babel). This eliminates any assumptions made about the Error’s call stack. ([Discussion](https://github.com/airbnb/javascript/issues/794))

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
  - [7.7](#es6-default-parameters) Use default parameter syntax rather than mutating function arguments.

    ```javascript
    // really bad
    function handleThings(opts) {
      // No! We shouldn’t mutate function arguments.
      // Double bad: if opts is falsy it'll be set to an object which may
      // be what you want but it can introduce subtle bugs.
      opts = opts || {};
      // ...
    }

    // still bad
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // good
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  - [7.8](#functions--default-side-effects) Avoid side effects with default parameters.

    > Why? They are confusing to reason about.

    ```javascript
    let b = 1;
    // bad
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  - [7.9](#functions--defaults-last) Always put default parameters last. eslint: [`default-param-last`](https://eslint.org/docs/rules/default-param-last)

    ```javascript
    // bad
    function handleThings(opts = {}, name) {
      // ...
    }

    // good
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  - [7.10](#functions--constructor) Never use the Function constructor to create a new function. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

    > Why? Creating a function in this way evaluates a string similarly to `eval()`, which opens vulnerabilities.

    ```javascript
    // bad
    const add = new Function('a', 'b', 'return a + b');

    // still bad
    const subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  - [7.11](#functions--signature-spacing) Spacing in a function signature. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > Why? Consistency is good, and you shouldn’t have to add or remove a space when adding or removing a name.

    ```javascript
    // bad
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // good
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  - [7.12](#functions--mutate-params) Never mutate parameters. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

    ```javascript
    // bad
    function f1(obj) {
      obj.key = 1;
    }

    // good
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  - [7.13](#functions--reassign-params) Never reassign parameters. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign)

    > Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

    ```javascript
    // bad
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // good
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  - [7.14](#functions--spread-vs-apply) Prefer the use of the spread syntax `...` to call variadic functions. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

    > Why? It’s cleaner, you don’t need to supply a context, and you can not easily compose `new` with `apply`.

    ```javascript
    // bad
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // good
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // bad
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // good
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  - [7.15](#functions--signature-invocation-indentation) Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
    // bad
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // good
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // bad
    console.log(foo,
      bar,
      baz);

    // good
    console.log(
      foo,
      bar,
      baz,
    );
    ```
