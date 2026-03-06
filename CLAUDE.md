# Brag Document - Registro de Entregas

Projeto para registrar entregas e conquistas ao longo dos ciclos de avaliação de engenharia.

## Filosofia

Engenheiros são excelentes em escrever código, mas nem sempre conseguem articular bem o impacto do que fazem. Este projeto existe para ajudar nisso.

Ao registrar entregas, o assistente vai:
- **Melhorar o texto:** Corrigir erros, melhorar clareza e tom profissional
- **Destacar impacto:** Ajudar a quantificar resultados (R$, %, tempo, etc.)
- **Fazer perguntas:** Se faltar informação ou o impacto puder ser maior
- **Conectar com a ladder:** Mapear entregas para competências do seu nível

Você pode escrever de forma informal - o assistente transforma em texto de avaliação.

## Como usar

1. **Primeiro uso:** Execute `/setup` para configurar seu perfil (nível, área, etc.)
2. **Registrar entrega:** Execute `/entrega` e responda as perguntas interativas
3. **Suas entregas** ficam salvas em `entregas.md`

## Estrutura do projeto

- `context/` - Contexto sobre ladder e processo de avaliação (não editar)
- `meu-perfil.md` - Seu perfil pessoal (nível, área)
- `entregas.md` - Suas entregas registradas

## Arquivos de contexto

Ao ajudar o usuário, consulte:
- `context/ladder-ic.md` - Competências de Individual Contributor (L0-L9)
- `context/ladder-management.md` - Competências de Management (L4-L9)
- `context/processo-avaliacao.md` - Como funciona o processo de avaliação

## Comandos disponíveis

- `/setup` - Configurar perfil do usuário
- `/entrega` - Registrar uma nova entrega
- `/atualizar` - Adicionar informações a uma entrega existente (evidências, impacto, reconhecimento, etc.)
- `/avaliar` - Avaliar seu pacote de entregas e receber feedback antes da avaliação oficial
