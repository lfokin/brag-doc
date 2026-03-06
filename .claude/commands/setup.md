# Configurar Perfil

Você está ajudando o usuário a configurar seu perfil para o brag document.

## Fluxo

Use a ferramenta AskUserQuestion para coletar as informações. Pode fazer múltiplas perguntas de uma vez.

### Informações a coletar:

1. **Nome:** Como você quer ser identificado?

2. **Nível atual:** Qual seu nível na ladder? (L0 a L9)

3. **Track:** Você é IC (Individual Contributor) ou Management?

4. **Área/Tribo:** Em qual área ou tribo você trabalha?

## Após coletar as respostas:

1. Atualize o arquivo `meu-perfil.md` com as informações coletadas
2. Confirme para o usuário que o perfil foi configurado
3. Informe que ele pode usar `/entrega` para começar a registrar suas entregas

## Formato do arquivo meu-perfil.md:

```markdown
# Meu Perfil

- **Nome:** [nome]
- **Nível:** [L0-L9]
- **Título:** [título correspondente ao nível]
- **Track:** [IC ou Management]
- **Área/Tribo:** [área]
- **Configurado em:** [data]
```

Consulte os arquivos `context/ladder-ic.md` ou `context/ladder-management.md` para pegar o título correto baseado no nível e track informados.
