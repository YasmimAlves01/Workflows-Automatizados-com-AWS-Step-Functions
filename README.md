# Workflows-Automatizados-com-AWS-Step-Functions
---

## 🧠 Conceitos Fundamentais

### O que são AWS Step Functions?
AWS Step Functions é um serviço de orquestração que permite coordenar múltiplos serviços da AWS em **fluxos de trabalho serverless**, com controle de estado, tratamento de erros e lógica condicional.

### Componentes principais:
- **State Machine**: definição do fluxo de estados.
- **States**: tarefas, escolhas, paralelismos, esperas, etc.
- **Tasks**: normalmente funções Lambda ou serviços integrados.
- **Transitions**: definem o caminho entre estados.
- **Input/Output**: cada estado pode receber e retornar dados.

---

## ⚙️ Processos Técnicos

### 1. Criação da State Machine
- Definida em JSON usando o **Amazon States Language (ASL)**.
- Exemplo de estrutura básica:
```json
{
  "StartAt": "TaskA",
  "States": {
    "TaskA": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGIAO:ID_FUNCION:func:taskA",
      "Next": "TaskB"
    },
    "TaskB": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGIAO:ID_FUNCION:func:taskB",
      "End": true
    }
  }
}
```

### 2. Integração com AWS Lambda
- Cada **Task** pode chamar uma função Lambda.
- As funções devem ser idempotentes e tratar entradas/saídas via JSON.

### 3. Tratamento de Erros
- Uso de blocos `Catch` e `Retry` para garantir resiliência.
- Exemplo:
```json
"Catch": [
  {
    "ErrorEquals": ["States.ALL"],
    "Next": "HandleError"
  }
]
```

### 4. Deploy com CloudFormation
- Templates para provisionar a state machine, funções Lambda e permissões.
- Exemplo de recurso:
```yaml
Resources:
  MyStateMachine:
    Type: AWS::StepFunctions::StateMachine
    Properties:
      DefinitionString: !Sub file://state-machines/basic-workflow.json
      RoleArn: arn:aws:iam::ID:role/StepFunctionsExecutionRole
```

---

## 📈 Insights e Aprendizados

- Diferença entre `Pass`, `Task` e `Choice`.
- Como versionar workflows com segurança.
- Estratégias para monitoramento com CloudWatch.
- Boas práticas para modularização de funções Lambda.

---

## 🧪 Testes e Validação

- Testes manuais via console AWS.
- Simulações com entradas de exemplo.
- Logs verificados no CloudWatch para cada execução.

---

Se quiser, posso te ajudar a transformar esse README em um repositório real com arquivos prontos para uso. É só me dizer!
