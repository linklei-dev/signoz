# signoz
Recursos para executar SigNoz, ferramenta de observabilidade e registro de logs de servidor.

## Versão
- Versão do SigNoz, em 2026-01-01: v0.105.1

# Para executar a aplicação em ambiente produção:
- Acesse: /home/ec2-user/signoz/deploy/docker
- suba os serviços:
```sh
docker compose up -d --remove-orphans
```
- Para parar os containers:
```sh
docker compose stop
```
- Para destruir os containers:
```sh
docker compose down
```


## Criar banco de dados PostgreSQL:
- Banco de dados do postgresql utilizado para armazenar configurações de conta e de usuário do signoz;
- Script SQL para criar o banco:
```sql
-- 1. Criar o banco de dados
CREATE DATABASE signoz;

-- 2. Criar o usuário (se ainda não existir)
CREATE USER signoz_user WITH PASSWORD 'senha_aqui';

-- 3. Conceder permissões necessárias
GRANT ALL PRIVILEGES ON DATABASE signoz TO signoz_user;

-- 4. Conectar ao banco signoz e conceder permissões no schema
-- signoz
GRANT ALL ON SCHEMA public TO signoz_user;
GRANT CREATE ON SCHEMA public TO signoz_user;

```


## Comando CURL para testar envio de log para o servidor do signoz:

```sh
curl --location 'http://172.31.93.164:8082' \
--header 'Content-Type: application/json' \
--data '[
  {
      "trace_id": "000000000000000018c51935df0b93b9",
      "span_id": "18c51935df0b93b9",
      "trace_flags": 0,
      "severity_text": "info",
      "severity_number": 4,
      "attributes": {
          "method": "GET",
          "path": "/api/test"
      },
      "resources": {
          "host": "myhost",
          "namespace": "prod"
      },
      "message": "This is a log line"
  }
]'

```