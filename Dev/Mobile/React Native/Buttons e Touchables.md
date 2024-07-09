# Buttons e Toucheables

Para lidar com situações onde possuímos um botão que dispara um evento, é natural pensarmos no componente `<Button/>`. Porém, dentro do ecossistema do React temos em nossa disposição outros componentes que cumprem essa função tão bem ou melhor quanto.

## Button: Limitações

Este componente é bem direito: renderiza um botão em nossa tela para que possamos realizar uma ação no momento do toque. O problema é que ele representa um botão padrão do sistema, variando seu estilo e comportamento ao toque de acordo com o sistema.

Sua estilização é muito básica, já que ele não aceita a propriedade `*style*`. Além disso, ao trocar a cor pela propriedade `*color*`, elementos diferentes mudam de acordo com a plataforma: no _Android_, muda-se a cor de fundo e no _iOS_ muda-se a cor principal. Vejamos:

```jsx
<Button
        title="Botão no iOS!"
        color={'blue'}
      />

<Button
        title="Botão no Android!"
        color={'blue'}
      />
```

![[Pasted image 20240708211803.png]]
![[Pasted image 20240708211922.png]]
## Touchables: Opacity, Highlight, withoutFeedBack

Para resolver essa questão, o react nos disponibiliza componentes que são mais flexíveis na estilização, e que vão se comportar de maneira igual - ou muita parecida - em ambas as plataformas. Além disso, podemos envolver outros elementos tornando-os clicáveis como uma foto, ou uma `*flatList*`, por exemplo. Abaixo podemos

`*<TouchableOpacity>` *****: seu comportamento quando clicado é a diminuição da opacidade.

`*<TouchableHighlight>`: seu comportamento quando clicado é um aumento no brilho.*

`*<TouchableWithoutFeedBack>*`: seu comportamento não muda quando clicado.


Subtópico: [[React Native]]