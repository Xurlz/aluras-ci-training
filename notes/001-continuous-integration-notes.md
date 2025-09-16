Integração Contínua
---

### O que é Integração Contínua

Conceito que defende que as alterações devem ser integradas ao código de forma frequente, contínua. Com integrações frequentes, ações podem ser tomadas de forma ágil, evitando problemas.

Processos automatizados são necessários, para isso, usam-se ferramentas para esse propósito.

A Integração contínua é toda a cultura de integrar modificações frequentemente, ele é erroneamente definido como apenas uma parte do todo.

### Iniciando projeto

Será configurada uma pipeline para o deploy de um projeto de uma linguagem não conhecida. Apenas os princípios basicos da CI serão necessários para a configuraçào

#### Deploy

Primeiro clone o repositório (`git clone`).

Projeto é um gerenciador de estudantes escrito em Go.

Deve-se utilizar a ferramenta **Docker**. No projeto, há um `docker-compose.yml` com dois serviços `app` e `postgres`.

`docker-compose.yml`:
```docker-compose
services:
  postgres:
    image: "postgres"
    environment:
      - POSTGRES_USER=root
      - POSTGRES_PASSWORD=root
      - POSTGRES_DB=root
    volumes:
      - ./postgres-data:/var/lib/postgresql/data

  app:
  image: golang:1.22
  command:
    - go
    - run
    - main.go
  volumes:
    - ./:/app
  working_dir: /app
  ports:
    - 8080:8080
  depends_on:
    - postgres
```

Após o clone, execute:

```bash
docker compose up
```

Para os serviços não bloquearem o TTY com logs, execute:

```bash
docker compose up -d
```

Comando `docker compose logs` com `-f` segue os logs:

```bash
docker compose logs -f app
```

Acesse o `http://localhost:8080`

Para lista: `localhost:8080/alunos`
Para saudação `localhost:8080/alunos/vinicius`

Resposta:
```json
{"API diz":"E aí Vinícius, tudo beleza?"}
```

#### Fork

Crie uma cópia do repositório clicando no botão " Fork", com projeto associado à sua conta: clone-o e assim terá o projeto para testar ou implementar qualquer workflow.

### Integração automatizada

O objetivo entender o que deve ser automatizado numa integração contínua.

#### Criação de variáveis de ambiente

Variáveis de ambiente serão inseridas no código. Não é necessário conhecer a linguagem.

`database/db.go`:

```go
func ConectaComBancoDados() {
  stringDeConexao := "host=postgre user=root password=root dbname=root port=5432 sslmode=disable"
  DB, err = gorm.Open(postgres.Open(stringDeConexao))
  if err != nil {
    log.Panic("Erro ao conectar com banco de dados")
  }

  DB.AutoMigrate(&models.Aluno{})
}
```

A `stringDeConexao` há informações _hardcoded_, isto deve ser mudado se quisermos a portabilidade do código.

A integração contínua envolvem múltiplos ambientes, como por exemplo: desenvolvimento, testes e produção.
