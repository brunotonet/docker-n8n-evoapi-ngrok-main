# Projeto de Automação com n8n, Evolution API e Ngrok

Bem-vindo! Este repositório traz uma stack completa para automação de fluxos de trabalho e integração de APIs, utilizando **n8n**, **Evolution API**, **PostgreSQL**, **Redis**, **Ngrok** e **Adminer**.

## Pré-requisitos

Antes de começar, instale em sua máquina:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- Conta gratuita no [Ngrok](https://ngrok.com/) (para expor o n8n publicamente)

## Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
```

### 2. Crie sua conta no Ngrok

- Acesse [ngrok.com](https://ngrok.com/) e crie sua conta.
- No painel, copie seu **Authtoken** (exemplo: `1a2b3c4d5e6f7g8h9i0j_xxxxxxxxxxxxxxxxxxxxxx`).

### 3. Configure o arquivo `.env`

- Se houver, copie `.env.example` para `.env`:
  ```bash
  cp .env.example .env
  ```
- Ou crie um `.env` seguindo o modelo abaixo e preencha com seus dados:

```env
# PostgreSQL
POSTGRES_USER=usuario
POSTGRES_PASSWORD=senha
POSTGRES_DB=nome_banco

# n8n
N8N_ENCRYPTION_KEY=SUA_KEY_32_CHAR
N8N_BASIC_AUTH_USER=email
N8N_BASIC_AUTH_PASSWORD=senha

# Evolution API
AUTHENTICATION_API_KEY=SUA_KEY_64_CHAR

# Ngrok (defina o token no arquivo ngrok.yml)
```
> Gere senhas/chaves fortes usando ferramentas como [1Password Generator](https://1password.com/password-generator).

### 4. Suba os serviços

```bash
docker-compose up -d
```

Serão iniciados:
- **n8n** (5678): Automação de fluxos.
- **PostgreSQL** (5432): Banco de dados com pgvector.
- **Evolution API** (8080): API de mensagens.
- **Ngrok** (4040): Painel do túnel público.
- **Redis** (6380): Cache para Evolution API.
- **Adminer** (8081): Interface web do banco.

### 5. Acesse os serviços

- **n8n**: [http://localhost:5678](http://localhost:5678) (credenciais `.env`)
- **Evolution API**: [http://localhost:8080](http://localhost:8080)
- **Adminer**: [http://localhost:8081](http://localhost:8081)
- **Ngrok**: [http://localhost:4040](http://localhost:4040) para obter a URL pública do n8n

### 6. Atualize Webhooks

- A URL do n8n (via Ngrok) muda sempre que o serviço reinicia.
- Consulte [http://localhost:4040](http://localhost:4040) para ver a URL pública (exemplo: `https://abcd-1234.ngrok.io`).
- Atualize todos os webhooks e integrações do n8n/Evolution API com a nova URL sempre que necessário.

### 7. Parando e limpando os serviços

Para parar:
```bash
docker-compose down
```
Para parar e remover volumes (apaga dados!):
```bash
docker-compose down -v
```

## Resumo da Stack

| Serviço         | Descrição                                    | Porta      |
|-----------------|----------------------------------------------|------------|
| n8n             | Automação de fluxos                          | 5678       |
| Evolution API   | API de integração de mensagens               | 8080       |
| PostgreSQL      | Banco de dados (com pgvector)                | 5432       |
| Redis           | Cache para Evolution API                      | 6380       |
| Ngrok           | Túnel público para o n8n                     | 4040       |
| Adminer         | Gerenciador web do banco de dados            | 8081       |

## Notas

- Certifique-se de que as portas citadas estejam livres em seu ambiente.
- A URL do Ngrok é temporária (salvo planos pagos ou configuração avançada).
- **Nunca** compartilhe seu arquivo `.env` publicamente.

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.
