# Projeto MongoDB Replica Set com Autenticação

Este projeto configura o MongoDB com Replica Set e autenticação habilitada utilizando Docker e Docker Compose.

## Passos para Configuração

1. Crie um arquivo `docker-compose.yml` para definir os serviços do MongoDB com Replica Set habilitado.
2. Inicie o contêiner utilizando o Docker Compose.
3. Verifique o status do Replica Set para garantir que está configurado corretamente.
4. Caso o Replica Set não esteja configurado automaticamente, realize a configuração manualmente.
5. Crie o usuário administrador no banco de dados `admin`.
6. Teste a conexão com o MongoDB usando a string de conexão com autenticação e Replica Set.
7. Verifique os logs do contêiner para identificar possíveis erros ou informações relevantes.
8. Finalize o contêiner quando necessário.

---

> **Nota:** Certifique-se de que a rede está configurada corretamente para uso em diferentes máquinas ou ambientes.
