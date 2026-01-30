# N8N Complete Setup

Uma configuração completa e pronta para produção do **n8n** (plataforma de automação de fluxo de trabalho) usando Docker Compose.

## 📋 Descrição

Este projeto fornece uma instalação containerizada do n8n com suporte completo a:

- **Banco de Dados**: PostgreSQL 15 para persistência de dados
- **Cache**: Redis 7 para gerenciamento de filas e cache
- **Autenticação**: Suporte a autenticação básica HTTP
- **Timezone**: Configurado para America/Sao_Paulo (Brasil)
- **HTTPS**: Suporte a conexões seguras via HTTPS

## 🚀 Requisitos

- Docker e Docker Compose instalados
- Acesso à porta 443 (HTTPS) e 80 (HTTP)
- Arquivo `.env` configurado com as variáveis de ambiente

## ⚙️ Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/mlluiz/mlluiz_n8n_complete.git
cd mlluiz_n8n_complete
```

### 2. Configure as variáveis de ambiente

Crie um arquivo `.env` baseado no `.env.example`:

```bash
cp .env.example .env
```

### 3. Edite o arquivo `.env`

Atualize as seguintes variáveis:

```env
# Database PostgreSQL
POSTGRES_DB=n8n
POSTGRES_USER=n8n
POSTGRES_PASSWORD=sua_senha_forte_aqui

# Redis
REDIS_PASSWORD=sua_senha_redis_aqui

# N8N Configuration
N8N_DOMAIN=seu-dominio.com.br
N8N_USER=admin
N8N_PASS=sua_senha_n8n_aqui
N8N_BASIC_AUTH_ACTIVE=true
```

### 4. Inicie os containers

```bash
docker-compose up -d
```

## 📱 Acessando o N8N

Após iniciar os containers, acesse:

```
https://seu-dominio.com.br
```

**Credenciais padrão**:

- **Usuário**: Valor de `N8N_USER` do `.env`
- **Senha**: Valor de `N8N_PASS` do `.env`

## 🛠️ Serviços

### PostgreSQL

- **Container**: postgres
- **Imagem**: postgres:15
- **Porta interna**: 5432
- **Volume**: `postgres_data`

### Redis

- **Container**: redis
- **Imagem**: redis:7
- **Volume**: `redis_data`

### N8N

- **Container**: n8n
- **Imagem**: n8nio/n8n:latest
- **Porta**: 443 (HTTPS) / 80 (HTTP)

## 🔧 Comandos Úteis

### Iniciar os containers

```bash
docker-compose up -d
```

### Parar os containers

```bash
docker-compose down
```

### Visualizar logs

```bash
docker-compose logs -f n8n
```

### Reiniciar o N8N

```bash
docker-compose restart n8n
```

### Acessar o shell do PostgreSQL

```bash
docker-compose exec postgres psql -U n8n -d n8n
```

## 📊 Variáveis de Ambiente

| Variável                | Descrição                  | Exemplo            |
| ----------------------- | -------------------------- | ------------------ |
| `POSTGRES_DB`           | Nome do banco de dados     | n8n                |
| `POSTGRES_USER`         | Usuário PostgreSQL         | n8n                |
| `POSTGRES_PASSWORD`     | Senha PostgreSQL           | senha_forte        |
| `REDIS_PASSWORD`        | Senha Redis                | senha_forte        |
| `N8N_DOMAIN`            | Domínio do N8N             | n8n.exemplo.com.br |
| `N8N_USER`              | Usuário de autenticação    | admin              |
| `N8N_PASS`              | Senha de autenticação      | senha_forte        |
| `N8N_BASIC_AUTH_ACTIVE` | Ativar autenticação básica | true               |

## 🌍 Timezone

O N8N está configurado para usar o timezone `America/Sao_Paulo`. Para alterá-lo, modifique a variável `GENERIC_TIMEZONE` no `docker-compose.yaml`.

## 📁 Volumes

Os dados são persistidos em volumes Docker:

- **postgres_data**: Armazena o banco de dados PostgreSQL
- **redis_data**: Armazena os dados do Redis

## 🔒 Segurança

⚠️ **Importante**:

- Sempre altere as senhas padrão no arquivo `.env`
- Use senhas fortes (mínimo 12 caracteres com números, letras e símbolos)
- Nunca commite o arquivo `.env` no repositório
- Configure SSL/TLS corretamente no seu servidor

## 📝 Licença

[Adicionar informações de licença se aplicável]

## 👤 Autor

mlluiz - [GitHub](https://github.com/mlluiz)

## 📞 Suporte

Para suporte e questões, abra uma issue no repositório.
