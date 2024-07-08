Para que possamos utilizar o useForm com o react native teremos que utilizar um `*Controller*`. Ele é um componente responsável por controlar nosso input e manipular as suas mudanças. Possui como atributos `*name*` , `*control`* e `*render*` . O atributo `*render*` recebe uma função que vai renderizar nosso input, e ele desestrutura os métodos do campo `*onChange*` , `onBlur` **e _`value` ._

Vejamos a estrutura básica:

```jsx
<Controller control={control}
            name={"produto"}
            render={({field: {onChange, onBlur, value}})=> (
                <Input onChangeText={onChange}
											 onBlur={onBlur}
											 value={value}/>)} /> 
```


Subtópico: [[Bibliotecas RN]]
Subtópicos: [[Bibliotecas]]