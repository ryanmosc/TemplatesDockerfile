# 🐳 Docker Templates – Multi Language

Este repositório contém **templates de Dockerfile reutilizáveis**, organizados por **linguagem e cenário**, seguindo **boas práticas de mercado**.

O objetivo é acelerar o desenvolvimento, padronizar builds e facilitar estudos, projetos pessoais e uso profissional.

---

## 🎯 Objetivo do Projeto

* Criar **Dockerfiles genéricos e reutilizáveis**
* Separar templates por **linguagem e tipo de aplicação**
* Facilitar aprendizado prático de Docker
* Servir como **portfólio DevOps**

---

## 📁 Estrutura do Repositório

```text
docker-templates/
├── python/
│   └── Dockerfile
├── java-spring/
│   └── Dockerfile
├── node/
│   └── Dockerfile
├── php/
│   └── Dockerfile
├── frontend-static/
│   └── Dockerfile
├── frontend-spa/
│   └── Dockerfile
└── README.md
```

---

## 🐍 Python (Flask / FastAPI / Django)

**Cenário:** APIs, microserviços, workers

**Características:**

* Imagem leve (`python:slim`)
* Instala dependências via `requirements.txt`
* Logs em stdout

```bash
docker build -t python-app .
docker run -p 8000:8000 python-app
```

---

## ☕ Java (Spring Boot)

**Cenário:** APIs Spring Boot empacotadas em JAR

**Características:**

* Multi-stage build
* Maven para build
* JRE leve para runtime

```bash
docker build -t spring-app .
docker run -p 8080:8080 spring-app
```

---

## 🟢 Node.js (Express / NestJS)

**Cenário:** APIs Node.js

**Características:**

* Instalação otimizada com `npm ci`
* Imagem Alpine

```bash
docker build -t node-app .
docker run -p 3000:3000 node-app
```

---

## 🐘 PHP (Laravel / PHP Puro)

**Cenário:** Aplicações PHP rodando em Apache

**Características:**

* PHP 8.x
* Extensões PDO habilitadas

```bash
docker build -t php-app .
docker run -p 80:80 php-app
```

---

## 🌐 Frontend Estático (HTML / CSS / JS)

**Cenário:** Sites estáticos, landing pages

**Características:**

* Servido via Nginx
* Build simples e rápido

```bash
docker build -t static-site .
docker run -p 80:80 static-site
```

---

## ⚙️ Frontend SPA (React / Vue / Angular)

**Cenário:** Frontends modernos em produção

**Características:**

* Build com Node.js
* Servido via Nginx
* Multi-stage build

```bash
docker build -t frontend-spa .
docker run -p 80:80 frontend-spa
```

---

## 🧠 Boas Práticas Aplicadas

* Imagens leves
* Multi-stage builds quando necessário
* Separação de build e runtime
* Uso de variáveis de ambiente
* Templates fáceis de adaptar

---

## 🚀 Como Usar

1. Copie a pasta do template desejado
2. Ajuste o `Dockerfile` se necessário
3. Suba sua aplicação com Docker

```bash
docker build -t minha-app .
docker run minha-app
```

# 🧩 Docker Compose Curinga (Reutilizável)

Este `docker-compose.yml` foi pensado para ser **genérico**, **flexível** e **reutilizável** para a maioria dos projetos backend modernos.

Ele funciona como base para **Python, Node, Java, PHP** e aplicações que dependem de **PostgreSQL**.

---

## 📄 docker-compose.yml

```yaml
version: "3.9"

services:
  app:
    build: .
    container_name: app_container
    ports:
      - "${APP_PORT}:8000"
    env_file:
      - .env
    volumes:
      - .:/app
    depends_on:
      db:
        condition: service_healthy
    restart: always

  db:
    image: postgres:16
    container_name: postgres_container
    env_file:
      - .env
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER}"]
      interval: 10s
      timeout: 5s
      retries: 5
    restart: always

volumes:
  postgres_data:
```

---

## 📄 .env (exemplo)

```env
# Aplicação
APP_PORT=8000

# Banco de dados
POSTGRES_DB=appdb
POSTGRES_USER=appuser
POSTGRES_PASSWORD=apppass
DB_HOST=db
```

---

## 🧠 Por que esse compose é "curinga"

* Serve para **qualquer backend** que exponha uma porta
* Banco desacoplado da aplicação
* Variáveis via `.env`
* Healthcheck garante que o app só suba após o banco
* Volume persistente para dados
* Volume de código para desenvolvimento

---

## 🚀 Como reutilizar em outro projeto

1. Copie `docker-compose.yml`
2. Copie `.env.example` → `.env`
3. Ajuste:

   * `APP_PORT`
   * Porta interna da aplicação (8000)
   * Imagem do banco, se necessário

---

## 🔄 Ajustes comuns por linguagem

### Python

* Porta interna: `8000`
* Comando definido no Dockerfile

### Node.js

* Porta interna: `3000`
* Ajustar `ports` para `${APP_PORT}:3000`

### Java (Spring Boot)

* Porta interna: `8080`
* Ajustar `ports` para `${APP_PORT}:8080`

### PHP

* Porta interna: `80`
* Remover volume de código em produção

---

## ⚠️ Observações Importantes

* Ideal para **desenvolvimento e CI**
* Para produção:

  * remover volume de código
  * usar secrets
  * ajustar restart policy

---

## 🎯 Uso recomendado

* Projetos pessoais
* Estudos DevOps
* CI/CD com Docker Compose
* Portfólio

---

Esse compose serve como **base sólida**, não como regra fixa.
Adapte conforme o cenário.


---

---

## 👤 Autor: Ryan Moscardini

Projeto criado para **estudo prático de Docker e DevOps**, focado em padronização e boas práticas.

---

⭐ Se este repositório te ajudou, considere deixar uma estrela.
