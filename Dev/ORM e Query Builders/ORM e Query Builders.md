## ORM - Object Relational Mapper

Responsável por integrar POO com o banco de dados, utilizando objetos e classes. Praticamente nenhuma preocupação com a sintaxe da linguagem SQL ou o banco que está sendo utilizado. Para montar as querys será utilizado objetos e métodos, sem precisar escrever SQL diretamente. Dessa maneira, você pode manipular os dados usando objetos e métodos, sem precisar escrever SQL diretamente.
Então, como exemplo, a sintaxe de uma query feita com sequelize, ficaria assim
``` js
// Para buscar um usuário com id = 1 
User.findByPk(1).then(
	user => { console.log(user); 
}).catch(error => { 
	console.error(error); 
});
```