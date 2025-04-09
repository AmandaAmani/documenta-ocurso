
# 🧭 Artigo 1: Adicione o carimbo de tempo com assinatura ZapSign

## O que é o Carimbo de Tempo?

O **Carimbo de Tempo** é uma solução de segurança que autentica a existência de um documento em um momento específico. Ele registra **data e hora do servidor de uma Autoridade Certificadora de Tempo (ACT)**, e adiciona uma **assinatura da ZapSign** ao PDF.

Esse endpoint é ideal para **comprovar a existência do documento**, mesmo que ele ainda não tenha sido assinado por um signatário.

## Quando usar este endpoint?

Use este endpoint se você deseja **carimbar um documento digital sem nenhuma assinatura anterior** ou se não é necessário preservar a assinatura original do signatário.

> ⚠️ Esse carimbo substitui eventuais assinaturas anteriores pelo certificado da ZapSign.

## Endpoint

```
POST https://api.zapsign.com.br/api/v1/timestamp/
```

## Headers

| Nome           | Valor                     |
|----------------|---------------------------|
| `Content-Type` | `application/json`        |
| `Authorization`| `API_TOKEN_DA_SUA_ORGANIZAÇÃO` |

## Body

Adicione a **URL pública** do documento ou envie o conteúdo codificado em base64 (máx. 10MB).

```json
{
  "url": "<Adicione_sua_url_ou_base64>"
}
```

## Exemplo de resposta

```json
{
  "url": "https://zapsign.s3.amazonaws.com/pdf/62c2b027-d8fc-4392-xas75-f3c46c3cfc7a/d33336-4182-8c8b-ded5287e4c0f.pdf"
}
```

## Teste com cURL

```bash
curl -X POST https://api.zapsign.com.br/api/v1/timestamp/ \
-H "Content-Type: application/json" \
-H "Authorization: SEU_API_TOKEN" \
-d '{"url": "https://exemplo.com/documento.pdf"}'
```

## Teste com Postman

1. Método: `POST`
2. URL: `https://api.zapsign.com.br/api/v1/timestamp/`
3. Headers:
   - `Content-Type`: `application/json`
   - `Authorization`: `SEU_API_TOKEN`
4. Body (raw JSON):

```json
{
  "url": "https://exemplo.com/documento.pdf"
}
```

---

# 🔒 Artigo 2: Adicione o carimbo de tempo preservando a assinatura original

## O que é?

Este endpoint também adiciona um **Carimbo de Tempo certificado por uma ACT**, mas **sem substituir a assinatura original** do signatário.

> ✅ Útil para reforçar a validade de documentos já assinados por outras partes.

## Quando usar este endpoint?

Use quando você já tem um documento assinado e deseja apenas adicionar a **camada de validação temporal**, sem interferir nas assinaturas.

## Endpoint

```
POST https://api.zapsign.com.br/api/v1/timestamp/no-signature
```

## Headers

| Nome           | Valor                     |
|----------------|---------------------------|
| `Content-Type` | `application/json`        |
| `Authorization`| `API_TOKEN_DA_SUA_ORGANIZAÇÃO` |

## Body

```json
{
  "url": "<Adicione_sua_url_ou_base64>"
}
```

## Exemplo de resposta

```json
{
  "url": "https://zapsign.s3.amazonaws.com/pdf/62c2b027-d8fc-4392-xas75-f3c46c3cfc7a/d33336-4182-8c8b-ded5287e4c0f.pdf"
}
```

## Teste com cURL

```bash
curl -X POST https://api.zapsign.com.br/api/v1/timestamp/no-signature \
-H "Content-Type: application/json" \
-H "Authorization: SEU_API_TOKEN" \
-d '{"url": "https://exemplo.com/documento.pdf"}'
```

## Teste com Postman

1. Método: `POST`
2. URL: `https://api.zapsign.com.br/api/v1/timestamp/no-signature`
3. Headers:
   - `Content-Type`: `application/json`
   - `Authorization`: `SEU_API_TOKEN`
4. Body (raw JSON):

```json
{
  "url": "https://exemplo.com/documento.pdf"
}
```

---

# 🔍 Comparativo entre os endpoints

| Característica                        | `/timestamp/`                        | `/timestamp/no-signature`                |
|--------------------------------------|--------------------------------------|------------------------------------------|
| Substitui assinatura existente?      | ✅ Sim                               | ❌ Não                                   |
| Preserva assinatura do signatário?   | ❌ Não                               | ✅ Sim                                   |
| Assinatura da ZapSign incluída?      | ✅ Sim                               | ❌ Não                                   |
| Recomendado para documentos assinados| ❌ Não                               | ✅ Sim                                   |

---

# 📌 Glossário

| Termo | Definição |
|-------|----------|
| **Signatário** | Pessoa que assina um documento |
| **Carimbo de Tempo** | Registro oficial da hora de assinatura, emitido por uma ACT |
| **ACT** | Autoridade Certificadora de Tempo |
| **API Token** | Chave de autenticação da organização na API |
| **Base64** | Formato de codificação de arquivos para transmissão segura |

---

# 🤝 Precisa ativar essa funcionalidade?

Entre em contato com nosso time comercial para incluir o carimbo de tempo direto ou com preservação de assinatura no seu plano.
