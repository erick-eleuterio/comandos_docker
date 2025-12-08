# Documentação Simples e Completa de Docker

## 📌 Introdução

Docker é uma plataforma que permite empacotar, distribuir e executar aplicações dentro de **containers**. Containers são ambientes isolados, leves e portáveis que garantem que sua aplicação rode da mesma forma em qualquer lugar.

---

## 🧱 Conceitos Fundamentais

### **🔹 Imagem (Image)**

* É o "pacote" com tudo que sua aplicação precisa: código, dependências, sistema mínimo.
* É somente leitura.
* Serve como base para criar containers.

### **🔹 Container**

* É uma instância em execução de uma imagem.
* É mutável: você pode iniciar, parar, remover.
* Cada container é isolado dos outros.

### **🔹 Dockerfile**

* Arquivo de instruções para construir imagens.
* Exemplo simples:

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "app.js"]
```

### **🔹 Docker Hub**

* Repositório público onde você baixa e envia imagens.

---

## 📦 Comandos Essenciais

### **▶️ Criar uma imagem**

```bash
docker build -t nome-da-imagem .
```

### **▶️ Listar imagens**

```bash
docker images
```

### **▶️ Remover imagem**

```bash
docker rmi nome-ou-id
```

Se ela estiver sendo usada por um container:

```bash
docker rm -f id-do-container
```

---

## 🚀 Containers

### **▶️ Rodar um container**

```bash
docker run nome-da-imagem
```

Rodar em modo destacado (em background):

```bash
docker run -d nome-da-imagem
```

### **▶️ Listar containers**

**Rodando:**

```bash
docker ps
```

**Todos (inclui parados):**

```bash
docker ps -a
```

### **▶️ Parar container**

```bash
docker stop id-ou-nome
```

### **▶️ Remover container**

```bash
docker rm id-ou-nome
```

### **▶️ Remover container em execução**

```bash
docker rm -f id-ou-nome
```

---

## 🔗 Volumes (Guardar dados)

Usado para persistir dados fora do container.

Criar volume:

```bash
docker volume create meu-volume
```

Rodar container usando volume:

```bash
docker run -v meu-volume:/app/data nome-da-imagem
```

Listar volumes:

```bash
docker volume ls
```

---

## 🌐 Redes

Listar redes:

```bash
docker network ls
```

Criar rede:

```bash
docker network create minha-rede
```

Rodar container dentro da rede:

```bash
docker run --network minha-rede nome-da-imagem
```

---

## 🛠️ Docker Compose

Ferramenta para rodar vários containers juntos.

Exemplo `docker-compose.yml`:

```yaml
version: '3'
services:
  app:
    image: node:18
    container_name: meu-app
    volumes:
      - .:/app
    ports:
      - "3000:3000"
    command: node app.js
```

Rodar tudo:

```bash
docker compose up
```

Parar:

```bash
docker compose down
```

---

## 💡 Dicas importantes

* Sempre pare containers antes de remover imagens.
* Use `--name` para evitar precisar digitar IDs enormes.
* Use Docker Compose para projetos reais.
* Sempre confira o `docker ps` para saber o que está rodando.

---


