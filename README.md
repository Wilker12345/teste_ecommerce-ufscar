# E-Commerce UFSCar

Sistema web de gestão de e-commerce (Python + Django + PostgreSQL).
Projeto da disciplina de Gerenciamento de Projetos e Qualidade de Software.

## Como rodar o projeto (para quem acabou de clonar)

Pré-requisitos: Python 3.10 ou superior, Git e um PostgreSQL (local ou via Docker).

```bash
git clone <URL-DO-REPOSITORIO>
cd ecommerce-ufscar

# 1. Ambiente virtual
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # Linux / macOS

# 2. Dependências
pip install -r requirements.txt

# 3. Configuração local
copy .env.example .env         # Windows (Linux/macOS: cp .env.example .env)
# Abra o .env e defina SECRET_KEY e DB_PASSWORD

# 4. Banco de dados (escolha UMA opção)
docker compose up -d           # opção A: PostgreSQL em container
# opção B: use um PostgreSQL instalado e crie o banco "loja"

# 5. Criar as tabelas e rodar
python manage.py migrate
python manage.py runserver
```

Acesse http://127.0.0.1:8000.

Se a porta 5432 já estiver em uso (por exemplo, por um PostgreSQL instalado),
troque `DB_PORT` no `.env` (por exemplo, para 5433) antes do `docker compose up`.

## Testes

```bash
python manage.py test
coverage run manage.py test && coverage report   # com cobertura
```

Meta de qualidade do plano: cobertura mínima de 70% nos módulos desenvolvidos.

## Fluxo de trabalho em equipe

- Ninguém faz commit direto na `main`.
- Crie uma branch por tarefa: `git checkout -b catalogo-cadastro-produtos`.
- Abra um Pull Request; outro integrante revisa e aprova antes do merge.
- Mantenha os testes passando (o GitHub Actions roda a cada push e PR).
- Nunca versione o `.env` nem senhas. Se mudar dependências, atualize o
  `requirements.txt` com `pip freeze > requirements.txt`.

## Estrutura

Um app Django por módulo da EAP: `catalogo`, `carrinho`, `pedidos`,
`pagamentos`, `clientes`, `relatorios`, `marketing`.
