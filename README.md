# Django API Crud Tasks

API REST simples para gerenciamento de tarefas, construída com Django e Django REST Framework para fins de estudo.

## Visão geral

O projeto expõe um CRUD completo para tarefas em `/api/tasks/`, usando SQLite como banco local e o roteador padrão do DRF para listar, criar, editar e remover registros.

Cada tarefa possui os seguintes campos:

- `id`: identificador gerado automaticamente
- `title`: titulo da tarefa
- `description`: descricao opcional
- `done`: status de conclusao
- `created_at`: data de criacao

## Stack

- Python 3.12+
- Django 6.0.3
- Django REST Framework 3.16.1
- SQLite

## Estrutura

```text
django-api-crud-tasks/
|-- config/
|-- tasks/
|-- manage.py
|-- requirements.txt
`-- README.md
```

## Como executar

### 1. Criar e ativar o ambiente virtual

No PowerShell:

```powershell
python -m venv venv
.\venv\Scripts\activate
```

### 2. Instalar dependencias

```powershell
pip install -r requirements.txt
```

### 3. Aplicar migracoes

```powershell
python manage.py migrate
```

### 4. Iniciar o servidor

```powershell
python manage.py runserver
```

Aplicacao disponivel em `http://127.0.0.1:8000/`.

## Endpoints

Base da API: `http://127.0.0.1:8000/api/tasks/`

| Metodo     | Rota                 | Descricao                     |
| ---------- | -------------------- | ----------------------------- |
| `GET`    | `/api/tasks/`      | Lista todas as tarefas        |
| `POST`   | `/api/tasks/`      | Cria uma nova tarefa          |
| `GET`    | `/api/tasks/{id}/` | Retorna uma tarefa especifica |
| `PUT`    | `/api/tasks/{id}/` | Atualiza todos os campos      |
| `PATCH`  | `/api/tasks/{id}/` | Atualiza parcialmente         |
| `DELETE` | `/api/tasks/{id}/` | Remove a tarefa               |

Autenticacao do navegador da API do DRF:

- `http://127.0.0.1:8000/api-auth/`

## Exemplos de uso

### Criar tarefa

```bash
curl -X POST http://127.0.0.1:8000/api/tasks/ \
  -H "Content-Type: application/json" \
  -d "{\"title\":\"Estudar Django\",\"description\":\"Revisar models e views\",\"done\":false}"
```

### Listar tarefas

```bash
curl http://127.0.0.1:8000/api/tasks/
```

### Atualizar status

```bash
curl -X PATCH http://127.0.0.1:8000/api/tasks/1/ \
  -H "Content-Type: application/json" \
  -d "{\"done\":true}"
```

### Remover tarefa

```bash
curl -X DELETE http://127.0.0.1:8000/api/tasks/1/
```

## Modelo de resposta

```json
{
  "id": 1,
  "title": "Estudar Django",
  "description": "Revisar models e views",
  "done": false,
  "created_at": "2026-03-11T12:00:00Z"
}
```

## Desenvolvimento

Com o ambiente virtual ativado, estas checagens sao as mais uteis:

```powershell
python manage.py check
python manage.py makemigrations
python manage.py migrate
```

## Observacoes

- O projeto usa SQLite, entao nao exige configuracao extra para rodar localmente.
- O arquivo `db.sqlite3` deve ser tratado como artefato local de desenvolvimento.
- O diretorio `venv/` e arquivos `__pycache__/` nao devem ser versionados.
