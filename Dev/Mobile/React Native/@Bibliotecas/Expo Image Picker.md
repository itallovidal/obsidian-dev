Biblioteca para pegar uma imagem da galeria do usuário.

```jsx
npx expo install expo-image-picker
```

```jsx
//app.json

{
  "expo": {
    "plugins": [
      [
        "expo-image-picker",
        {
          "photosPermission": "The app accesses your photos to let you share them with your friends."
        }
      ]
    ]
  }
}
```

Agora precisamos importar o ImagePicker e utilizá-lo. Lembrando que esse é um processo assíncrono.

```jsx
import * as ImagePicker from 'expo-image-picker'

async function handleUserPhoto(){
																								// abre a galeria
        const selectedPhoto = await ImagePicker.launchImageLibraryAsync()

				// verifica se o processo foi cancelado
        if(selectedPhoto.canceled){
            return
        }

				// seleciona a URI da imagem e atualiza
        setUserPhoto(selectedPhoto.assets[0].uri)
    }
```

Uma das coisas interessantes é que podemos utilizar um objeto de configuração com algumas propriedades interessantes:

```jsx
// exibe apenas mídia que é foto
mediaTypes: ImagePicker.MediaTypeOptions.Images,
// permite cortar a foto
allowsEditing: true,

```


Subtópico: [[Bibliotecas RN]]