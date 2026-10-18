# Retrospectiva da documentação do ReqAI para handoff de implementação

## Objetivo e critério de leitura

Este documento analisa o trabalho de documentação feito no repositório desde a preparação da estrutura inicial até a descrição de Discovery e os diagramas. O objetivo é distinguir o que está apoiado por fontes do projeto, o que foi inferido ou acrescentado como modelo conceitual e o que ainda precisa ser decidido antes de um agente implementar o produto sem inventar comportamento.

**Importante:** uma inferência coerente com o README não é uma decisão aprovada pelo stakeholder. Os documentos são uma base para descoberta e handoff, não uma especificação funcional completa nem evidência de que o fluxo já funciona.

## 1. Inferências alinhadas às fontes disponíveis

| Inferência/documentação | Evidência no projeto | Avaliação |
|---|---|---|
| O foco do ReqAI é apoiar a etapa inicial de Discovery em projetos de software. | O README descreve levantamento de requisitos, análise de riscos e transformação de descrições de negócio em artefatos. | Alinhada ao contexto fornecido. |
| A jornada conceitual começa com texto fornecido em formulário e termina com revisão humana e possível exportação. | O README menciona formulário inicial, contexto textual, revisão pelo usuário e exportação Markdown/JSON. | Síntese coerente; o fluxo não foi confirmado com usuários. |
| Os artefatos principais são histórias de usuário, NFRs e riscos preliminares. | O README enumera esses três tipos e seus conteúdos gerais. | Diretamente apoiada, mas os esquemas e critérios de qualidade faltam. |
| O MVP descrito é local, sem histórico persistido, autenticação ou chat multi-turno. | Restrições e lacunas declaradas no README. | Diretamente apoiada para o escopo descrito; deve ser revalidada se o escopo mudar. |
| A IA é um serviço externo, mas seu fornecedor não pode ser afirmado apenas pelo nome da variável de configuração. | O README menciona SDK de IA e mostra `GEMINI_API_KEY` como exemplo. | Tratar Gemini como hipótese, não como decisão confirmada. |
| A pessoa usuária deve validar os resultados antes de usá-los. | O README atribui explicitamente validação e adaptação ao usuário. | Diretamente apoiada e preservada na descrição e nos diagramas. |
| Os requisitos não funcionais precisam de medidas e limites que ainda não foram fornecidos. | O README cita categorias, mas não define metas, volumes ou SLAs. | Correto não inventar valores; os critérios de medição são propostas para futura validação, não metas aprovadas. |

### Inferências plausíveis que continuam abertas

- Desenvolvedores e analistas são usuários possíveis, mas nenhum perfil foi confirmado.
- O fluxo de formulário → geração → revisão → exportação é uma jornada pretendida deduzida dos limites descritos, ainda não observada ou aprovada por stakeholders.
- A exportação pode ocorrer depois da revisão e para arquivos locais; os formatos são citados, mas nomes, estrutura, conteúdo e comportamento de download não foram definidos.
- A ausência de banco não determina se a aplicação pode manter resultados temporários na sessão. Essa distinção não foi especificada.

## 2. O que precisou ser ajustado ou explicitamente limitado

1. **Descrição de produto versus implementação:** o README original descrevia capacidades pretendidas como se fossem capacidades do sistema. A revisão passou a declarar que `app.py` contém somente a tela inicial Streamlit; integração com IA, geração, revisão e exportação ainda não estão implementadas.
2. **Limite dos containers:** uma decomposição inicial poderia sugerir serviços separados para interface e processamento. Como as fontes indicam uma aplicação local Python/Streamlit, o desenho estrutural foi consolidado em um container conceitual, sem inventar deploys ou serviços.
3. **Identidade do provedor:** `GEMINI_API_KEY` não prova qual SDK, endpoint ou modelo está efetivamente escolhido. O diagrama e a documentação mantêm o serviço externo genérico e registram a confirmação como pendência.
4. **Persistência:** o diagrama indica a ausência de banco/histórico no MVP, em vez de desenhar armazenamento inexistente. A retenção do estado temporário da sessão, entretanto, ainda precisa de uma decisão.
5. **Timeout e idempotência:** o diagrama de sequência foi ampliado a pedido para mostrar timeout, tentativa explícita e chave idempotente. Esse comportamento é conceitual. Não há implementação, garantia do provedor, chave durável, política de repetição ou decisão sobre custo confirmado. Timeout deixa o resultado remoto indeterminado; não significa que a chamada não foi processada.
6. **Detalhe de comportamento apresentado como exemplo:** frases como “retornar resultado associado à chave”, “evitar duplicidade concorrente” e “o provedor processa uma vez” descrevem possibilidades. Não podem ser usadas como contrato de implementação sem decisões sobre estado, escopo da chave e suporte externo.
7. **Localização e fontes dos diagramas:** os diagramas começaram como material da área de skills e foram colocados também em `diagramas/`, conforme o pedido posterior. O README contém cópias renderizáveis além dos fontes `.mmd`; essas cópias podem divergir se não houver validação de sincronização.
8. **Uso de GenAI:** os diagramas foram redigidos com assistência do agente, mas não houve chamada verificada a um provedor externo durante essa documentação. Portanto, não há versão/modelo de GenAI, prompt ou execução registrados para reprodução.
9. **Critérios não funcionais:** foram propostos métodos de medição sem criar metas numéricas. São um roteiro de esclarecimento; sem valores, contexto e aprovação, não são critérios de aceite executáveis.

