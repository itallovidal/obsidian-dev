### O que é HTML?

HTML é uma linguagem de marcação de texto que faz parte da construção de uma página web. Seu acrônimo significa HyperText Markup Languagem. Com ela poderemos estruturar nossa página web e organizar categoricamente cada trecho do site. Por ser uma linguagem de marcação, nós não programamos em HTML, já que ela não é uma linguagem de programação.

### Estrutura Base

Abaixo veremos a estrutura básica de como um documento HTML é. Veremos que as palavras reservadas da linguagem ficam entre sinais de _**<>**_ e em sua maioria abrem e fecham. Elas são chamadas de Tags. Ao longo dos nossos estudos veremos diversas tags, o que elas fazem e quais contexto são inseridas. Vamos entender um pouco o que é a estrutura básica.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Título da página</title>
</head>
<body>
</body>
</html>
```

No começo do documento temos uma tag Doctype: além de não fechar, ela tem sua escrita em capslock e um sinal de exclamação a antecedendo. Ela serve apenas para indicar que tipo de documento estamos escrevendo - o HTML.

Abaixo temos uma tag HTML que engloba todas as outras indicando que a página será escrita ali dentro daquele espaço. Em seguida temos uma tag chamada Head e uma tag chamada Body. Na “Cabeça” do documento irá entrar algumas informações importantes sobre o documento, coisas que o usuário final não verá. Importação para fontes, CDNS, arquivos de estilo, arquivos javascript, tags que descrevem ao navegador sobre o que é a página, dentre outras coisas. Além disso podemos definir o título da página, também.

Dentro da tag de corpo, irão entrar de fato o conteúdo exposto para o usuário. Parágrafos, fotos, links, etc etc etc. Antes de partirmos para saber como construímos uma página para o usuário final, devemos entender o que cada coisa da estrutura base nos informa. Ao iniciar o VSCode e digitar ! e apertar o enter, a IDE irá autocompletar a estrutura para nós:

```html
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
```

Você pode perceber que foi preenchido com algumas tags novas e algumas palavras especiais em destaque. Essas palavras são chamadas de atributos, são palavras reservadas da linguagem capazes de fornecer alguma informação especial ou para nós ou para o navegador. Por exemplo, o atributo lang usado na tag HTML indica ao navegador em qual linguagem foi escrita os elementos estáticos - parágrafos - do nosso documento. Caso alguém usando opções de acessibilidade como leitura de tela for ler o site, a voz será definida para aquele idioma.

A tag meta é responsável por informar ao navegador determinada configuração. Podemos ver que a primeira meta tag está dizendo que os conjuntos de caracteres da página são do tipo UTF-8. Isso faz com que caracteres como o cedilha seja mostrados corretamente.

A segunda meta tag é voltada para o internet explorer. Como ele é um navegador antigo e sem suporte ao HTML5, essa tag faz com que ele renderize a página de acordo com outra versão. Esta tag está caindo em desuso já que agora o número de usuários do internet explorer é ínfimo.

A terceira tag é muito importante para facilitar nossa vida.

### O que é ViewPort?

Antigamente as páginas eram pensadas apenas para desktops, então era super comum termos uma página estática onde possuia apenas valores fixos. O problema disso é que com o avanço da tecnologia possibilitando a internet e as páginas irem pra tablets e desktops, criou-se a necessidade de adaptar de alguma formas essas páginas. Hoje em dia temos uma mentalidade muito diferente já que a maioria dos usuários acessam a internet através de dispositivos mobile, temos o pensamento de Mobile First.

Para resolver esse problema foi introduzido o viewport através da meta tag. Viewport é a área visível de uma página da internet. Ele é totalmente relativo, e depende de qual dispositivo você está mexendo. No telefone, por exemplo, ele será muito menor do que em um computador, já que a tela de um telefone é bem menor.

```html
o que estamos configurando             quais configurações
					|                                      |
 <meta name="viewport" content="width=device-width, initial-scale=1.0">

```

Com essa tag as dimensões e escalas das páginas serão iguais independente do dispositivo, já que a largura total é equivalente à largura do próprio dispositivo. Por exemplo, se eu importar uma imagem e para ela ficar com 100% de largura, se eu não uso a tag meta, no telefone a imagem irá ficar maior do que a largura total do telefone.

Agora, se eu informar que a largura da página deve ser relacionada com a largura do dispositivo, esse erro é corrigido. Veremos melhor sobre medidas relativas ao viewport para que possamos construir sites responsivos com mais facilidade em breve!

```html
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	
    <!-- comentando a linha para que ela não tenha efeito 
		<meta name="viewport" content="width=device-width, initial-scale=1.0"> -->
    <title>Document</title>
</head>
<body>
	  <!-- tag que faz com que possamos estilizar o documento -->
    <style>
        img{
           width: 100%;
        }
    </style>
		
    <!-- tag que importa uma imagem -->
    <img src="./imgs/foto.jpg" alt="" srcset="">
</body>
</html>
```

### Modelo de Caixas.

Um dos pontos mais importantes na construção de uma página bem estrutura é o entendimento da lógica do modelo de caixas usado na WEB. Veremos essa lógica mais a frente novamente com o CSS, mas é importante desde já que você entenda esse conceito.

Imagine o seu guarda roupa. O objetivo primário dele é guardar suas roupas. Pessoas bem organizadas possuem o guarda roupa todo segmentado: gavetas para cuecas, armários para roupas de sair, armário para roupas de ficar em casa. Parte dos tênis, parte dos casacos. Lugarzinho para colocar colchas e edredons. Percebe que, apesar de você poder simplesmente fazer um amontoado de roupa e jogar dentro do guarda roupa, é muito melhor você ter uma parte para cada segmento?

E mesmo nesses segmentos, você tem subsegmentos! Você quer uma meia. Então você abre o guarda roupa, depois abre a gaveta, depois abre o seu saco de meia, e pega a meia. Você não deixa a meia no vazio do espaço tempo. Você não deixa um amontoado de meias, um amontoado de blusas, um amontoado de calças jogado no quarto - ou pelo menos não deveria né.

Com HTML iremos aplicar a mesma lógica. Vamos ver na próxima seção.

Tópico: [[Front-end]]