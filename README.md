# 📊 Coletor de Métricas e Observabilidade

Stack completa de observabilidade e monitoramento de infraestrutura e serviços utilizando **Prometheus** para coleta e armazenamento de séries temporais e **Grafana** para visualização e criação de dashboards, orquestrados via **Docker Compose**.

---

## 🚀 Funcionalidades

- **Coleta de Métricas (Prometheus):**
  - Configuração pré-definida para scraping contínuo de métricas.
  - Armazenamento em série temporal otimizado.
  - Interface nativa para execução de queries PromQL e inspeção de targets.
- **Visualização & Dashboards (Grafana):**
  - Painéis interativos e personalizáveis para métricas de sistema, containers e aplicações.
  - Persistência de dados através de Docker Volume nomeado (`grafana-storage`).
  - Suporte a alertas e múltiplos data sources.
- **Orquestração Descomplicada:**
  - Inicialização de toda a stack com um único comando Docker Compose.
  - Rede isolada para comunicação segura entre os containers.

---

## 🛠️ Tecnologias Utilizadas

- **Time-Series Database / Métricas:** [Prometheus](https://prometheus.io/) (`prom/prometheus`)
- **Visualização & Analytics:** [Grafana](https://grafana.com/) (`grafana/grafana:latest`)
- **Orquestração e Containers:** Docker & Docker Compose

---

## 📂 Estrutura do Repositório

```text
Coletor-Metricas-observability/
├── database/
│   └── prometheus/
│       └── prometheus.yml       # Configuração global de scraping e targets do Prometheus
├── grafana_prometheus.yml       # Manifesto Docker Compose da stack
├── .gitignore                   # Arquivos ignorados pelo Git
└── README.md                    # Documentação do projeto
```

---

## ⚙️ Como Executar

### Pré-requisitos
- [Docker](https://docs.docker.com/get-docker/) instalado
- [Docker Compose](https://docs.docker.com/compose/) instalado (ou Docker CLI v2+)
- [Git](https://git-scm.com/)

---

### Passo a Passo

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/igorpaiva26/Coletor-Metricas-observability.git
   cd Coletor-Metricas-observability
   ```

2. **Suba os serviços com Docker Compose:**
   ```bash
   docker compose -f grafana_prometheus.yml up -d
   ```
   *(Em versões mais antigas do Docker, utilize: `docker-compose -f grafana_prometheus.yml up -d`)*

3. **Verifique se os containers estão em execução:**
   ```bash
   docker compose -f grafana_prometheus.yml ps
   ```

---

## 🌐 Acesso aos Serviços

| Serviço | Porta | URL de Acesso | Credenciais Padrão |
|---|---|---|---|
| **Grafana** | `3000` | [http://localhost:3000](http://localhost:3000) | Usuário: `admin` | Senha: `admin` |
| **Prometheus** | `9090` | [http://localhost:9090](http://localhost:9090) | Não requer autenticação |

---

## 📈 Conectando o Prometheus no Grafana

1. Acesse o Grafana em **[http://localhost:3000](http://localhost:3000)** e faça login com `admin` / `admin`.
2. No menu lateral, acesse **Connections** > **Data Sources** > **Add data source**.
3. Selecione **Prometheus**.
4. No campo **Prometheus server URL**, insira o endereço da rede interna do Docker:
   ```text
   http://prometheus:9090
   ```
5. Role até o final da página e clique em **Save & Test**. Uma mensagem de confirmação verde indicará o sucesso da integração.
6. Agora você já pode criar dashboards ou importar painéis prontos da comunidade (ex: Node Exporter ID 1860).

---

## 🛑 Parando a Stack

Para interromper a execução dos containers mantendo os dados salvos:
```bash
docker compose -f grafana_prometheus.yml down
```

Para remover os containers e também os volumes de dados do Grafana:
```bash
docker compose -f grafana_prometheus.yml down -v
```

---

## 👤 Autor

Desenvolvido por **[Igor Paiva](https://github.com/igorpaiva26)**.
