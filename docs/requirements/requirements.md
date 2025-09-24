# Documento de Requisitos

## 1. Requisitos Funcionais (RF)

| ID | Descrição |
| :--- | :--- |
| *RF01* | Cadastro e autenticação de usuários (administradores, voluntários, doadores, adotantes) |
| *RF02* | Gerenciamento de animais do abrigo (cadastro, edição, histórico de saúde, status de adoção) |
| *RF03* | Processo de adoção (solicitação, aprovação, acompanhamento pós-adoção) |
| *RF04* | Gestão de doações (financeiras, ração, medicamentos, registro de doadores) |
| *RF05* | Controle de voluntários (escala de atividades, registro de horas) |
| *RF06* | Controle de estoque (ração, medicamentos, itens de higiene) com alertas de nível crítico |
| *RF07* | Geração de relatórios e dashboard (métricas de adoção, doações, estoque crítico) |
| *RF08* | Comunicação via notificações (e-mail, SMS, push) para eventos importantes |

## 2. Requisitos Não-Funcionais (RNF)

| ID | Descrição |
| :--- | :--- |
| *RNF01* | Multiplataforma: Interface web responsiva e aplicativo móvel nativo para Android e iOS. |
| *RNF02* | Segurança: Autenticação via JWT e criptografia de dados sensíveis no banco de dados. |
| *RNF03* | Escalabilidade: Arquitetura baseada em microsserviços para permitir escalamento independente. |
| *RNF04* | Disponibilidade: O sistema deve suportar até 50 usuários simultâneos com uptime de 99.5%. |
| *RNF05* | Performance: Tempo de resposta inferior a 3 segundos para operações críticas. |
| *RNF06* | Integração: Sistema deve se integrar com gateways de pagamento (Pix, cartão de crédito). |

## 3. Regras de Negócio
- Apenas usuários com perfil de *Administrador* podem:
  - Aprovar ou reprovar solicitações de adoção.
  - Gerenciar (adicionar, editar, remover) itens do estoque crítico.
  - Visualizar todos os relatórios financeiros e de doações.
- *Voluntários* podem:
  - Atualizar o status de saúde e behavioral dos animais.
  - Registrar suas horas de trabalho.
- *Adotantes* podem:
  - Visualizar apenas animais disponíveis para adoção.
  - Preencher e enviar um formulário de solicitação de adoção para um animal.
- *Doadores* podem:
  - Visualizar um histórico de suas próprias doações.

## 4. Histórias de Usuário (Exemplos)

### Para Administradores
- *Como* administrador, *eu quero* aprovar solicitações de adoção *para* garantir que os animais vão para lares adequados.
- *Como* administrador, *eu quero* gerar um relatório de doações do mês *para* prestar contas aos parceiros.

### Para Voluntários
- *Como* voluntário, *eu quero* registrar a medicação administrada em um animal *para* manter seu histórico de saúde atualizado.

### Para Adotantes
- *Como* adotante, *eu quero* filtrar animais disponíveis por espécie e idade *para* encontrar um companheiro compatível com meu estilo de vida.

### Para Doadores
- *Como* doador, *eu quero* doar uma quantia em dinheiro via PIX *para* contribuir com os custos do abrigo.

## 5. Perfis de Usuários
1.  *Administrador:* Responsável pela gestão completa do sistema e pela supervisão de todas as operações.
2.  *Voluntário:* Auxilia nas atividades diárias do abrigo, como limpeza, cuidados com os animais e atendimento ao público.
3.  *Adotante:* Pessoa interessada em encontrar e adotar um animal do abrigo.
4.  *Doador:* Pessoa ou empresa interessada em fazer doações financeiras ou materiais ao abrigo.