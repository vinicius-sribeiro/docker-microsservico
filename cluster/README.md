# Cluster (Docker Swarm)

O cluster é um grupo de computadores ligados que trabalham juntos.

Computadores em cluster **executam a mesma tarefa, controlado e programado** por software.

Cada computador em um cluster é conhecido como **nó (node)**.

O **Docker Swarm** é a ferramenta do docker que permite criarmos um cluster.

No Docker Swarm, os nós são divididos em dois papeis:
- **Manager** -> Máquina principal, que vai administrar o cluster.
- **Workes** -> Máquinas que irão apenas executar as tarefas/containers.

## Criando o cluster

### Criando o Manager

```bash
docker swarm init
```
- Esse comando irá retornar outro comando para adicionarmos os Workes.

```bash
docker swarm join ....
```
- Basta colar esse comando na outra máquina e executar.

## Rodando o serviço

O serviços serão os containers que rodarão nossa aplicação nos nós(nodes).

Para rodar o serviço dentro do cluster basta executar:

```bash
docker service create \
  --name <service_name> \
  --replicas <valor> \
  -dt \
  -p <port_host>:<port_service> \
  -v <volume>:<lugar_da_aplicacao>
  <image_name>
```

- **Exemplo Completo**: 
```bash
docker service create \
 --name web-server \
 --replicas 5 \
 -dt \
 -p 80:80 \
 -v app:/app/ \
 webdevops/php-apache:alpine-php7
```

Explicação do volume feita em [Criando Volume do App](php/README.md#criando-volume-do-app).

## Replicando um volume dentro do cluster

Um problema do docker swarm é que ele não replica o que está armazenado entre os nós, então se houve uma mudança em um, nada acontece no outro.

Para resolvermos isso, usamos o `nfs-server` (Manager) e o `nfs-common` (Workers).

- Manager 
```bash
sudo apt install -y nfs-server
```

```bash
nano /etc/exports
```

Use o arquivo [exports](cluster/exports) como exemplo.

```bash
exports -ar
```

- Workes
```bash
sudo apt install -y nfs-common
```

```bash
mount -o v4 <ip_host>:<volume_path_host> <volume_path_node>
```


# Continuação

➡️ [Criando o Proxy](proxy/README.md#container-proxy)