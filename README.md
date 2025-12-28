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

---


---

## 👤 Autor: Ryan Moscardini

Projeto criado para **estudo prático de Docker e DevOps**, focado em padronização e boas práticas.

---

⭐ Se este repositório te ajudou, considere deixar uma estrela.
