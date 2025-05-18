# 🤖 MEI Assist: Assistente Inteligente para Microempreendedores Individuais

> Projeto submetido para a premiação da **Imersão IA 2025 - Alura & Google**

## 💡 Visão Geral
O **MEI Assist** é um assistente inteligente com foco em **educação financeira e suporte prático** para **MEIs (Microempreendedores Individuais)** brasileiros. Desenvolvido com a mais recente tecnologia da Google, ele é capaz de entender comandos em linguagem natural, interagir por meio de agentes especializados e ajudar o usuário a:

- Registrar entradas e saídas financeiras;
- Recuperação de histórico;
- Oferecer educação financeira em linguagem acessível.

## 🌟 Destaques do Projeto

| Critério      | Destaque |
|---------------|----------|
| **Utilidade** | Resolve um problema real enfrentado por milhões de MEIs no Brasil: falta de orientação simples e precisa sobre suas finanças e obrigações. |
| **Criatividade** | Utiliza um modelo multi-agente que atua como um "concierge de finanças do MEI", com routing automático para especialistas internos. |
| **Eficácia** | Capaz de compreender intenções complexas, como "quanto gastei este mês com insumos?" e gerar respostas contextualizadas com base no histórico. |

---

## ⚙️ Tecnologias e Ferramentas Utilizadas neste MVP

| Tecnologia | Função |
|------------|--------|
| **Google AI Gemini SDK (v1.5)** | Criação do modelo de chat com histórico e suporte a function calling |
| **Python 3.10+** | Lógica de negócio e manipulação de dados |
| **Jupyter Notebook (Colab)** | Interface de execução e apresentação |
| **Agents & Tools Pattern** | Roteamento inteligente de mensagens entre agentes especialistas |
| **LangChain-like abstraction** | Design baseado em arquiteturas modernas de IA interativa |

---

## 📊 Estrutura do Projeto

```
mei-assist/
├── Assistente_MEI.ipynb        # Notebook principal com os agentes e demonstração interativa
├── Motivacao Assistente MEI.md # Documento explicativo sobre os porquês do projeto
├── Testes Realizados.md        # Blocos de validação de comportamento
```

---

## 🔧 Testes e Qualidade
- Testes manuais com diferentes perfis de usuário e perguntas variadas
- Casos contemplados:
  - Registro de entradas e saídas
  - Recuperação de histórico
  - Perguntas sobre gestão financeira com foco no MEI
  - Explicações conceituais com linguagem acessível

Os testes garantiram consistência no comportamento dos agentes e robustez nos comandos suportados.

---

## 🚀 Possíveis Evoluções
- Integração com Google Calendar para lembretes fiscais
- Dashboard com gráficos interativos de gastos e receitas
- Treinamento com dados reais anonimizados
- Publicação como aplicativo web/mobile

---

## 🎓 Sobre o Autor
**Leandro Rocha Cherubini** — Especialista em integrações SAP e entusiasta em IA. Apaixonado por desenvolver ferramentas que resolvem problemas reais com alto padrão técnico e foco na experiência do usuário final.

---

## 🌟 Submissão Oficial
Este projeto foi submetido como parte da participação na **Imersão IA 2025 da Alura + Google**, atendendo aos seguintes requisitos:

- [x] Relacionado à Aula 4 (Chatbots) e Aula 5 (Agentes)
- [x] Hospedado no GitHub
- [x] Documentado e funcional
- [x] Foco em utilidade, criatividade, eficácia e apresentação

> Obrigado por visitar o projeto! Se você gostou, “estrela” o repositório e compartilhe com a comunidade! 🌟
