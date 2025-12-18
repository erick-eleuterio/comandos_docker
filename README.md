# Documentação Simples e Completa de Docker

## 📌 Introdução

Docker é uma plataforma que permite empacotar, distribuir e executar aplicações dentro de **containers**. Containers são ambientes isolados, leves e portáveis que garantem que sua aplicação rode da mesma forma em qualquer lugar.

---

## 🧱 Conceitos Fundamentais

### 🔹 Imagem (Image)

* É o "pacote" com tudo que sua aplicação precisa: código, dependências, sistema mínimo.
* É somente leitura.
* Serve como base para criar containers.

### 🔹 Container

* É uma instância em execução de uma imagem.
* É mutável: você pode iniciar, parar, remover.
* Cada container é isolado dos outros.

### 🔹 Dockerfile

* Arquivo de instruções para construir imagens.
* Exemplo simples:

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "app.js"]
```

### 🔹 Docker Hub

* Repositório público onde você baixa e envia imagens.

---

## 📦 Comandos Essenciais - Imagens

### ▶️ Baixar uma imagem do Docker Hub

```bash
docker pull nome-da-imagem
```

Exemplo:
```bash
docker pull nginx
docker pull mysql:8.0
```

### ▶️ Criar uma imagem

```bash
docker build -t nome-da-imagem .
```

Com uma tag específica:
```bash
docker build -t meu-app:v1.0 .
```

### ▶️ Listar imagens

```bash
docker images
```

Ou:
```bash
docker image ls
```

### ▶️ Ver histórico de uma imagem

```bash
docker history nome-da-imagem
```

### ▶️ Renomear/criar tag de uma imagem

```bash
docker tag imagem-origem nome-novo:tag
```

Exemplo:
```bash
docker tag meu-app:latest meu-app:v1.0
```

### ▶️ Enviar imagem para Docker Hub

```bash
docker push usuario/nome-da-imagem:tag
```

Exemplo:
```bash
docker push erick/meu-app:v1.0
```

### ▶️ Salvar imagem em arquivo

```bash
docker save -o arquivo.tar nome-da-imagem
```

### ▶️ Carregar imagem de arquivo

```bash
docker load -i arquivo.tar
```

### ▶️ Remover imagem

```bash
docker rmi nome-ou-id
```

Forçar remoção:
```bash
docker rmi -f nome-ou-id
```

### ▶️ Remover imagens não utilizadas

```bash
docker image prune
```

Remover todas as imagens não usadas:
```bash
docker image prune -a
```

---

## 🚀 Containers

### ▶️ Rodar um container

```bash
docker run nome-da-imagem
```

Rodar em modo destacado (em background):
```bash
docker run -d nome-da-imagem
```

Rodar com nome personalizado:
```bash
docker run -d --name meu-container nome-da-imagem
```

Rodar mapeando portas:
```bash
docker run -d -p 8080:80 nginx
```
*Mapeia a porta 80 do container para a porta 8080 do host.*

Rodar com variáveis de ambiente:
```bash
docker run -d -e MYSQL_ROOT_PASSWORD=senha mysql
```

Rodar com volume:
```bash
docker run -d -v meu-volume:/app/data nome-da-imagem
```

Rodar interativo (para testar):
```bash
docker run -it ubuntu bash
```

### ▶️ Listar containers

**Rodando:**
```bash
docker ps
```

**Todos (inclui parados):**
```bash
docker ps -a
```

**Último container criado:**
```bash
docker ps -l
```

### ▶️ Iniciar container parado

```bash
docker start id-ou-nome
```

### ▶️ Reiniciar container

```bash
docker restart id-ou-nome
```

### ▶️ Parar container

```bash
docker stop id-ou-nome
```

Parar com timeout:
```bash
docker stop -t 30 id-ou-nome
```

### ▶️ Pausar/despausar container

Pausar temporariamente:
```bash
docker pause id-ou-nome
```

Continuar execução:
```bash
docker unpause id-ou-nome
```

### ▶️ Ver logs do container

```bash
docker logs id-ou-nome
```

Seguir logs em tempo real:
```bash
docker logs -f id-ou-nome
```

Ver últimas 100 linhas:
```bash
docker logs --tail 100 id-ou-nome
```

### ▶️ Executar comando dentro do container

```bash
docker exec id-ou-nome comando
```

Abrir terminal interativo:
```bash
docker exec -it id-ou-nome bash
```

Ou para imagens Alpine Linux:
```bash
docker exec -it id-ou-nome sh
```

### ▶️ Ver informações detalhadas do container

```bash
docker inspect id-ou-nome
```

Ver IP do container:
```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' id-ou-nome
```

### ▶️ Ver processos rodando no container

```bash
docker top id-ou-nome
```

### ▶️ Ver estatísticas de uso (CPU, memória)

Todos os containers:
```bash
docker stats
```

Container específico:
```bash
docker stats id-ou-nome
```

### ▶️ Copiar arquivos entre host e container

Do host para o container:
```bash
docker cp arquivo.txt id-ou-nome:/caminho/destino
```

Do container para o host:
```bash
docker cp id-ou-nome:/caminho/arquivo.txt ./
```

### ▶️ Conectar ao terminal do container

```bash
docker attach id-ou-nome
```

### ▶️ Remover container

```bash
docker rm id-ou-nome
```

### ▶️ Remover container em execução

```bash
docker rm -f id-ou-nome
```

### ▶️ Remover todos os containers parados

```bash
docker container prune
```

Sem confirmação:
```bash
docker container prune -f
```

---

## 🔗 Volumes (Guardar dados)

Volumes são usados para persistir dados fora do container. Quando o container é removido, os dados no volume permanecem.

### ▶️ Criar volume

```bash
docker volume create meu-volume
```

### ▶️ Listar volumes

```bash
docker volume ls
```

### ▶️ Ver detalhes do volume

```bash
docker volume inspect meu-volume
```

### ▶️ Rodar container usando volume

Volume nomeado:
```bash
docker run -v meu-volume:/app/data nome-da-imagem
```

Bind mount (pasta do host):
```bash
docker run -v /caminho/host:/app/data nome-da-imagem
```

No Windows:
```bash
docker run -v C:\pasta:/app/data nome-da-imagem
```

### ▶️ Remover volume

```bash
docker volume rm meu-volume
```

### ▶️ Remover volumes não utilizados

```bash
docker volume prune
```

---

## 🌐 Redes

Redes permitem que containers se comuniquem entre si de forma isolada e segura.

### ▶️ Listar redes

```bash
docker network ls
```

### ▶️ Criar rede

```bash
docker network create minha-rede
```

Criar rede com driver específico:
```bash
docker network create --driver bridge minha-rede
```

### ▶️ Ver detalhes da rede

```bash
docker network inspect minha-rede
```

### ▶️ Rodar container dentro da rede

```bash
docker run --network minha-rede nome-da-imagem
```

Com nome do container (para DNS interno):
```bash
docker run --network minha-rede --name api nome-da-imagem
```

### ▶️ Conectar container existente a uma rede

```bash
docker network connect minha-rede id-ou-nome
```

### ▶️ Desconectar container de uma rede

```bash
docker network disconnect minha-rede id-ou-nome
```

### ▶️ Remover rede

```bash
docker network rm minha-rede
```

### ▶️ Remover redes não utilizadas

```bash
docker network prune
```

---

## 🛠️ Docker Compose

Ferramenta para rodar vários containers juntos de forma organizada.

### ▶️ Exemplo de docker-compose.yml

```yaml
version: '3'
services:
  app:
    build: .
    container_name: meu-app
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=db
    volumes:
      - .:/app
    networks:
      - minha-rede
    depends_on:
      - db

  db:
    image: mysql:8.0
    container_name: mysql-db
    environment:
      - MYSQL_ROOT_PASSWORD=senha123
      - MYSQL_DATABASE=meubanco
    volumes:
      - db-data:/var/lib/mysql
    networks:
      - minha-rede

