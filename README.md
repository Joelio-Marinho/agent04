# Agente organizador de tarefas

Agente construído com Google ADK que conversa com o usuário para organizar as tarefas do dia e usa o Trello para armazená-las.

## O que o agente faz

O agente inicia perguntando quais são as tarefas do dia, informa a data e hora atuais e pode continuar perguntando se há mais tarefas. As tarefas são organizadas como cards em um board do Trello.

### Ferramentas

- `get_temporal_context`: retorna a data e a hora atuais.
- `adicionar_tarefa`: cria um card com nome, descrição e vencimento na lista de tarefas a fazer.
- `listar_tarefas`: lista os cards de todas as listas ou filtra por `a fazer`, `em andamento` ou `concluido`.
- `mudar_status_tarefa`: move um card para `a fazer`, `em andamento` ou `concluido`.

O agente precisa de um board chamado `DIO`. Para adicionar tarefas, esse board também precisa ter uma lista `TO DO` ou `A FAZER`. Para mover tarefas, crie as listas de destino `A FAZER`, `EM ANDAMENTO` e `CONCLUÍDO`.

## Configuração e execução

1. Instale as dependências a partir da pasta do projeto:

   ```bash
   pip install -r requirements.txt
   ```

2. No Trello, obtenha uma API key e um API secret nas configurações de desenvolvedor e gere um token com acesso ao board `DIO`. As credenciais precisam permitir consultar o board e criar e mover cards.

3. Crie o arquivo `agenttaskmanager/.env` com as credenciais do Trello e a chave de acesso ao modelo Gemini:

   ```dotenv
   TRELLO_API_KEY=sua_api_key
   TRELLO_API_SECRET=seu_api_secret
   TRELLO_TOKEN=seu_token
   GOOGLE_API_KEY=sua_chave_google
   ```

   Não compartilhe esse arquivo nem publique suas credenciais. O arquivo `.env` já está listado no `.gitignore` do agente.

4. A partir da pasta do projeto, inicie a interface web do Google ADK:

   ```bash
   adk web
   ```

   Selecione `agenttaskmanager` na interface para conversar com o agente.

## Melhoria implementada e teste

A melhoria escolhida foi tratar erros com `try/except` em todas as ferramentas, não apenas em `mudar_status_tarefa`. As ferramentas agora retornam uma mensagem de erro em português quando ocorre uma exceção; ao adicionar uma tarefa com sucesso, também retornam uma confirmação.

O teste realizado foi a verificação de sintaxe do módulo:

```bash
python -m py_compile agenttaskmanager/agent.py
```

O comando terminou com sucesso. Esse teste valida a sintaxe do código, mas não testa a conexão nem as operações reais com o Trello.
# agent04
