---

# 📌 Fluxo n8n – Geração Automática de Backlog de Tarefas

Este projeto contém um **workflow n8n** responsável por gerar automaticamente através da IA um **backlog com tarefas pra fazer durante o TCC no IFPR Colombo** para usuários que ainda não possuem esse campo preenchido no banco de dados do **Supabase**.
.

---

## 🚀 Objetivo do Fluxo

Automatizar o processo de:

* Buscar usuários no Supabase
* Verificar se o campo `backlog` está vazio
* Gerar um backlog com **3 tarefas prioritárias**
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

   * Usa o modelo **GPT-4o Mini** para gerar backlog de 3 tarefas pra executar durante o tcc.

5. **Atualiza o campo backlog no Supabase**

   * Atualiza o campo `backlog` do usuário correspondente com o conteúdo gerado pela IA.

---

## 🛠️ Tecnologias Utilizadas

* **n8n** – Orquestração do workflow
* **Supabase** – Banco de dados
* **OpenAI API (GPT-4o Mini)** – Geração automática de backlog
* **LangChain (node OpenAI do n8n)** – Integração com LLM

---

## 📋 Estrutura da Tabela `users`

A tabela `users` deve conter, no mínimo, os seguintes campos:

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








