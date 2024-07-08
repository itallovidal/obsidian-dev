# API Routes

Muitas vezes no desenvolvimento da nossa aplicação, para juntar, manipular e preparar dados para nossa aplicação frontend, nos vemos na necessidade de criar uma API para lidar com esses processos, tendo duas aplicações trabalhando em conjunto.

Para contextos mais simples, o next possui uma feature chamada API Routes, que nos fornece a possibilidade da criação de uma API RESTful, eliminando a necessidade da criação de uma segunda base de códigos para esses tipos de processos.

O processo é muito parecido com o desenvolvimento de API com `*fastify*` ou `*express*`. Para todo conteúdo dentro da pasta `*/pages/**api` ,*** o next cria um endpoint para que possamos utilizá-lo.

```tsx
import {NextApiRequest, NextApiResponse} from "next";

export default async function handler(req: NextApiRequest, res: NextApiResponse){

		// fazer alguma coisa

    return res.status(201).json({
        message: 'Olá mundo!'
    })
}
```

<aside> 💡 Atenção: O next não faz diferenciação de método HTTP. Independente do método chamado, se a rota for passada corretamente a função será disparada.

</aside>

<aside> 💡 Atenção: essa função deve ser exportada com `*export default*`

</aside>

Subtópico de: [[Next]]