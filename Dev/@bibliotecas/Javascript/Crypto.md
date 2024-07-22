Por algum raio de motivo as operações utilizando o `*crypto*` não funcionam nativamente no react native. Para isso devemos instalar a biblioteca com o expo:

```node
npx expo install expo-crypto
```

Depois é só importar e usar do mesmo jeito

```jsx
import * as crypto from 'expo-crypto';
```

```bash
npm i bcryptjs
```

Subtópicos: [[Bibliotecas]]
Subtópico: [[Bibliotecas RN]]