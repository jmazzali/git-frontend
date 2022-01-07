# Anotações | Javascript

## JS

### Funções

As funções podem ser construídas de 2 diferentes maneiras

```js

cosnt test = function(){
    return 'função em expressão'
}

function test(){
    return 'função declarada'
}

```

**Observação**: em funções declaradas podemos chamá-la antes da linha de declaração - isso por conta do hoisting; enquanto em funções de expressão isso não ocorre

Exemplo:

```js

// console.log(`${x()}`)
const x = function(){
    return 'x = 0'
}


console.log(`${y()}`)
function y(){
    return 'y = 0'
}

```

Na linha comentada, o erro seria o seguinte: 

```

Cannot access 'x' before initialization

```

---

### Tipos de Variáveis

* let

As variáveis declaradas como let, podem ser acessadas apenas após sua declaração em seu escopo principal (ou filhos - o inverso não funciona, por exemplo existe a variavel let X em um escopo fechado, fora dele (no pai) não vai exisitir). Exemplificando:

```js
let qtd = 0

{/*ESCOPO 1*/
function dependeQuantidade(){
    let pmt
    if(qtd === 0){
        pmt = '1'
    } else{
        pmt = '10'
    }
    qtd += 1
    return pmt + ' na ' + qtd + ' chamada'
}

console.log(`${pmt}`)

    {/*ESCOPO 2*/
    console.log(`NOVO ESCOPO: ${qtd}`)
    }

console.log(`PRIMEIRA CHAMADA = ${dependeQuantidade()}`)
console.log(`SEGUNDA CHAMADA = ${dependeQuantidade()}`)
console.log(`TERCEIRA CHAMADA = ${dependeQuantidade()}`)
}

/*VOLTA ESCOPO GLOBAL*/
console.log(`${qtd}`)
console.log(`${pmt}`)
```

Nesse exemplo, na função dependeQuantidade(), a variável qtd é acessada em um diferente escopo (ESCOPO 1), isso porquê o conteúdo da função é *filho do filho do escopo global* (existe o escopo global, abre-se outro escopo, por fim existe o escopo da função)

No ESCOPO 2, a variável está definida e com um tipo de dado já inserido, confirmando mais uma vez que em escopos filhos (em relação a declaração de uma variável let) é possível acessadar e manipular um variavel do escopo pai

Todavia, a saída depois da função chamando uma variável do tipo let (pmt) já ocasionaria um erro(ESCOPO 1), visto que ela não estaria definida - tudo por conta de pmt não possuir relacionamento de filho com essa saída de fora do escopo da função

Isso também aconteceria com a linha que procede o fechamento desse escopo (VOLTA ESCOPO GLOBAL), mas não teria erro com relação a variável qtd

---
### Enviando argumentos para funções

Para isso vamos usar o exemplo base do tópico acima, mas com novas alterações

```js
let qtd = 0

console.log(`${qtd}`)
{
function dependeQuantidade(qtd){
    let pmt
    if(qtd === 0){
        pmt = '1'
    } else{
        pmt = '10'
    }
    qtd += 1
    return pmt + ' na ' + qtd + ' chamada'
}

console.log(`${dependeQuantidade(qtd)}`)
console.log(`${dependeQuantidade(qtd)}`)
console.log(`${dependeQuantidade(qtd)}`)
}

console.log(`${qtd}`)
```

A saída desse bloco de javascript seria:

```
0
0
1 na 1 chamada
1 na 1 chamada
1 na 1 chamada
```

Entendendo: diferentemente do exemplo anterior, nesse bloco:
* criamos uma variável let **qtd**
* criamos uma função que vai receber **qtd**(não o mesmo que a variável) como parametro
* convocamos a função enviando a variável let **qtd** como argumento
* função vai receber essa variavel como **parametro**, na condição irá atribuir 0 à variável pmt (do tipo let) - visto que o **parametro** que ele está **em condição** (nosso argumento) ainda possui valor 0
* o parametro **dentro da função** vai receber +1 ao seu valor (como cada vez que chamamos a função temos que qtd vale 0, na mensagem de retorno sempre possuirá valor 1)
* retorna a mensagem
* invocamos novamente a função que vai enviar o mesmo argumento (variável **qtd**)
* percebe-se que o valor desse argumento não foi alterado, o que foi alterado foi o parametro DENTRO DA FUNÇÃO

Portanto, deve-se atentar no bloco que, apesar do mesmo nome de variável, existe uma diferença entre nosso argumento (originado da nossa variável let no escopo global) e o parâmetro que é manipulado internamente

---