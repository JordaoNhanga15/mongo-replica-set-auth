Claro! Aqui está o conteúdo do **README.md** com todos os comandos que você precisa:

```markdown
# MongoDB com Replica Set e Autenticação no Docker

Este README descreve os passos para configurar o MongoDB com Replica Set e autenticação habilitada utilizando Docker e Docker Compose.

## Passos para Configuração

### 1. Criar o Arquivo `docker-compose.yml`

Crie um arquivo `docker-compose.yml` com a seguinte configuração:

```yaml
version: "3.8"

services:
  mongo_lotus:
    image: mongo:7.0
    command: ["--replSet", "rs0", "--bind_ip_all", "--port", "27017"]
    ports:
      - 27017:27017
    extra_hosts:
      - "host.docker.internal:host-gateway"
    healthcheck:
      test: echo "try { rs.status() } catch (err) { rs.initiate({_id:'rs0',members:[{_id:0,host:'172.17.0.1:27017'}]}) }" | mongosh --port 27017 --quiet
      interval: 5s
      timeout: 30s
      start_period: 0s
      start_interval: 1s
      retries: 30
    volumes:
      - "mongo1_data:/data/db"
      - "mongo1_config:/data/configdb"

volumes:
  mongo1_data:
  mongo1_config:
```

### 2. Subir o Contêiner MongoDB com Docker Compose

Para iniciar o contêiner MongoDB com a configuração de Replica Set, execute o seguinte comando no terminal:

```bash
docker-compose up -d
```

Isso irá iniciar o contêiner e configurar o MongoDB em modo Replica Set.

### 3. Acessar o MongoDB e Verificar o Status do Replica Set

Após a inicialização do contêiner, acesse o MongoDB usando o comando `mongosh` dentro do contêiner:

```bash
docker exec -it replica-set-mongo-mongo_lotus-1 mongosh --port 27017
```

No shell do MongoDB, execute:

```javascript
rs.status();
```

Se o replica set ainda não foi configurado corretamente, inicie a configuração manualmente:

```javascript
rs.initiate({
  _id: 'rs0',
  members: [
    { _id: 0, host: "172.17.0.1:27017" }
  ]
});
```

### 4. Criar o Usuário Administrador

Para configurar a autenticação, crie o usuário `root` no banco de dados `admin`. No shell do MongoDB, execute o seguinte comando:

```javascript
use admin
db.createUser({
  user: "root",
  pwd: "example",
  roles: [{ role: "root", db: "admin" }]
})
```

Isso cria um usuário administrador com permissões completas.

### 5. Testar a Conexão com o MongoDB

Agora que o usuário foi criado, você pode testar a conexão com a string de conexão do MongoDB, que inclui a autenticação e a configuração do replica set. Use a seguinte string de conexão:

```plaintext
mongodb://root:example@172.17.0.1:27017/?replicaSet=rs0&authSource=admin
```

### 6. Verificar Logs do Contêiner MongoDB

Se houver qualquer erro ou para depuração, você pode visualizar os logs do contêiner MongoDB com o comando:

```bash
docker logs replica-set-mongo-mongo_lotus-1
```

### 7. Parar o Contêiner

Para parar o contêiner MongoDB, use o comando:

```bash
docker-compose down
```

## Conclusão

Agora o MongoDB está configurado com Replica Set e autenticação. Você pode usar esse ambiente para desenvolver, testar ou até mesmo para produção, se configurar adequadamente.

---

> **Nota:** Certifique-se de que a rede entre os contêineres está configurada corretamente para que o MongoDB funcione como esperado em diferentes máquinas ou ambientes.
```
