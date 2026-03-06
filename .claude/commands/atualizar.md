# Atualizar Entrega Existente

Você está ajudando o usuário a adicionar mais informações a uma entrega já registrada.

## Objetivo

Agregar informações a uma entrega existente sem sobrescrever o que já está lá. Útil para:
- Adicionar evidências (novos PRs, docs)
- Atualizar impacto quando métricas ficam disponíveis
- Registrar reconhecimentos recebidos
- Adicionar colaborações que surgiram depois
- Complementar informações que faltaram

## Fluxo

### 1. Listar entregas

Leia o arquivo `entregas.md` e extraia todas as entregas registradas. Para cada entrega, mostre:
- Nome da entrega
- Data
- Ciclo (2025-H1, 2025-H2, etc.)

Use AskUserQuestion para o usuário selecionar qual entrega quer atualizar. Liste as entregas como opções (máximo 4 por vez, se tiver mais, agrupe por ciclo ou pagine).

### 2. Mostrar entrega atual

Após o usuário selecionar, mostre o conteúdo completo da entrega atual para ele ter contexto.

### 3. Coletar novas informações

Pergunte o que o usuário quer adicionar. Use AskUserQuestion com opções:

- **Evidências** - Novos PRs, docs, dashboards, cards
- **Impacto** - Métricas atualizadas, resultados que surgiram depois
- **Reconhecimento** - Feedback positivo, elogios recebidos
- **Colaboração** - Novos times/pessoas envolvidas
- **Visibilidade** - Tech talks, demos, apresentações
- **Outro** - Qualquer outra informação

### 4. Coletar detalhes

Baseado na opção selecionada, faça perguntas específicas:

**Evidências:**
- "Cole os links das novas evidências"

**Impacto:**
- "Qual métrica/resultado você quer adicionar?"
- "É impacto de negócio ou técnico?"

**Reconhecimento:**
- "Quem deu o feedback? (pessoa, cargo)"
- "O que foi dito? (pode ser informal)"

**Colaboração:**
- "Quais novos times/pessoas se envolveram?"

**Visibilidade:**
- "Onde você apresentou? (tech talk, demo, all hands, etc.)"
- "Tem link da apresentação ou gravação?"

**Outro:**
- "O que você quer adicionar?"

### 5. Atualizar a entrega

Ao atualizar, **não sobrescreva** informações existentes. Adicione as novas informações na seção apropriada:

- Novas evidências: adicione na lista de evidências existente
- Novo impacto: adicione como item novo na seção de impacto, com data se relevante
- Reconhecimento: crie seção **Reconhecimentos:** se não existir
- Nova colaboração: adicione aos times já listados
- Visibilidade: crie seção **Visibilidade:** se não existir
- Outro: adicione na seção mais apropriada ou crie nova

### 6. Melhoria de texto

Assim como no /entrega, melhore o texto do usuário:
- Corrija erros gramaticais
- Torne mais profissional
- Mantenha consistência com o resto da entrega

### 7. Confirmar

Mostre o que foi adicionado e pergunte se está ok ou se quer ajustar algo.

## Exemplo de atualização

**Antes:**
```markdown
**Impacto:**
- Negócio: Adequação a requisitos de compliance
- Técnico: Implementação do princípio do menor privilégio
```

**Usuário adiciona:** "descobrimos que evitamos 3 incidentes de segurança por mês"

**Depois:**
```markdown
**Impacto:**
- Negócio: Adequação a requisitos de compliance; prevenção estimada de 3 incidentes de segurança/mês
- Técnico: Implementação do princípio do menor privilégio
```

## Perguntar se quer continuar

Após cada atualização, pergunte se o usuário quer adicionar mais informações à mesma entrega ou se finalizou.
