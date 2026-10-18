# ReqAI - Assistente Inteligente de Engenharia de Requisitos e Análise de Riscos

O **ReqAI** é uma ferramenta projetada para automatizar e padronizar as etapas iniciais de levantamento de requisitos e análise de riscos em projetos de software utilizando Inteligência Artificial Generativa. O projeto foi concebido como Trabalho de Conclusão de Curso (TCC) para a pós-graduação em Engenharia de Software.

---

## 📋 Visão Geral

Na fase de concepção (*Discovery*) de software, a documentação inicial consome tempo considerável e muitas vezes carece de padronização. O **ReqAI** atua como uma ferramenta de apoio (*Developer/Analyst Tooling*), recebendo descrições textuais brutas de problemas de negócio e transformando-as em artefatos formais e estruturados de engenharia de software.

---

## 🎯 Escopo do Sistema

### O que o sistema faz:
- **Processamento de Linguagem Natural:** Recebe uma descrição textual bruta de um problema de negócio ou ideia de software.
- **Geração de Artefatos Estruturados:**
  - **Histórias de Usuário:** Formato ágil (*Como... Quero... Para...*) com critérios de aceitação.
  - **Requisitos Não Funcionais:** Categorizados (desempenho, segurança, usabilidade, etc.).
  - **Matriz de Riscos Preliminar:** Riscos com probabilidade, impacto e estratégias de mitigação.
- **Exportação:** Permite a visualização e exportação dos dados gerados em formatos estruturados (Markdown / JSON).

### O que o sistema NÃO faz:
- Não é um sistema de gestão de projetos (não possui Kanban, sprints ou gestão de tarefas).
- Não substitui a validação técnica e de negócio realizada por profissionais humanos.
- Não realiza persistência complexa de dados em banco de dados na versão MVP.

---

## 👤 Limites e Responsabilidades

* **Limites do Sistema:** Focado na geração pontual e estruturada de artefatos a partir do envio de um formulário inicial.
* **Responsabilidade do Sistema:** Processar o texto de entrada e retornar dados estruturados via técnicas avançadas de *prompting* e *Structured Outputs*.
* **Responsabilidade do Usuário:** Fornecer um contexto inicial claro, revisar, validar e adaptar os requisitos e riscos gerados para uso real no projeto.

---

## 🛠️ Pilha Tecnológica e Integrações

* **Linguagem:** Python 3.x
* **Interface:** Streamlit
* **Inteligência Artificial:** SDK oficial de IA Generativa (com suporte a *Structured Outputs*)
* **Ambiente de Desenvolvimento:** Visual Studio Code
* **Controle de Versão:** Git / GitHub

---

## ⚠️ Restrições e Lacunas (Gaps)

### Restrições:
* **Tempo de Desenvolvimento:** Projetado para execução individual em um período de 2 meses (~32 horas de dedicação total).
* **Infraestrutura:** Aplicação executada localmente, sem necessidade de infraestrutura de nuvem ou *containers* complexos para a versão MVP.

### Lacunas Conhecidas (Work in Progress / Futuras Melhorias):
* **Autenticação:** Não contempla controle de acesso ou múltiplos perfis de usuário.
* **Persistência de Dados:** Ausência de banco de dados para histórico de projetos gerados.
* **Refinamento Iterativo:** A geração é executada em bloco único a partir do prompt inicial, sem suporte a chat multi-turno nesta versão.

---

## 🚀 Como Executar o Projeto Localmente

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/seu-usuario/reqai.git
   cd reqai
   ```

2. **Crie e ative um ambiente virtual:**
   ```bash
   python -m venv venv
   # No Linux/macOS:
   source venv/bin/activate
   # No Windows:
   venv\Scripts\activate
   ```

3. **Instale as dependências:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure a chave de API da IA:**
   Crie um arquivo `.env` na raiz do projeto e adicione a sua chave:
   ```env
   GEMINI_API_KEY=sua_chave_aqui
   ```

5. **Execute a aplicação Streamlit:**
   ```bash
   streamlit run app.py
   ```
