# Container MySQL

Este container será responsável por executar uma instância do MySQL, permitindo a persistência dos dados por meio de volumes Docker.

## Criando o container

### Criando o volume do banco

```bash
docker volume create <volume_name>
```
Este volume será utilizado para **armazenar e persistir** os dados do banco no servidor, mesmo após a reinicialização ou remoção do container.

- **Exemplo:**
```bash
docker volume create mysql-data
```

### Rodando o container

```bash
docker run \
  --name <container_name> \
  -v <volume_name>:/var/lib/mysql \
  -d \
  -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD=<senha_root> \
  -e MYSQL_DATABASE=<database_name> \
  mysql:<tag>
```

- Parâmetros:
  - `--name`: Define o nome do container.
  - `-p`: Mapeia a porta do host para a porta do container (**host:container**).
  - `-v`: Cria o vínculo entre o volume Docker e o diretório onde o MySQL armazena os dados
  (`volume <=> /var/lib/mysql`).
  - `-e`: Define variáveis de ambiente utilizadas na inicialização do container.
  - `tag`: Define a versão da imagem do MySQL.


- **Exemplo Completo**: 
```bash
docker run \
  --name mysql-db \
  -v mysql-data:/var/lib/mysql \
  -d \
  -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD=senha123 \
  -e MYSQL_DATABASE=testedb \
  mysql:5.7
```

Após a criação do container, espere um pouco para poder estabelecer uma conexão com o banco de dados.

Comando para verificar a execução do container: 

`docker logs <container_name>`


## Utilizando o banco

Após o container subir o bando de dados, você pode acessar o banco de dados de qualquer aplicação e executar consultas normalmente, basta passar os parâmetros definidos na criação do container.

O arquivo `Banco.sql` é apenas uma consulta de exemplo.

# Continuação

➡️ [Preparando o Container PHP](/php/README.md)
