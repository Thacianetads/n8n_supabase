Perfeito, já dei uma boa olhada no fluxo 👌
Aqui vai um **README.md** claro e pronto pra repositório, explicando exatamente o que esse workflow faz e como usar.

---

# 📌 Fluxo n8n – Geração Automática de Backlog de Testes (QA)

Este projeto contém um **workflow n8n** responsável por gerar automaticamente um **backlog de testes de QA** para usuários que ainda não possuem esse campo preenchido no banco de dados do **Supabase**.

O backlog é gerado por meio da **API da OpenAI**, seguindo um prompt específico voltado para a fase de **validação de um projeto de TCC**.

---

## 🚀 Objetivo do Fluxo

Automatizar o processo de:

* Buscar usuários no Supabase
* Verificar se o campo `backlog` está vazio
* Gerar um backlog de testes com **3 tarefas prioritárias**
* Atualizar automaticamente o registro do usuário no Supabase

Tudo isso de forma centralizada, rastreável e escalável via n8n.

---

## 🧠 Visão Geral do Workflow

### Etapas do fluxo:

1. **Trigger Manual**

   * Inicia o workflow ao clicar em **“Execute workflow”** no n8n.

2. **Busca os usuários**

   * Consulta a tabela `users` no Supabase e retorna todos os registros.

3. **Verifica se o backlog foi preenchido**

   * Condicional que verifica se o campo `backlog` **existe ou está vazio**.

4. **Gera o campo backlog automaticamente**

   * Usa o modelo **GPT-4o Mini** para gerar:

     * Um backlog de testes
     * Exatamente 3 tarefas
     * Focado em QA e validação de TCC
     * Formato de lista, sem textos adicionais

5. **Atualiza o campo backlog no Supabase**

   * Atualiza o campo `backlog` do usuário correspondente com o conteúdo gerado pela IA.

---

## 🛠️ Tecnologias Utilizadas

* **n8n** – Orquestração do workflow
* **Supabase** – Banco de dados
* **OpenAI API (GPT-4o Mini)** – Geração automática de backlog
* **LangChain (node OpenAI do n8n)** – Integração com LLM

---

## 🔐 Credenciais Necessárias

Antes de executar o fluxo, é necessário configurar:

* **Supabase API**

  * URL do projeto
  * API Key
* **OpenAI API**

  * Chave de API válida

As credenciais devem estar configuradas no n8n e vinculadas aos respectivos nodes.

---

## 📋 Estrutura da Tabela `users`

A tabela `users` deve conter, no mínimo, os seguintes campos:

| Campo   | Tipo       | Descrição                                |
| ------- | ---------- | ---------------------------------------- |
| id      | UUID / INT | Identificador único do usuário           |
| backlog | TEXT       | Backlog de testes gerado automaticamente |

---

## ▶️ Como Executar

1. Importe o workflow no n8n
2. Configure as credenciais do Supabase e OpenAI
3. Garanta que a tabela `users` exista
4. Clique em **Execute workflow**
5. O fluxo irá:

   * Ignorar usuários que já possuem backlog
   * Gerar backlog apenas para os que não possuem

---

## 📌 Observações Importantes

* O fluxo está configurado para execução **manual**
* O conteúdo gerado segue estritamente o prompt definido
* Cada execução pode gerar conteúdos diferentes, mantendo o mesmo formato
* Ideal para automação em projetos acadêmicos ou sistemas de apoio ao TCC

---

## ✨ Possíveis Melhorias Futuras

* Agendar execução automática (cron)
* Registrar logs de geração
* Parametrizar o tipo de backlog (QA, Dev, UX, etc.)
* Adaptar o prompt conforme o curso ou área do TCC

---

Se quiser, posso:

* Ajustar o README para **padrão acadêmico**
* Criar um **diagrama do fluxo**
* Otimizar o prompt de QA
* Transformar isso em um **template reutilizável no n8n**

Só dizer 😄


CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    phone NUMERIC,
    email TEXT,
    name TEXT,
    description TEXT, 
    job_position TEXT,
    sprint TEXT,
    backlog TEXT
);
