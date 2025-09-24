# Especificação da API

## Autenticação e Autorização
A autenticação é feita via *JWT (JSON Web Token)*. Após login bem-sucedido, um token deve ser incluído no cabeçalho de todas as requisições subsequentes para endpoints protegidos:
Authorization: Bearer <seu_token_jwt_aqui>

## Endpoints Previstos

### Autenticação
| Método | Endpoint | Descrição | Autenticação |
| :--- | :--- | :--- | :--- |
| POST | /api/auth/login | Autentica um usuário e retorna um JWT. | Pública |

### Animais
| Método | Endpoint | Descrição | Autenticação |
| :--- | :--- | :--- | :--- |
| GET | /api/animals | Lista todos os animais, com filtros opcionais. | Pública |
| POST | /api/animals | Cria um novo registro de animal. | Admin |
| GET | /api/animals/{id} | Retorna os detalhes de um animal específico. | Pública |
| PUT | /api/animals/{id} | Atualiza os dados de um animal. | Admin/Voluntário |

### Adoções
| Método | Endpoint | Descrição | Autenticação |
| :--- | :--- | :--- | :--- |
| POST | /api/adoptions | Submete uma nova solicitação de adoção. | Adotante |
| GET | /api/adoptions | Lista todas as adoções (com filtros para admin). | Admin |
| PUT | /api/adoptions/{id} | Aprova ou reprova uma solicitação. | Admin |

### Doações
| Método | Endpoint | Descrição | Autenticação |
| :--- | :--- | :--- | :--- |
| POST | /api/donations | Registra uma nova doação. | Doador |
| GET | /api/donations/stats | Retorna métricas e estatísticas de doações. | Admin |

## Exemplos de Request e Response

### 1. POST /api/auth/login
*Request:*
http
POST /api/auth/login HTTP/1.1
Host: localhost:3000
Content-Type: application/json

{
  "email": "voluntario@abrigo.org",
  "password": "senhaSegura123"
}


*Response (Sucesso - 200 OK):*
http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": 123,
    "name": "Fulana de Tal",
    "email": "voluntario@abrigo.org",
    "role": "volunteer"
  }
}


### 2. GET /api/animals
*Request:*
http
GET /api/animals?species=Cachorro&status=Disponível HTTP/1.1
Host: localhost:3000


*Response (Sucesso - 200 OK):*
http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "name": "Rex",
    "species": "Cachorro",
    "breed": "Vira-lata",
    "age": 2,
    "health_status": "Saudável, vacinado",
    "adoption_status": "Disponível",
    "entry_date": "2024-01-15"
  }
]


### 3. POST /api/adoptions
*Request:*
http
POST /api/adoptions HTTP/1.1
Host: localhost:3000
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json

{
  "animal_id": 5,
  "adopter_message": "Tenho um quintal grande e amo animais."
}


*Response (Sucesso - 201 Created):*
http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 42,
  "animal_id": 5,
  "adopter_id": 123,
  "status": "Pendente",
  "request_date": "2024-09-19T10:30:00.000Z",
  "message": "Solicitação de adoção enviada com sucesso. Aguarde a aprovação."
}