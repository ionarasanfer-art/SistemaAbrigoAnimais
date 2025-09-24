# Modelo de Dados

## Descrição das Entidades e Relacionamentos
O modelo de dados é relacional e foi projetado para refletir as entidades principais do negócio e seus relacionamentos.

-   *usuarios:* Armazena os dados de todos os usuários do sistema (administradores, voluntários, adotantes, doadores). A discriminação do tipo é feita pelo campo tipo.
-   *animais:* Contém informações sobre cada animal abrigado.
-   *adocoes:* Registra cada processo de adoção, vinculando um animal a um usuário adotante.
-   *doacoes:* Armazena registros de doações, sejam financeiras ou materiais.
-   *registros_medicos:* Mantém um histórico de vacinas, medicamentos e tratamentos de cada animal.

## Diagrama Entidade-Relacionamento (ER)
O diagrama abaixo representa visualmente as entidades, seus atributos e relacionamentos.

![Modelo ER](../assets/diagrama-modelo-er.jpeg)

## Dicionário de Dados

### Tabela: usuarios
| Atributo | Tipo | Descrição | Restrições |
| :--- | :--- | :--- | :--- |
| id | INTEGER | Identificador único do usuário. | PRIMARY KEY |
| nome | VARCHAR(100) | Nome completo do usuário. | NOT NULL |
| email | VARCHAR(255) | E-mail para login e comunicação. | UNIQUE, NOT NULL |
| senha_criptografada | VARCHAR(255) | Hash da senha do usuário. | NOT NULL |
| tipo | VARCHAR(50) | Perfil do usuário (admin, voluntario, adotante, doador). | NOT NULL |
| telefone | VARCHAR(20) | Número de telefone para contato. |  |
| data_criacao | TIMESTAMP | Data e hora de criação do registro. | DEFAULT CURRENT_TIMESTAMP |

### Tabela: animais
| Atributo | Tipo | Descrição | Restrições |
| :--- | :--- | :--- | :--- |
| id | INTEGER | Identificador único do animal. | PRIMARY KEY |
| nome | VARCHAR(100) | Nome do animal. | NOT NULL |
| especie | VARCHAR(50) | Espécie (ex: Cachorro, Gato). | NOT NULL |
| raca | VARCHAR(100) | Raça do animal. |  |
| idade | INTEGER | Idade aproximada em anos. |  |
| status_saude | TEXT | Descrição do estado de saúde atual. |  |
| status_adoção | VARCHAR(20) | Status atual (Disponível, Adotado, Em Processo). | DEFAULT 'Disponível' |
| data_entrada | DATE | Data de entrada no abrigo. | NOT NULL |

### Tabela: adocoes
| Atributo | Tipo | Descrição | Restrições |
| :--- | :--- | :--- | :--- |
| id | INTEGER | Identificador único do processo de adoção. | PRIMARY KEY |
| id_animal | INTEGER | ID do animal sendo adotado. | FOREIGN KEY REFERENCES animais(id) |
| id_adotante | INTEGER | ID do usuário solicitante da adoção. | FOREIGN KEY REFERENCES usuarios(id) |
| status | VARCHAR(20) | Status da solicitação (Pendente, Aprovada, Rejeitada). | DEFAULT 'Pendente' |
| data_solicitacao | TIMESTAMP | Data e hora da solicitação. | DEFAULT CURRENT_TIMESTAMP |
| data_aprovacao | TIMESTAMP | Data e hora de aprovação/rejeição. |  |
| observacoes_administrador | TEXT | Observações do administrador sobre a adoção. |  |

### Tabela: doacoes
| Atributo | Tipo | Descrição | Restrições |
| :--- | :--- | :--- | :--- |
| id | INTEGER | Identificador único da doação. | PRIMARY KEY |
| id_doador | INTEGER | ID do usuário que realizou a doação. | FOREIGN KEY REFERENCES usuarios(id) |
| tipo | VARCHAR(50) | Tipo de doação (financeira, ração, medicamento). | NOT NULL |
| valor | VARCHAR(255) | Valor em R$ (se financeira) ou descrição do item doado. | NOT NULL |
| data | TIMESTAMP | Data e hora do registro da doação. | DEFAULT CURRENT_TIMESTAMP |

### Tabela: registros_medicos
| Atributo | Tipo | Descrição | Restrições |
| :--- | :--- | :--- | :--- |
| id | INTEGER | Identificador único do registro médico. | PRIMARY KEY |
| id_animal | INTEGER | ID do animal que recebeu o procedimento. | FOREIGN KEY REFERENCES animais(id) |
| procedimento | VARCHAR(255) | Nome do procedimento (ex: Vacina V10, Aplicação de Antipulgas). | NOT NULL |
| data | DATE | Data em que o procedimento foi realizado. | NOT NULL |
| observacoes | TEXT | Observações adicionais sobre o procedimento. |  |