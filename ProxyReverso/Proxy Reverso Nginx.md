


# 🚀 Guia Prático: Proxy Reverso com Nginx Proxy Manager (NPM)

Este documento centraliza as anotações para configurar um ambiente Docker onde o Nginx Proxy Manager gerencia o tráfego de múltiplas aplicações de forma automatizada.

---

## 1. Conceito Chave
Para que o Proxy funcione, o container do **NPM** e os **containers das aplicações** devem compartilhar a mesma rede Docker. O Proxy será a única "porta de entrada" (expondo 80 e 443), distribuindo o tráfego internamente para os outros containers.

## 2. Preparação da Rede
O primeiro passo é criar a rede que servirá de ponte. Rode este comando no terminal:

```bash
docker network create proxy-network
```

---

## 3. Configuração do Nginx Proxy Manager
Crie um diretório para o proxy e salve o arquivo `docker-compose.yml` abaixo:

```yaml
version: '3.8'

services:
  nginx-proxy:
    image: jc21/nginx-proxy-manager:latest
    container_name: nginx-proxy-manager
    restart: unless-stopped
    environment:
      TZ: 'America/Sao_Paulo'
    ports:
      - "80:80"   # Tráfego HTTP
      - "443:443" # Tráfego HTTPS
      - "81:81"   # Painel Administrativo (Interface Web)
    volumes:
      - ./npm/data:/data
      - ./npm/letsencrypt:/etc/letsencrypt
    networks:
      - proxy-network

networks:
  proxy-network:
    external: true # Indica que a rede já foi criada manualmente
```

---

## 4. Configuração da Aplicação (Exemplo)
Abaixo, um exemplo de como configurar sua aplicação para ser "enxergada" pelo proxy. 
> **Atenção:** Note que a aplicação não precisa expor portas (`ports:`) para o host, apenas estar na rede do proxy.

```yaml
version: '3.8'

services:
  api:
    image: ryanmosc/backend-vagas-fatec:1.0.3
    container_name: backend-vagas-fatec
    volumes:
      - uploads-curriculos:/app/uploads
    networks:
      - backendfatec  # Rede privada para comunicação API <-> DB
      - proxy-network # Rede para o Proxy encontrar esta API
    restart: unless-stopped

  frontend:
    image: ryanmosc/frontend-vagas-fatec:1.0.7
    container_name: frontend-vagas-fatec
    networks:
      - backendfatec
      - proxy-network
    restart: unless-stopped

volumes:
  uploads-curriculos:

networks:
  backendfatec:
    driver: bridge
  proxy-network:
    external: true
```

---

## 5. Configuração na Interface Web (NPM)
Após subir os containers (`docker-compose up -d`), acesse `http://seu-ip:81` e siga estes passos:

1.  Vá em **Proxy Hosts** -> **Add Proxy Host**.
2.  **Domain Names:** Digite seu domínio (ex: `meusite.com.br`) e aperte Enter.
3.  **Scheme:** Mantenha `http`.
4.  **Forward Hostname / IP:** Use o **nome do container** definido no compose (ex: `frontend-vagas-fatec`).
5.  **Forward Port:** A porta interna que o container usa (geralmente `80`, `3000` ou `8080`).
6.  **SSL:** Na aba SSL, selecione "Request a new SSL Certificate" para gerar o certificado Let's Encrypt automaticamente.

---
*Notas: O login padrão do NPM costuma ser `admin@example.com` com a senha `changeme`.*
```

Basta copiar o conteúdo acima! Alguma dúvida sobre como integrar um banco de dados nesse fluxo?