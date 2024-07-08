No js é muito comum que nós queiramos capturar a posição do mouse na tela, ou capturar o tamanho atual de um elemento, mexer com o scroll da página ou quem sabe a posição em relação ao topo da página. Neste documento veremos alguns métodos e propriedades interessantes que vai nos ajudar a manipular nossa página.

### _PageY_ e _PageX_

Para capturar a posição do mouse em relação ao documento podemos utilizar `*PageY*` e `*PageX*`.

```jsx
// neste caso estamos disparando o evento em 
// qualquer lugar clicado no body
document.body.addEventListener('click', (e)=>{
    console.log(e.pageX)
    console.log(e.pageY)
})
```

### _OffsetWidth / OffsetHeight e ClientWidth / ClientHeight_

A diferença entre offset e client é basicamente que o client quando se tem um elemento que tem borda, ela é retirada da largura total.

Supondo que temos um elemento que possui 500px e uma borda de 100px.

Com um `*clientWidth*` ele devolverá 400px de elemento.

Com `*OffsetWidth*` ele devolverá 500px de elemento.

Lembrando que essas propriedades sempre devolverão valores em **PX**.

- _**OffsetWidth / OffsetHeight**_
    - **Margem não** é adicionada à conta
    - **Padding não** é adicionado à conta
    - **Borda não** é adicionada à conta
- _**ClientWidth / ClientHeight**_
    - **Margem não** é adicionada à conta
    - **Padding não** é adicionado à conta
    - **Borda é retirada da conta da largura total** largura = largura - borda

### _GetBoundingClientRect e OffsetTop/left/etc_

O método `*GetBoundingClientRect*` retorna um objeto com 8 propriedades muito úteis. O tamanho do elemento (altura e largura) e a distância dele às 4 laterais (left, top, right, bottom) em relação ao viewport.

- `*Width*` e `*Height*`
    
    - Retorna os mesmos valores do OffsetWidth
- `*Top / y`* , `*Bottom*`
    
    - É a distância da borda desejada em **relação ao topo da janela.**
- `*Left / x`* , `*right*`
    
    - É a distância da borda desejada em **relação ao lado esquerdo da janela.**
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/651f7003-14cd-4c7b-8ab6-899c1c0260cf/Untitled.png)
    

O método `*OffsetTop*`- assim como left, right e bottom - também nos retorna a distância entre a borda do elemento com o lado/topo, porém ele não leva em consideração o scroll da página assim como o `*getBoundingClientRect*` considera.

Por exemplo, vamos supor que temos um container no final da página, um `*footer*`. Quando a página carregar, o `*getBoundingClientRect*` e o `*offsetTop`* serão iguais, pois ainda não ‘scrollamos’ para baixo.

Porém a medida que nós chegamos no final da página, o `*footer`* vai subindo para mais próximo do topo da janela, até que chega um momento que ele aparece e nós alçamos o final da página.

Com o `*getBoundingClientRect*`, iremos perceber que a medida que descemos esse valor muda, já que esse método acompanha a posição do scroll e a posição da página como um todo.

Com o `*offsetTop*`, o valor permanece o de origem, já que ele não é atualizado conforme descemos a página.

### Mexendo com o Scroll: ScrollTop e ScrollY

As propriedades `*ScrollTop*` e `*ScrollLeft*` são para elementos que possui um `*overflow: scroll*`, e com elas podemos capturar quantos pixels esses elementos já rolaram.

Já a propriedade `*ScrollY*` e `*ScrollX*` são propriedades relacionadas à janela - podemos capturar quantos pixels o usuário está de distância do topo ou da lateral esquerda. Essa propriedade é uma propriedade `*read-only*`. Para alterar seus valores use um dos métodos de scroll.

### ScrollTo e ScrollBy

Com `*scrollBy`* nós podemos ‘’scrollar’’ a página uma quantia desejada de pixels tanto horizontal quanto verticalmente.

Então se quisermos descer _**+ 100px**_, podemos utilizar `*window.scrollBy(0, 100)`*

Já com `*scrollTo`* a página é levada para o local especificado. Então no caso se quisermos ir de 0px para o ponto _**1500px do topo**_, utilizamos `*window.scrollTo(0, 1500px)*`

Linguagem: [[Javascript]]