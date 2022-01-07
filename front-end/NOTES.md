# Anotações | FRONT-END

## HTML

---

## CSS

---

## JS

### TIPOS DE VARIÁVEIS

* let
As variáveis declaradas como let, podem ser acessadas apenas após sua declaração em seu escopo principal (ou filhos - o inverso não funciona, por exemplo existe a variavel let X em um escopo fechado, fora dele (no pai) não vai exisitir). Exemplificando:

```js

let qtd = 0

{
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

console.log(`COMO QUE UMA VARIÁVEL DO TIPO LET, DECLARADA NO ESCOPO GLOBAL, ESTÁ SENDO ACESSADA PELO ESCOPO DA FUNÇÃO?`)
console.log(`${pmt}`)

{
console.log(`NOVO ESCOPO: ${qtd}`)
}

console.log(`PRIMEIRA CHAMADA = ${dependeQuantidade()}`)
console.log(`SEGUNDA CHAMADA = ${dependeQuantidade()}`)
console.log(`TERCEIRA CHAMADA = ${dependeQuantidade()}`)
}

console.log(`${qtd}`)
console.log(`${pmt}`)
```

Nesse exemplo, na função dependeQuantidade(), a variável qtd é acessada em um diferente escopo, isso porquê o conteúdo da função é *filho do filho do escopo global* (existe o escopo global, abre-se outro escopo, por fim existe o escopo da função)

Todavia, a saída depois da função chamando uma variável do tipo let (pmt) já ocasionaria um erro, visto que ela não estaria definida - tudo por conta de pmt não possuir relacionamento de filho com essa saída de fora do escopo da função

Isso também aconteceria com a linha que procede o fechamento desse escopo (que contém o escopo da função dentro dele)

---