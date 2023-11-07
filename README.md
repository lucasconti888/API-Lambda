# API-Lambda

## Endpoint: https://8e4svgeky1.execute-api.us-east-1.amazonaws.com/default/lucasfuncao

```python
import json
import base64

username = "username"
password = "senha"

def lambda_handler(event, context):
    if 'headers' in event and 'Authorization' in event['headers']:
        encoded_credentials = event['headers']['Authorization'].split(' ')[-1]
        decoded_credentials = base64.b64decode(encoded_credentials).decode('utf-8')
        user, pwd = decoded_credentials.split(':')

        if user == username and pwd == password:
            
            return {
                'statusCode': 200,
                'body': json.dumps(event['body'])
            }
    
    return {
        'statusCode': 401,
        'body': json.dumps({'error': 'Acesso não autorizado'})
    }
```
O teste foi feito com a extensão do VS Code Thunder Clients.

import json:
Este módulo é usado para formatar a resposta HTTP em JSON.

import base64:
Este módulo é usado para decodificar a string Base64 que representa as credenciais no cabeçalho "Authorization", necessário para autenticação Basic.

username e password:
Estas são as variáveis que armazenam o nome de usuário e a senha para autenticação.

def lambda_handler(event, context)::
Esta função Lambda recebe dois parâmetros: event e context. event contém informações sobre a solicitação HTTP, incluindo o cabeçalho "Authorization" e o corpo da solicitação.

if 'headers' in event and 'Authorization' in event['headers']::
Verifica se o objeto event contém um campo 'headers' e se esse campo contém um campo 'Authorization'. Este é o local onde as credenciais de autenticação são transmitidas.

if user == username and pwd == password::
Compara o nome de usuário e a senha fornecidos na solicitação com os valores armazenados nas variáveis username e password. Se as credenciais estiverem corretas, a solicitação é autenticada.

return {'statusCode': 200, 'body': json.dumps(event['body'])}:
Se a autenticação for bem-sucedida, retorna uma resposta com status 200 (OK) e o corpo da solicitação em formato JSON.

return {'statusCode': 401, 'body': json.dumps({'error': 'Acesso não autorizado'})}:
Se as credenciais estiverem ausentes ou incorretas, retorna uma resposta com status 401 (Acesso não autorizado) e uma mensagem de erro em formato JSON. Isso indica falha na autenticação.
