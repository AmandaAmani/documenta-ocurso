## Boas vindas à documentação de api da ZapSign!
### Nossa API é projetada para ser simples e intuitiva, permitindo que você integre a ZapSign rapidamente em suas aplicações.

A ZapSign é uma plataforma de assinatura eletrônica de documentos que cumpre os requisitos da Medida Provisória 2.200-2/2001, garantindo autenticidade, integridade e não repúdio. Assim, todas as assinaturas realizadas através da ZapSign possuem validade jurídica.
### Antes de começar
- [Registre-se](https://app.zapsign.com.br/acesso/criar-conta) ou [faça login na ZapSign](https://app.zapsign.com.br/acesso/entrar) para obter seu token de autenticação.
- Sempre configure Token de Acesso no header de Autorização de todas as suas chamadas

## E como obter meu api token?
Dentro da sua conta zapsign, clique **Configurações>Integrações>API ZAPSIGN** depois copie seu token e configure na sua ferramenta.  

![chrome-capture-2024-7-25 (2)](https://github.com/user-attachments/assets/eb777fa6-f08c-4315-af5b-14a8212a271f)



Trabalhamos com uma API REST, que utiliza os métodos GET e POST. Lemos tudo em JSON e nossas respostas também são em JSON.
|----------------------------------------------------------------------------------------------------------------------------------|


#### Ambientes
A ZapSign oferece dois ambientes para utilização da Api. Se você ainda não realizou nenhuma integração com a ZapSign, recomendamos que você inicie pelo ambiente de testes (sandbox) para evitar cobranças indevidas. 
|Ambiente|Endpoint|Validade juridica|
|--------|--------|------------------|
|Sandbox|https://sandbox.api.zapsign.com.br|não possui validade jurídica|
|Produção|https://api.zapsign.com.br|Possui validade jurídica|

## Integração com Clientes para API: Postman e Insomnia ##

Postman e Insomnia são ferramentas que facilitam o desenvolvimento, teste e documentação de APIs. Nós da ZapSign deixamos todas as bibliotecas de requisições prontas para ambas as ferramentas.
[POSTMAN WORKSPACE](https://elements.getpostman.com/redirect?entityId=27495556-787b914f-ebeb-426a-9808-7fb0bd0d47fd&entityType=collection)
|------------------------------------------------------------------------------------------------------------------------------------------|

Após abrir o link, selecionar o ambiente que você gostaria de testar, disponível no canto superior direito e crie um fork para acessar todos os endpoints dentro do seu próprio WorkSpace

![image](https://github.com/user-attachments/assets/6623593d-9698-40ed-8107-206e6ed76b26)

Com o postman configurado, você já pode utilizar todos os endpoints. A única variavel obrigatória é a [api_token](https://app.zapsign.com.br/conta/configuracoes/integration?tab=api-zapsign), seu token de autenticação. Todas as outras podem ser preenchidas conforme sua necessidade.

Para o Insomnia, deixamos todosos endpoints preparados neste arquivo:

[Biblioteca Insomnia](https://3085168645-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M4noMoX5ZGb2-RhWjjf-887967055%2Fuploads%2Fx7qCxGPFotUx362LKpvF%2FInsomnia_2023-03-27.json?alt=media&token=92133638-2480-439e-9e9c-eab3727e72f5)
|---------------------------------------------------------------------------------------|
//Inserir imagens do insomnia e mais detalhes//


## Autenticação
















 
