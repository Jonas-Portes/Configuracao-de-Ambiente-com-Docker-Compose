<h1 align="center">Docker Compose - Atividade 2</h1>

# Feito com as aulas da [RocketSeat](https://app.rocketseat.com.br/me/jonasportes)


## Pŕe-requisitos

- Docker
- Docker compose

## Arquitetura do projeto

- **MySQL 8**: Banco de dados relacional
- **App**: Aplicação customizada visualiazadora de arquivos
- **Network backtier**: Rede para comunicação entre containers
- **Volume db-data**: Persistência de dados do MySQL


## Variáveis de Ambiente

### MySQL

| Variável | Valor | Descrição |
|----------|-------|-----------|
| `MYSQL_ROOT_PASSWORD` | `rootadm` | Senha do usuário root |
| `MYSQL_DATABASE` | `atividade-db` | Nome do banco criado automaticamente |
| `MYSQL_USER` | `admin` | Usuário adicional criado |
| `MYSQL_PASSWORD` | `rootadm` | Senha do usuário admin |

### App Container

O container `app` não possui variáveis de ambiente definidas no docker-compose.yml. Configure conforme necessário para sua aplicação.







# Como utilizar

Baixe o projeto
Em sua pasta raiz, abra um terminal e digite 
Utilize os comandos abaixo conforme necessidade:

```bash
# Construir e iniciar em modo detached (background)
docker compose up -d

# Construir e iniciar com logs visíveis
docker compose up

# Forçar rebuild das imagens
docker compose up --build -d
```

### Parar os containers

```bash
# Parar os containers (mantém volumes)
docker compose down

# Parar e remover volumes (CUIDADO: apaga dados do banco)
docker compose down -v
```

### Visualizar logs

```bash
# Logs de todos os serviços
docker compose logs

# Logs em tempo real
docker compose logs -f

# Logs de um serviço específico
docker compose logs mysql
docker compose logs app
```

### Verificar status dos containers

```bash
docker compose ps
```


##  Testando a Conexão


### 1. Testar conexão MySQL do host

```bash
# Usando cliente MySQL (se instalado)
mysql -h 127.0.0.1 -P 3306 -u admin -prootadm atividade-db

# Ou usando Docker
docker compose exec mysql mysql -u admin -prootadm atividade-db
```

### 2. Testar conexão entre containers

Entre no container da aplicação e teste a conexão com o MySQL:

```bash
# Acessar o shell do container app
docker compose exec app sh

# Dentro do container, testar conexão (exemplo com nc/netcat)
nc -zv mysql 3306

```

### 3. Verificar rede

```bash
# Listar redes
docker network ls

# Inspecionar a rede backtier
docker network inspect backtier

# Ver containers conectados à rede
docker network inspect backtier | grep -A 5 "Containers"
```


### 4. Testar aplicação

```bash
# Fazer requisição HTTP para a aplicação
curl http://localhost:3001

# Ou abrir no navegador
# http://localhost:3001
```