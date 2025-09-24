# Documentação da Arquitetura

## Descrição da Arquitetura
A arquitetura do sistema será do tipo *cliente-servidor* com separação clara entre frontend e backend, seguindo princípios de *API First. O backend será estruturado em **microsserviços* para isolamento de falhas e melhor escalabilidade. A comunicação entre frontend e backend ocorrerá exclusivamente via APIs RESTful.

## Componentes do Sistema
1.  *Clientes (Frontend):*
    -   *Aplicação Web:* Desenvolvida em React.js, será a principal ferramenta de gestão para administradores e voluntários dentro do abrigo.
    -   *Aplicativo Mobile:* Desenvolvido em React Native, voltado para adotantes e doadores, facilitando a busca por animais e o processo de doação.

2.  *Backend (API Gateway e Microsserviços):*
    -   *API Gateway:* Ponto único de entrada para todas as requisições. Responsável por rotear requests, autenticação (JWT) e rate limiting.
    -   *Serviço de Autenticação:* Microsserviço responsável pelo login, registro e gestão de tokens JWT.
    -   *Serviço de Gestão de Animais:* Gerencia todo o CRUD de animais, seu histórico de saúde e status.
    -   *Serviço de Adoções:* Controla o fluxo de solicitação, aprovação e acompanhamento de adoções.
    -   *Serviço de Doações e Estoque:* Gerencia doações financeiras, materiais e o controle de inventário.

3.  *Banco de Dados:*
    -   *PostgreSQL:* Banco de dados relacional principal, armazenando a maioria dos dados estruturados (usuários, animais, adoções).
    -   *Firebase Firestore:* Banco NoSQL utilizado para armazenar dados de notificações push e logs em tempo real.

4.  *Serviços Externos:*
    -   *Gateway de Pagamento:* (Ex: Asaas, Mercado Pago) para processar doações financeiras via Pix e cartão.
    -   *Serviço de E-mail/SMS:* (Ex: SendGrid, Twilio) para envio de notificações transacionais.

## Padrões Arquiteturais Utilizados
-   *Microsserviços:* Para dividir a aplicação em serviços independentes e com responsabilidades únicas.
-   *REST:* Para a construção das APIs, garantindo statelessness e uma interface uniforme.
-   *JWT (JSON Web Tokens):* Para autenticação stateless e segura.

## Diagrama de Arquitetura
O diagrama abaixo ilustra a interação entre os componentes:
![Diagrama de Arquitetura](../assets/diagrama-arquitetura.jpeg)


## Decisões Técnicas e Justificativas
-   *React.js + React Native:* Escolhidos para maximizar a reutilização de código e conhecimento entre as equipes de web e mobile, acelerando o desenvolvimento.
-   *Node.js (Express):* Optado pela vasta ecosystem, performance para I/O e simplicidade no desenvolvimento de APIs.
-   *PostgreSQL:* Selecionado por ser um banco SQL robusto, open-source e com suporte avançado a tipos de dados JSON, ideal para modelos de dados complexos e relacionais.
-   *Arquitetura de Microsserviços:* Adotada para permitir que times diferentes desenvolvam e implantem serviços independentemente, além de escalar componentes específicos sob carga.