volumes:
  db-data:

networks:
  minha-rede:
```

### ▶️ Subir todos os serviços

```bash
docker compose up
```

Em background:
```bash
docker compose up -d
```

Forçar rebuild das imagens:
```bash
docker compose up --build
```

### ▶️ Parar todos os serviços

```bash
docker compose down
```

Parar e remover volumes:
```bash
docker compose down -v
```

### ▶️ Ver logs dos serviços

Todos os serviços:
```bash
docker compose logs
```

Seguir logs em tempo real:
```bash
docker compose logs -f
```

Serviço específico:
```bash
docker compose logs app
```

### ▶️ Listar serviços rodando

```bash
docker compose ps
```

### ▶️ Executar comando em um serviço

```bash
docker compose exec app bash
```

### ▶️ Reiniciar serviços

Todos:
```bash
docker compose restart
```

Serviço específico:
```bash
docker compose restart app
```

### ▶️ Parar serviços sem remover

```bash
docker compose stop
```

### ▶️ Iniciar serviços parados

```bash
docker compose start
```

### ▶️ Ver uso de recursos

```bash
docker compose top
```

### ▶️ Construir/reconstruir imagens

```bash
docker compose build
```

Sem usar cache:
```bash
docker compose build --no-cache
```

---

## 🧹 Comandos de Limpeza

### ▶️ Remover tudo que não está sendo usado

```bash
docker system prune
```

Incluir volumes:
```bash
docker system prune --volumes
```

Remover TUDO (cuidado!):
```bash
docker system prune -a
```

### ▶️ Ver espaço em disco usado pelo Docker

```bash
docker system df
```

Detalhado:
```bash
docker system df -v
```

### ▶️ Remover containers parados

```bash
docker container prune
```

### ▶️ Remover imagens não utilizadas

```bash
docker image prune
```

### ▶️ Remover volumes não utilizados

```bash
docker volume prune
```

### ▶️ Remover redes não utilizadas

```bash
docker network prune
```

---

## ⚙️ Configurações Avançadas

### ▶️ Limitar recursos do container

Limitar memória:
```bash
docker run -m 512m nome-da-imagem
```

Limitar CPU:
```bash
docker run --cpus="1.5" nome-da-imagem
```

### ▶️ Restart automático

```bash
docker run -d --restart unless-stopped nome-da-imagem
```

Opções de restart:
- `no` - Nunca reinicia (padrão)
- `on-failure` - Reinicia se falhar
- `always` - Sempre reinicia
- `unless-stopped` - Reinicia exceto se foi parado manualmente

### ▶️ Usar arquivo de variáveis de ambiente

Criar arquivo `.env`:
```
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
```

Usar no container:
```bash
docker run --env-file .env nome-da-imagem
```

### ▶️ Health check personalizado

No Dockerfile:
```dockerfile
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1
```

---

## 💡 Dicas Importantes

### ✅ Boas práticas

* Sempre use `--name` para nomear seus containers e facilitar o gerenciamento.
* Use Docker Compose para projetos com múltiplos serviços.
* Sempre pare containers antes de remover imagens.
* Use volumes para dados importantes que precisam persistir.
* Mantenha suas imagens pequenas usando imagens base Alpine quando possível.

### 🔍 Comandos úteis para debug

* `docker ps` - Ver o que está rodando
* `docker logs -f container` - Ver logs em tempo real
* `docker exec -it container bash` - Entrar no container
* `docker inspect container` - Ver todas as configurações
* `docker stats` - Monitorar uso de recursos

### ⚠️ Atenção

* `docker system prune -a` remove TUDO que não está em uso. Use com cuidado!
* Containers são efêmeros por natureza. Dados importantes devem estar em volumes.
* Sempre revise o `docker-compose.yml` antes de fazer `up` em produção.

---

## 📚 Recursos Adicionais

* [Documentação Oficial do Docker](https://docs.docker.com/)
* [Docker Hub](https://hub.docker.com/)
* [Docker Compose Documentation](https://docs.docker.com/compose/)
* [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

---

**✨ Documentação criada por Erick Eleutério**
