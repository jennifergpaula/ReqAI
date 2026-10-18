# Esclarecimento de requisitos — ReqAI

## Base usada

### Fatos informados no README

- O ReqAI apoia as etapas iniciais de levantamento de requisitos e análise de riscos em projetos de software.
- Recebe uma descrição textual de um problema de negócio ou ideia de software.
- Gera histórias de usuário com critérios de aceitação, requisitos não funcionais categorizados e uma matriz preliminar de riscos com probabilidade, impacto e mitigação.
- Permite visualizar e exportar os resultados em Markdown e JSON.
- O fluxo descrito é pontual, iniciado por um formulário; não há chat multi-turno nesta versão.
- A aplicação é executada localmente no MVP, sem persistência complexa ou histórico em banco de dados.
- Profissionais humanos devem revisar e validar os resultados; o sistema não substitui essa validação.
- O README informa Python 3.x, Streamlit e um SDK de IA generativa com suporte a *Structured Outputs*. A configuração de exemplo usa `GEMINI_API_KEY`.
- O projeto é um TCC planejado para execução individual em aproximadamente dois meses e 32 horas de dedicação.
- O README declara que não há autenticação nem múltiplos perfis de usuário.

### Hipóteses inferidas — precisam de confirmação

- O usuário principal pode ser uma pessoa desenvolvedora ou analista envolvida na descoberta de um produto de software.
- A jornada principal pode consistir em preencher o formulário uma vez, revisar os artefatos gerados e exportá-los.
- O uso local pode ser individual, mas o README não confirma se haverá mais de uma sessão ou usuário na mesma instalação.
- A chave `GEMINI_API_KEY` sugere uso de um serviço Gemini; o provedor, modelo e fluxo efetivamente utilizados ainda precisam ser confirmados.

### Lacunas conhecidas

- Perfil dos usuários, volume e frequência de uso, idiomas, tamanho e sensibilidade das entradas.
- Provedor/modelo de IA, tratamento dos dados por esse provedor, região de processamento e condições de uso.
- Metas de qualidade, limites de custo, requisitos de acessibilidade e sistemas operacionais suportados.
- Requisitos legais, regulatórios, de licenciamento, retenção e descarte de dados.
- Comportamento esperado em falhas, indisponibilidade de rede ou respostas inválidas do serviço externo.

## 1. Perguntas de esclarecimento

Ordenadas pelo potencial de alterar decisões difíceis de reverter. Responda “a definir” quando ainda não houver uma decisão.

1. **Usuários e decisões:** Quem usará o ReqAI e em que etapa do trabalho? Quais decisões ou entregáveis dependerão dos resultados?
2. **Consequências de erro:** O que pode acontecer se uma história, requisito ou risco for omitido ou apresentado incorretamente? Há usos em que o resultado não pode ser utilizado sem validação adicional?
3. **Dados de entrada:** Que informações reais serão inseridas (por exemplo, dados de clientes, funcionários, produtos ou propriedade intelectual)? Há dados pessoais, confidenciais ou regulados?
4. **Envio a serviços externos:** Os usuários podem autorizar o envio da descrição e dos resultados a um provedor de IA externo? Que dados não podem sair do ambiente local?
5. **Provedor de IA:** Qual provedor e serviço/modelo serão usados no MVP? Há exigência de região, retenção, não treinamento com os dados, contrato ou conta específica?
6. **Público e implantação:** “Executada localmente” significa uso apenas pela pessoa desenvolvedora, instalação em computadores de usuários ou acesso por uma rede local? Mais de uma pessoa poderá usar a mesma instalação?
7. **Escopo dos artefatos:** Quais campos e regras são obrigatórios para histórias, critérios de aceitação, NFRs e riscos? Existem modelos, normas ou formatos que precisam ser seguidos?
8. **Qualidade e revisão:** Como os usuários decidirão que um resultado é aceitável? Quais erros devem ser sinalizados, corrigidos ou rejeitados, e quem aprova a saída?
9. **Conteúdo e limites de entrada:** Quais idiomas, tipos de texto e comprimentos de descrição precisam ser aceitos? Há anexos ou apenas texto digitado?
10. **Exportação:** Os arquivos Markdown e JSON atendem ao uso esperado? É necessário definir nomes, estrutura, codificação, compatibilidade ou proteção dos arquivos exportados?
11. **Retenção e histórico:** Uma geração deve existir apenas durante a sessão ou ser recuperável depois? Por quanto tempo entradas, resultados e arquivos exportados podem permanecer no dispositivo?
12. **Falhas externas:** O que o usuário deve ver quando não houver internet, a chave estiver inválida, o serviço estiver indisponível ou a resposta não puder ser usada? Deve ser possível repetir a solicitação?
13. **Prioridades de qualidade:** Como devem ser priorizados tempo de resposta, qualidade dos artefatos, privacidade/segurança, facilidade de uso e custo? Há algum requisito inegociável?
14. **Volume e custo:** Qual frequência de uso e quantidade de gerações são esperadas? Existe orçamento ou limite de consumo? Como custo e consumo devem ser acompanhados?
15. **Plataformas e acessibilidade:** Quais sistemas operacionais, navegadores e tecnologias assistivas precisam ser suportados? Há requisitos de idioma ou acessibilidade aplicáveis?
16. **Regulação e licenças:** Há obrigações legais, contratuais, acadêmicas ou de licenciamento para dados de entrada, conteúdo gerado, dependências e serviço de IA?
17. **MVP e evolução:** O fluxo de geração única é suficiente para a entrega do TCC? Histórico, autenticação e refinamento iterativo estão explicitamente fora do MVP ou são necessários para algum usuário?

