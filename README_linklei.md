# signoz
Recursos para executar SigNoz, ferramenta de observabilidade e registro de logs de servidor.

## Versão
- Versão do SigNoz, em 2026-01-01: v0.105.1

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
