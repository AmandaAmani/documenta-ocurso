## Boas vindas à documentação de API da ZapSign!

### Nossa API é projetada para ser simples e intuitiva, permitindo que você integre a ZapSign rapidamente em suas aplicações.

A ZapSign é uma plataforma de assinatura eletrônica de documentos que cumpre os requisitos da Medida Provisória 2.200-2/2001, garantindo autenticidade, integridade e não repúdio. Assim, todas as assinaturas realizadas através da ZapSign possuem validade jurídica.

### Antes de começar

- [Registre-se](https://app.zapsign.com.br/acesso/criar-conta) ou [faça login na ZapSign](https://app.zapsign.com.br/acesso/entrar) para obter seu API token.
- Sempre configure Api token no header de Autorização de todas as suas chamadas.

## E como obter meu API token?

Dentro da sua conta ZapSign, clique em **Configurações > Integrações > API ZAPSIGN**. Depois, copie seu token e configure na sua ferramenta.  

![chrome-capture-2024-7-25 (2)](https://github.com/user-attachments/assets/eb777fa6-f08c-4315-af5b-14a8212a271f)

Trabalhamos com uma API REST, que utiliza os métodos GET e POST. Lemos tudo em JSON e nossas respostas também são em JSON.

---

#### Ambientes

A ZapSign oferece dois ambientes para utilização da API. Se você ainda não realizou nenhuma integração com a ZapSign, recomendamos que você inicie pelo ambiente de testes (sandbox) para evitar cobranças indevidas. 

| Ambiente | Endpoint | Validade Jurídica |
| -------- | -------- | ----------------- |
| Sandbox  | https://sandbox.api.zapsign.com.br | Não possui validade jurídica |
| Produção | https://api.zapsign.com.br | Possui validade jurídica |

## Integração com Clientes para API: Postman e Insomnia

Postman e Insomnia são ferramentas que facilitam o desenvolvimento, teste e documentação de APIs. Nós da ZapSign deixamos todas as bibliotecas de requisições prontas para ambas as ferramentas.

[POSTMAN WORKSPACE](https://elements.getpostman.com/redirect?entityId=27495556-787b914f-ebeb-426a-9808-7fb0bd0d47fd&entityType=collection)

Após abrir o link, selecione o ambiente que você gostaria de testar, disponível no canto superior direito, e crie um fork para acessar todos os endpoints dentro do seu próprio WorkSpace.

![image](https://github.com/user-attachments/assets/6623593d-9698-40ed-8107-206e6ed76b26)

Com o Postman configurado, você já pode utilizar todos os endpoints. A única variável obrigatória é a [api_token](https://app.zapsign.com.br/conta/configuracoes/integration?tab=api-zapsign), seu token de autenticação. Todas as outras podem ser preenchidas conforme sua necessidade.

Para o Insomnia, deixamos todos os endpoints preparados neste arquivo:

[Biblioteca Insomnia](https://3085168645-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4noMoX5ZGb2-RhWjjf-887967055%2Fuploads%2Fx7qCxGPFotUx362LKpvF%2FInsomnia_2023-03-27.json?alt=media&token=92133638-2480-439e-9e9c-eab3727e72f5)


## Autenticação

Se autenticar na ZapSign é muito simples! Atualmente, fornecemos duas opções para autenticação em nossa API pública: Token estático e JWT.

### Token estático

É a autenticação utilizando o [api_token](https://app.zapsign.com.br/conta/configuracoes/integration?tab=api-zapsign) da sua conta. Insira seu token no header "Authorization" da requisição, com o prefixo "Bearer ". 

Por exemplo:

```json
'headers': {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer [SEUAPI_TOKEN]'
}
```

### Atenção:

Se você tentar acessar algum endpoint sem inserir o header "Authorization" ou inserir um token inválido, você receberá uma resposta com status 403 (Não Autorizado).

Todos os endpoints da nossa API possuem uma barra ao final. Assim, o ponto de interrogação (?) deve seguir após a última barra (/):

- Correto: `https://api.zapsign.com.br/api/v1/docs/`
- Errado: `https://api.zapsign.com.br/api/v1/docs`


# Autenticação na API da ZapSign com JWT

Os JSON Web Tokens (JWT) são uma forma eficaz e segura de autenticação entre entidades distintas. Ao utilizar o fluxo de autenticação baseado em JWT, você garante uma maior segurança durante o desenvolvimento da sua aplicação de forma simples e eficiente.

## Como Funciona o Fluxo de Autenticação JWT

O fluxo baseado em JWT funciona através de dois tipos de tokens fundamentais:

1. **Token de Acesso**
2. **Token de Atualização**

### 1. Obter o Token de Acesso

O token de acesso é utilizado para se autenticar com a API da ZapSign. Ele está associado ao seu usuário e à organização especificada ao gerar o token e possui um tempo de expiração de 1 hora.

#### Passo a Passo:

1. Chame o endpoint `Obter token de acesso` com as credenciais do seu usuário ZapSign. Você precisará do ID da sua organização. Para isso, navegue até **Configurações>Integrações>API ZAPSIGN** [ou utilize este atalho](https://app.zapsign.com.br/conta/configuracoes/integration?tab=api-zapsign)

   **Endpoint:**
   ```
   POST https://api.zapsign.com.br/api/v1/auth/token/{{id_da_organização}}/
   ```

   **Request Body:**
   ```json
   {
       "username": "seu_email@dominio.com",
       "password": "sua_senha"
   }
   ```

   **Respostas Possíveis:**
   - `200: OK` - Autenticação realizada com sucesso
   - `401: Unauthorized` - Credenciais inválidas
   - `400: Bad Request` - Tentativas de login excedidas

   **Exemplo de Resposta com Sucesso:**
   ```json
   {
       "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTcxMDE3ODM0NCwianRpIjoiYjhmZjMwNDJmNjRkNDJmM2FlMzczZmRiNDQ3YTQ2NGEiLCJ1c2Vyb",
       "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
   }
   ```

2. Utilize o token de acesso nos headers de suas requisições para se autenticar nos endpoints da ZapSign.

   **Exemplo de Header:**
   ```json
   'headers': {
       'Content-Type': 'application/json',
       'Authorization': 'Bearer seu_token_de_acesso'
   }
   ```


> ℹ️ <strong>Importante:</strong> Neste chamada, você receberá o token de acesso e o token de atualização (refresh), que será utilizado toda vez que o token de acesso expirar.


### 2. Atualizando o Token de Acesso

O token de atualização serve para renovar o seu token de acesso quando este expirar (após 1 hora). O token de atualização tem um tempo de expiração de 1 dia.

#### Passo a Passo:

1. Quando o seu token de acesso expirar, utilize o token de atualização para obter um novo token de acesso.

   **Endpoint:**
   ```
   POST https://api.zapsign.com.br/api/v1/auth/token-refresh/
   ```

   **Request Body:**
   ```json
   {
       "refresh": "seu_token_de_atualização"
   }
   ```

   **Respostas Possíveis:**
   - `200: OK` - Atualização realizada com sucesso
   - `401: Unauthorized` - Token inválido

   **Exemplo de Resposta com Sucesso:**
   ```json
   {
       "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
   }
   ```
# Versionamento da API

Estamos constantemente adicionando recursos e melhorias à nossa API. No entanto, garantimos que seu aplicativo não parará de funcionar devido a alterações que fizermos. Se fizermos uma alteração significativa em um endpoint, lançaremos uma nova versão da API. Até o momento, não houve necessidade de mudanças desse tipo, portanto, continuamos na v1.

**Versão atual da API:** v1

Consideramos as seguintes alterações como compatíveis com versões anteriores:

- Adicionar novos endpoints na API.
- Adicionar novos parâmetros opcionais nas requisições.
- Tornar um parâmetro obrigatório da requisição opcional.
- Adicionar novas propriedades às respostas existentes da API.
- Adicionar novos eventos a webhooks (seu endpoint de webhook deve lidar com tipos de eventos desconhecidos, por exemplo, ignorando-os e retornando status 200).

Sempre que lançarmos novidades, enviaremos um e-mail de notificação.

# Políticas de Rate Limit

### Limite Geral e Aplicação
Para todos os endpoints públicos da aplicação, o rate limit é definido como 500 requisições por minuto. Este limite é aplicado por IP ou por token de autenticação válido, garantindo que cada entidade (IP ou token) tenha uma cota justa de uso.

### Funcionamento do Rate Limit
- **Limite de Requisições:** Cada IP ou token de autenticação válido pode realizar até 500 requisições por minuto aos endpoints públicos.
- **Janelas de Tempo:** A contagem de requisições é feita em janelas de tempo de 1 minuto, reiniciando a cada novo minuto.
- **Feedback de Limite Atingido:** Quando o limite de 500 requisições por minuto é atingido por um IP ou token específico, as requisições subsequentes dentro do mesmo período de 1 minuto receberão uma resposta com código de status HTTP 429 (Too Many Requests).

### Melhores Práticas para Desenvolvedores
Para evitar atingir o limite de requisições, recomendamos seguir estas melhores práticas:
- **Implementar Caching:** Utilize técnicas de caching para reduzir o número de requisições repetidas ao servidor.
- **Otimização de Requisições:** Agrupe múltiplas operações em uma única requisição quando possível.
- **Gestão de Erros:** Implemente uma lógica de retry exponencial para lidar com respostas de limite excedido (HTTP 429).

### Suporte e Contato
Caso encontre problemas relacionados ao rate limit ou precise de um limite personalizado entre em contato com nossa equipe de suporte através do e-mail [support@zapsign.com.br](mailto:support@zapsign.com.br) ou WhatsApp +55 11 4040-1991.

# Alerta de Incidentes

Sempre mantemos o padrão de disponibilidade das nossas aplicações em no mínimo 99,9%. 

### Verificação de Status
Se você quiser saber se estamos enfrentando algum problema de disponibilidade para fins de debug, acesse:

[ZapSign Status](https://zapsign.statuspage.io/)

### Notificações de Incidentes
Qualquer indisponibilidade ou incidente é sinalizado o mais rápido possível ao email cadastrado como proprietário. Para receber notificações sobre qualquer incidente e indisponibilidade, clique no botão "Subscribe to updates".

![image](https://github.com/user-attachments/assets/ee6f846d-5a81-44ae-9a3e-ccbbb4db9ea3)

# Status Code
 A ZapSign utiliza os códigos de status HTTP padrão. Erros 4xx ocorrem quando há um problema na solicitação enviada pelo cliente para a ZapSign. Já os erros 5xx indicam problemas inesperados nos servidores da ZapSign.

| Código | Referência         | Explicação                                                                                                                                                                              |
|--------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 400    | BAD REQUEST        | O servidor não processará a solicitação devido a algo que é percebido como um erro do cliente. Este é um erro genérico.A ZapSign processa todas as requisições em JSON, portanto erros no formato como falta de virgulas, base64 desformatados,etc podem ocasionar um erro 400.                                                                  |
| 401    | UNAUTHORIZED       | O servidor não autorizou a requisição. Access Token inválido.                                                                                                                             |
| 402    | PAYMENT REQUIRED   | O cliente não possui plano API. No ambiente de produção, é obrigatório possuir um plano mensal para utilizar a API em produção. Navegue até configurações>planos e preços ou [clique aqui](https://app.zapsign.co/conta/configuracoes/plans?tab=plans)                                                                                                                                                        |
| 403    | FORBIDDEN          | O servidor não autorizou a requisição. Verifique se o API token utilizado corresponde ao ambiente que deseja utilizar                                                                                      |
| 404    | NOT FOUND          | O servidor não encontrou o recurso ou não está disposto a divulgar sua existência. Verifique a url utilizada ou o template ID se estiver utilizando modelos dinâmicos                                                                                                      |
| 406    | NOT ACCEPTABLE     | A requisição está chegando no servidor e o servidor está recusando.                                                                                                                      |
| 429    | TOO MANY REQUESTS  | O cliente excedeu o limite de requisições permitidas em um determinado período de tempo.                                                                                                |

# Tipos de Tokens e Como Localizá-los

Tokens são essenciais para a integração e utilização eficiente da ZapSign. Neste guia, apresentamos os diferentes tipos de tokens disponíveis e como encontrá-los na plataforma. Se você precisa de informações sobre API Token, User Token, Template Token, Signer Token ou Doc Token, continue lendo!

### API Token
- **Localização:** Acesse **Configurações > Integrações > API Zapsign > Token de Acesso**.
- **Descrição:** Este é o token principal da conta, utilizado para integrar com a API.

### User Token
- **Localização:** Vá para **Configurações > Meu Perfil > Segurança > Assinatura via API**.
- **Descrição:** Token de assinatura exclusivo do usuário para assinatura em lote via API.

### Template ID
- **Localização:** Em **Modelos**, selecione o modelo desejado que deseja utilizar na API e clique em **Gerenciar**. Copie o código da URL após "modelos/".
- **Descrição:** Token específico de um modelo/formulário criado na plataforma.

### Signer Token
- **Localização:** Conjunto de números após o /verificar na url..
- **Descrição:** Token associado ao signatário. Após criar o documento e vincular os signatários, cada um possuirá seu próprio link. Este token ajuda a definir métodos de autenticação e até a detalhar o signatário via API.

### Doc Token
- **Localização:** Em **Documentos Criados**, selecione o documento e clique sobre ele. Copie o código da URL após "documentos/".
- **Descrição:** Token único para um documento criado na plataforma, usado para identificação e operações específicas.