## 2. Requisitos não funcionais a esclarecer

Os critérios abaixo indicam como verificar cada atributo; **as metas e limites de aceitação ainda precisam ser definidos pelos stakeholders**. Não há valores numéricos assumidos.

1. **Privacidade e minimização:** O sistema deve enviar a um serviço externo somente os dados autorizados pelo usuário, durante uma geração. **Condição:** submissão de uma descrição e processamento externo habilitado. **Verificação:** mapear os dados enviados e comparar uma captura da requisição com os campos aprovados; acordar previamente quais campos são permitidos.
2. **Proteção de dados e credenciais:** O sistema deve evitar exposição de chaves e de conteúdo sensível em arquivos versionados, mensagens de erro e registros acessíveis. **Condição:** configuração, geração bem-sucedida e falhas de autenticação/conectividade. **Verificação:** inspecionar arquivos versionados e saídas da aplicação com valores de teste identificáveis; definir os locais e o período de retenção permitidos.
3. **Correção estrutural dos resultados:** Os artefatos devem respeitar os campos e formatos acordados e ser exportáveis em Markdown e JSON. **Condição:** execução com casos representativos, incluindo entradas incompletas e respostas inesperadas. **Verificação:** validar a estrutura JSON, abrir e revisar o Markdown e comparar campos obrigatórios com uma lista de aceitação aprovada pelos stakeholders.
4. **Desempenho percebido:** A geração deve concluir em tempo compatível com o fluxo de trabalho. **Condição:** medir desde o envio do formulário até a exibição do resultado, separando, quando possível, o tempo do serviço externo. **Verificação:** coletar tempos em cenários representativos e acordar o limite aceitável com os usuários antes de definir uma meta.
5. **Tratamento de falhas e confiabilidade:** Falhas do serviço externo ou de rede devem ser comunicadas sem apresentar uma resposta incompleta como sucesso. **Condição:** chave ausente/inválida, desconexão, indisponibilidade e resposta inválida. **Verificação:** simular cada falha e confirmar mensagem compreensível, preservação do estado permitido e orientação de recuperação definida pelos stakeholders.
6. **Usabilidade e revisão humana:** Um usuário do público-alvo deve conseguir enviar o contexto, identificar os artefatos e revisar o conteúdo antes de utilizá-lo. **Condição:** execução da jornada principal por usuários representativos, sem instruções adicionais além das que serão disponibilizadas. **Verificação:** observar a conclusão das tarefas e registrar dúvidas, erros e pontos de abandono; definir critérios de aceitação com os usuários.
7. **Compatibilidade de execução:** A aplicação deve funcionar nos sistemas operacionais e navegadores definidos para o MVP. **Condição:** instalação limpa nos ambientes-alvo, com dependências e configuração documentadas. **Verificação:** executar uma lista acordada de instalação, geração e exportação em cada ambiente suportado.
8. **Custo operacional:** O consumo do serviço de IA deve ser observável o suficiente para avaliar se cabe no orçamento acordado. **Condição:** uso representativo durante o período de avaliação definido pelo responsável pelo projeto. **Verificação:** registrar número de solicitações e custos informados pelo provedor, comparar com o orçamento aprovado e definir previamente o procedimento para excedentes.

## 3. Decisões que não devem ser tomadas ainda

- **Escolha ou compromisso com provedor/modelo de IA:** faltam confirmação do serviço, região, termos de retenção, uso dos dados para treinamento, custo e limites.
- **Persistência de entradas e resultados:** faltam decisão sobre histórico, necessidade de recuperação, sensibilidade dos dados, retenção e descarte.
- **Compartilhamento, autenticação ou múltiplos perfis:** faltam público, modelo de implantação, quantidade de usuários e limites de acesso necessários.
- **Limites de entrada e desempenho:** faltam idiomas, comprimentos e volumes representativos, prioridade de qualidade e tempos aceitáveis medidos.
- **Regras definitivas de geração e aceitação:** faltam campos obrigatórios, padrões aplicáveis, tolerância a erros e processo de revisão/aprovação.
- **Política de tratamento de falhas e novas tentativas:** faltam impacto de uma falha, custo por nova solicitação e comportamento esperado pelo usuário.
- **Metas de segurança, privacidade e conformidade:** faltam classificação dos dados, jurisdição, obrigações legais/contratuais e restrições do provedor.
- **Suporte a plataformas e acessibilidade:** faltam sistemas operacionais, navegadores, tecnologias assistivas e necessidades dos usuários.
- **Inclusão de histórico, autenticação ou refinamento iterativo no MVP:** faltam prioridade dos stakeholders e impacto dessas capacidades no escopo de aproximadamente 32 horas informado no README.