## 3. O que a documentação ainda precisa para um agente construir sem inventar decisões

As perguntas e NFRs existentes em [esclarecimento-reqai.md](./esclarecimento-reqai.md) são um bom backlog de descoberta, mas as respostas ainda não estão registradas. Antes de implementar cada área, registrar uma decisão aprovada, um responsável e os critérios de aceite. No mínimo, completar os itens a seguir.

### 3.1 Decisões bloqueantes de produto e integração

- **Público e ambiente:** perfis de usuário, se o uso é individual/compartilhado, sistemas operacionais e browsers suportados, e significado concreto de “local”.
- **Dados e autorização:** campos aceitos, classificação de dados que não podem ser enviados, aviso/consentimento antes de enviar, conteúdo transmitido ao fornecedor, retenção no fornecedor e retenção/descarte local.
- **Fornecedor de IA:** SDK, provedor, modelo, região, conta, autenticação, termos de uso e tratamento de dados. O exemplo de variável de ambiente não é confirmação.
- **Contrato de chamada:** operações, campos enviados, formato esperado, limites, erros mapeados, versão do contrato e referência oficial a usar.
- **Custo e uso:** orçamento ou limite aprovado, modo de estimar/mostrar consumo e comportamento ao exceder limites; sem isso não escolher uma política silenciosamente.

### 3.2 Contrato funcional de cada artefato

Para histórias, critérios de aceitação, NFRs e riscos, definir antes da implementação:

- campos obrigatórios e opcionais, tipos, cardinalidade e exemplos aprovados;
- categorias permitidas e convenção de idioma/terminologia;
- regras para entrada incompleta, contradições e ausência de informação — perguntar, marcar como lacuna ou emitir resultado parcial;
- escalas e definições para probabilidade e impacto de risco, além da forma de representar mitigação;
- estrutura JSON versionada e regras para produzir Markdown equivalente;
- como apresentar incerteza, conteúdo inferido e necessidade de revisão humana.

### 3.3 Jornada, estado e falhas

- Campos, validações, limites e mensagens do formulário.
- Estados visíveis ao usuário (por exemplo, aguardando, concluído, falhou, resultado desconhecido) e quais dados permanecem após rerun/refresh da interface.
- Política de timeout definida com medição e critério aprovado; o README não fornece duração.
- Se e quando permitir repetição, limite/custo de novas chamadas e comportamento quando o timeout deixa o processamento remoto incerto.
- Garantias reais do fornecedor para idempotência; escopo e duração da chave; tratamento de pedidos simultâneos e de mesma chave com conteúdo diferente. Se nada disso for decidido, não anunciar “exactly once” nem simular uma garantia.
- Resposta para chave ausente/inválida, falha de rede, indisponibilidade, limite do fornecedor, resposta malformada, conteúdo vazio ou falha de validação.
- Se resultados são apenas temporários, quando expiram; se há download, quais arquivos são gerados e como são tratados cancelamento e repetição.

### 3.4 Qualidade, segurança e aceite

- Critérios testáveis para qualidade dos resultados, validação humana e categorias obrigatórias; exemplos de entrada/saída aprovados para testes de regressão.
- Requisitos de privacidade e segurança para chave, dados enviados, logs, exceções, dependências e arquivos exportados.
- Metas aprovadas para desempenho, custo e compatibilidade, ou um plano de medição e responsável por aprovar metas.
- Requisitos legais, acadêmicos, de licenciamento, acessibilidade e idiomas aplicáveis.
- Comandos e ambientes de execução/teste suportados, política de configuração e comportamento documentado da aplicação.

## 4. Regras de handoff para o agente de implementação

- Tratar fatos do README e decisões aprovadas como requisitos; tratar hipóteses e diagramas conceituais como não vinculantes.
- Não escolher provedor/modelo, persistência, retenção, escalas, limites, retry automático, timeouts numéricos ou metas de NFR por conveniência.
- Para uma lacuna bloqueante, interromper a implementação daquele comportamento e pedir decisão. Para uma lacuna não bloqueante, propor opções sem aplicá-las e registrar a proposta como pendente.
- Associar cada requisito a critérios de aceite observáveis e testes; não interpretar “gerar artefatos” como definição completa dos esquemas.
- Atualizar os diagramas quando contratos aprovados divergirem do desenho conceitual. Manter fonte `.mmd` e cópia Mermaid no README sincronizados, ou escolher uma única fonte canônica.
- Manter explícito o limite entre comportamento efetivamente implementado, escopo aprovado e hipótese futura.

## Conclusão

A documentação atual é suficiente para explicar o propósito, o escopo de alto nível, os limites conhecidos e algumas jornadas candidatas. **Ainda não é suficiente para implementar a integração generativa com segurança e comportamento determinístico sem decisões inventadas.** O principal bloqueio não é falta de mais diagramas: são decisões de stakeholder sobre dados, fornecedor, contrato dos artefatos, tratamento de falhas, estado/retenção, custo e critérios de aceite.
