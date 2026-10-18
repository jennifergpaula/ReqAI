# Discovery — descrição do sistema ReqAI

## Visão e propósito

O ReqAI é concebido como uma ferramenta de apoio às etapas iniciais (*Discovery*) de projetos de software. Seu propósito é receber uma descrição textual de um problema de negócio ou de uma ideia de produto e ajudar a transformá-la em artefatos preliminares de engenharia de requisitos e análise de riscos. Os resultados apoiam o trabalho de pessoas, mas não substituem análise, julgamento ou aprovação humanos.

Esta descrição consolida o escopo pretendido documentado no README. Ela não afirma que todos os fluxos já estejam implementados: o `app.py` atual contém apenas uma interface Streamlit inicial, sem fluxo de geração integrado.

## Nível da visão

- **Visão de negócio/produto:** reduzir o esforço de padronização dos artefatos iniciais de requisitos e riscos.
- **Visão de usuário:** uma pessoa fornece contexto em um formulário, solicita uma geração pontual, revisa o resultado e pode exportá-lo.
- **Visão de sistema:** aplicação local com interface Streamlit e código Python, que pretende integrar-se a um serviço externo de IA generativa e apresentar artefatos estruturados.
- **Nível de detalhe:** visão conceitual do MVP; usuários específicos, implantação compartilhada, provedor/modelo e políticas de dados ainda precisam ser confirmados.

## Usuários e jornada

### Fatos documentados

- O sistema recebe uma descrição textual por meio de um formulário inicial.
- O usuário é responsável por fornecer contexto, revisar, validar e adaptar os resultados.
- A geração do MVP é pontual; chat multi-turno não faz parte do escopo descrito.

### Hipótese a confirmar

- O público principal pode incluir pessoas desenvolvedoras e analistas que participam da descoberta de produtos de software. O README não define perfis, permissões nem se o uso será individual ou compartilhado.

### Jornada pretendida

1. A pessoa descreve um problema de negócio ou uma ideia de software.
2. Solicita uma geração de artefatos.
3. Revisa as histórias de usuário, os requisitos não funcionais e os riscos preliminares.
4. Ajusta ou valida os resultados fora do sistema e, quando úteis, exporta-os em Markdown ou JSON.

## Escopo funcional

- Receber uma descrição textual de problema ou ideia.
- Gerar histórias de usuário no formato “Como... Quero... Para...” com critérios de aceitação.
- Gerar requisitos não funcionais categorizados, por exemplo em desempenho, segurança e usabilidade.
- Gerar uma matriz preliminar de riscos com probabilidade, impacto e estratégias de mitigação.
- Apresentar os resultados e permitir exportação em Markdown e JSON.

## Limites e responsabilidades

### Responsabilidade do sistema pretendido

- Processar a entrada e apresentar artefatos estruturados.
- Sinalizar que os artefatos são preliminares e dependem de revisão humana.
- Apoiar, e não substituir, a análise técnica ou de negócio.

### Responsabilidade do usuário

- Fornecer contexto apropriado e autorizado para processamento.
- Revisar, validar e adaptar requisitos e riscos antes do uso real.
- Decidir se o conteúdo pode ser compartilhado com o serviço externo de IA.

### Fora do escopo documentado para o MVP

- Gestão de projetos, incluindo Kanban, sprints e tarefas.
- Autenticação, controle de acesso e múltiplos perfis.
- Histórico persistente em banco de dados.
- Conversa iterativa ou refinamento em chat multi-turno.
- Aprovação automática dos artefatos sem validação humana.

## Integrações

- **IA generativa externa:** o README prevê um SDK de IA com suporte a *Structured Outputs*. A configuração de exemplo usa `GEMINI_API_KEY`, o que sugere Gemini, mas não confirma o provedor, o modelo nem as condições de tratamento dos dados.
- **Execução e interface:** Python 3.x e Streamlit são as tecnologias indicadas no README.
- **Exportação:** arquivos Markdown e JSON são saídas para a pessoa usuária, não uma integração remota especificada.
- **Desenvolvimento:** VS Code e Git/GitHub são ferramentas de desenvolvimento e versionamento; não são integrações de runtime do produto.

## Restrições

- O MVP é descrito como uma aplicação executada localmente, sem necessidade de infraestrutura em nuvem ou containers complexos.
- O esforço previsto no README é individual, com duração aproximada de dois meses e cerca de 32 horas.
- Não há requisito informado de disponibilidade, desempenho, volume, custo máximo, sistemas operacionais suportados ou acessibilidade; esses critérios precisam ser definidos antes de se tornarem metas.
- A dependência atualmente listada em `requirements.txt` é Streamlit. O `app.py` atual mostra apenas a tela inicial e não implementa a integração de IA nem os fluxos funcionais descritos no README.

## Lacunas e perguntas em aberto

- Quais perfis usarão o sistema e se haverá uma ou várias pessoas por instalação?
- Quais dados podem ser enviados ao serviço externo? Há dados pessoais, confidenciais ou regulados?
- Qual provedor/modelo será usado, em que região e com quais regras de retenção ou uso dos dados?
- Como serão medidos qualidade dos artefatos, tempo de resposta e custo aceitáveis?
- Como a aplicação deve se comportar diante de falha de rede, timeout, chave inválida ou resposta malformada?
- Qual é a política para retenção e descarte de entradas, resultados e arquivos exportados?
- Quais regras e campos tornam cada artefato aceitável para os stakeholders?
- Quais sistemas operacionais, necessidades de acessibilidade e obrigações regulatórias se aplicam?
