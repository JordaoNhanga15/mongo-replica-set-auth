# Projeto MongoDB Replica Set com Autenticação

Este projeto configura o MongoDB com Replica Set e autenticação habilitada utilizando Docker e Docker Compose.

## Passos para Configuração

1. Existe um arquivo `docker-compose.yml` para definir os serviços do MongoDB com Replica Set habilitado.
2. Inicie o contêiner utilizando o Docker Compose.
3. Verifique o status do Replica Set para garantir que está configurado corretamente.

   ```bash
   docker exec -it replica-set-mongo-mongo_lotus-1 mongosh --port 27017

4. Caso o Replica Set não esteja configurado automaticamente, realize a configuração manualmente.

Para configurar a autenticação, crie o usuário root no banco de dados `admin`. No shell do MongoDB, execute o seguinte comando:

   ```javascript
   use admin
   db.createUser({
     user: "root",
     pwd: "example",
     roles: [{ role: "root", db: "admin" }]
   })
```

5. Teste a conexão com o MongoDB usando a string de conexão com autenticação e Replica Set.
Agora que o usuário foi criado, você pode testar a conexão com a seguinte string de conexão:
   ```plaintext
   mongodb://root:example@172.17.0.1:27017/?replicaSet=rs0&authSource=admin
   ```

6. Verifique os logs do contêiner para identificar possíveis erros ou informações relevantes.

7. Finalize o contêiner quando necessário.

> **Nota:** Certifique-se de que a rede está configurada corretamente para uso em diferentes máquinas ou ambientes, e que a solução pode ser adaptável ao contexto.
