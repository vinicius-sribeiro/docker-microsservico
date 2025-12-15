# Container Proxy

Este container será responsável por executar uma instância do **Nginx**, atuando como proxy da nossa aplicação.

O proxy é responsável por **receber as requisições** e **distribuí-las entre os containers do cluster**, funcionando como um balanceador de carga.


## Criando o container

### Criando a imagem do proxy

1. Crie um arquivo para definir as configurações do proxy (`nginx.conf`).

2. Crie um **dockerfile** para gerar uma nova imagem com as configurações do proxy. Utilize a imagem do `nginx` como base.

3. Faça o build do dockerfile para criar a nova imagem.
```bash
docker build -t <image_proxy_name> .
```

- **Exemplo:**
```bash
docker build -t proxy-app .
```

### Rodando o container

```bash
docker run \
  --name <container_name> \
  -dti \
  -p 4500:4500
  <image_proxy_name>
```

- **Exemplo Completo**: 
```bash
docker run \
  --name my-proxy-app \
  -dti \
  -p 4500:4500
  proxy-app
```