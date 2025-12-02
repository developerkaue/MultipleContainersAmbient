Multiple Containers Environment - Docker Compose Project

🎯 Project Overview:
O objetivo desse repositório é apenas demonstrar a utilização de 2 containers funcionando ao mesmo tempo na aplicação utilizando Docker.

É uma api em Node.js/NestJS extremamente básica, apenas com o código inicial, para dar ênfase na criação dos containers.

Foram criados 2 containers:
1 - Camada de aplicação.
2 - Utilização do banco de dados.


Utilizei duas etapas na criação dos containers, primeiro criei o arquivo Dockerfile para fins de conhecimento e saber como funciona a criação do container de forma completa,
buscando a imagem no dockerhub e realizando toda a configuração do ambiente necessário para rodar a camada de aplicação.

Logo após eu simplifico tudo isso com o docker-compose colocando os serviços a serem utilizados, algumas variáveis de ambiente e a configuração de networks e volumes.

Arquivos : DockerFile e docker-compose.

Comandos para subir os containers:
bash: docker-compose up -d

📄 License
This project is MIT licensed.

👨‍💻 Author
Kaue Fernandes

GitHub: @developerkaue

Email: kauecaobiancofernandes2@gmail.com

🤝 Contributing
Feel free to submit issues and enhancement requests!

Note: This is a demonstration project focusing on Docker container orchestration. The API is a simple NestJS starter with added database connectivity examples.
