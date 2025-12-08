# 📋 HANDOFF - Landing Page de Diagnóstico para Metalmecânicas

**Data de criação:** 08/12/2025  
**Projeto:** Landing Page com Formulário de Diagnóstico + Integração Supabase  
**Repositório:** https://github.com/tiagoriveira/landing-metalmec-diagnostico  
**Cliente:** Tiago Ribeiro - Consultoria em Otimização de Processos

---

## 🎯 Objetivo do Projeto

Criar uma landing page com formulário de diagnóstico empresarial para capturar leads qualificados de empresas metalmecânicas. O formulário identifica gargalos operacionais, financeiros, de RH, compras e gestão, permitindo ao consultor criar propostas customizadas.

---

## 🏗️ Arquitetura Técnica

### Stack Tecnológico

- **Frontend:** HTML5, CSS3, JavaScript (Vanilla)
- **Backend/Database:** Supabase (PostgreSQL)
- **Hospedagem:** Vercel / GitHub Pages / Netlify
- **Versionamento:** Git + GitHub

### Estrutura de Arquivos

```
landing-metalmec-diagnostico/
├── index.html          # Landing page completa (HTML + CSS + JS inline)
├── vercel.json         # Configuração para deploy no Vercel
├── README.md           # Documentação do projeto
├── HANDOFF.md          # Este documento
└── .git/               # Controle de versão
```

---

## 🗄️ Banco de Dados - Supabase

### Informações de Conexão

**Projeto Supabase:** Plataforma-operacional-industrial  
**Project ID:** `omrodclevaidlijnnqeq`  
**Region:** sa-east-1 (São Paulo)  
**Status:** ACTIVE_HEALTHY

**URLs:**
- Dashboard: https://supabase.com/dashboard/project/omrodclevaidlijnnqeq
- API URL: https://omrodclevaidlijnnqeq.supabase.co
- Database Host: db.omrodclevaidlijnnqeq.supabase.co

### Credenciais (já configuradas no código)

```javascript
// Estas credenciais estão no index.html
const SUPABASE_URL = 'https://omrodclevaidlijnnqeq.supabase.co';
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im9tcm9kY2xldmFpZGxpam5ucWVxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjQ2MjUwNjUsImV4cCI6MjA4MDIwMTA2NX0.J_Xwh_0aju6-bxGGAk7PxkfIs_5Vr4_01EVFECcpOpE';
```

**⚠️ IMPORTANTE:** A `ANON_KEY` é pública e segura para uso no frontend. Nunca exponha a `SERVICE_ROLE_KEY` no código do cliente.

### Tabela: `leads_diagnostico`

**Schema completo:**

```sql
CREATE TABLE public.leads_diagnostico (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    
    -- Parte 1: Informações Gerais
    empresa TEXT NOT NULL,
    nome_cargo TEXT NOT NULL,
    email TEXT NOT NULL,
    whatsapp TEXT NOT NULL,
    funcionarios INTEGER,
    produto_servico TEXT,
    maior_desafio_inicial TEXT,
    
    -- Parte 2: Diagnóstico Operacional
    controle_producao TEXT,
    frequencia_atrasos TEXT,
    visibilidade_producao TEXT,
    medicao_qualidade TEXT,
    taxa_retrabalho TEXT,
    frequencia_quebras TEXT,
    manutencao_preventiva TEXT,
    falta_materia_prima TEXT,
    controle_estoque TEXT,
    
    -- Parte 3: Recursos Humanos
    turnover_funcionarios TEXT,
    dificuldade_mao_obra TEXT,
    treinamento_funcionarios TEXT,
    
    -- Parte 4: Compras e Fornecedores
    gestao_fornecedores TEXT,
    negociacao_fornecedores TEXT,
    problema_fornecedores TEXT,
    
    -- Parte 5: Financeiro
    calculo_custo TEXT,
    dificuldade_financeira TEXT,
    identificacao_lucratividade TEXT,
    
    -- Parte 6: Gestão e Comercial
    comunicacao_areas TEXT,
    motivo_perde_vendas TEXT,
    areas_urgentes JSONB,
    
    -- Parte 7: Perguntas Finais
    problema_unico TEXT,
    tentativas_anteriores TEXT,
    objetivo_12_meses TEXT,
    
    -- Metadata
    data_preenchimento TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    status TEXT DEFAULT 'novo',
    observacoes TEXT
);
```

**Índices criados:**
- `idx_leads_email` (email)
- `idx_leads_empresa` (empresa)
- `idx_leads_status` (status)
- `idx_leads_created_at` (created_at)

**Políticas de Segurança (RLS):**
- ✅ Inserção pública permitida (role: `anon`)
- ✅ Leitura apenas para autenticados (role: `authenticated`)
- ✅ Atualização apenas para autenticados

---

## 📝 Formulário - Estrutura

### Seções do Formulário (29 perguntas)

1. **PARTE 1: Informações Gerais** (7 campos)
   - Nome da empresa, cargo, email, WhatsApp, funcionários, produto/serviço, desafio inicial

2. **PARTE 2: Diagnóstico Operacional** (9 perguntas)
   - Controle de produção, atrasos, visibilidade, qualidade, retrabalho, quebras, manutenção, falta de material, estoque

3. **PARTE 3.5: Recursos Humanos** (3 perguntas)
   - Turnover, dificuldade de mão de obra, treinamentos

4. **PARTE 3.6: Compras e Fornecedores** (3 perguntas)
   - Gestão de fornecedores, negociação, problemas

5. **PARTE 3: Diagnóstico Financeiro** (3 perguntas)
   - Cálculo de custos, dificuldades financeiras, lucratividade

6. **PARTE 4: Gestão e Comercial** (3 perguntas)
   - Comunicação entre áreas, motivos de perda de vendas, áreas urgentes (máx 2)

7. **PARTE 5: Perguntas Finais** (3 perguntas)
   - Problema único, tentativas anteriores, objetivo 12 meses

### Validações Implementadas

- ✅ Todos os campos obrigatórios marcados com `*`
- ✅ Validação de email (HTML5)
- ✅ Validação de telefone (HTML5)
- ✅ Máximo 2 checkboxes em "áreas urgentes"
- ✅ Conversão automática de `funcionarios` para INTEGER
- ✅ Proteção contra duplo envio (botão desabilitado durante envio)
- ✅ Feedback visual: "Enviando..." → "✅ Sucesso" ou "❌ Erro"

---

## 🚀 Deploy - Instruções Completas

### Opção 1: Vercel (Recomendado)

**Passo a passo:**

1. Acesse: https://vercel.com/new
2. Faça login com GitHub
3. Clique em **"Import Git Repository"**
4. Selecione: `tiagoriveira/landing-metalmec-diagnostico`
5. Configure:
   - **Project Name:** landing-metalmec-diagnostico (ou personalizado)
   - **Framework Preset:** Other
   - **Root Directory:** `./`
   - **Build Command:** (deixe vazio)
   - **Output Directory:** `./`
   - **Install Command:** (deixe vazio)
6. Clique em **"Deploy"**
7. Aguarde 30-60 segundos
8. ✅ URL de produção: `https://landing-metalmec-diagnostico.vercel.app`

**Configurar domínio customizado (opcional):**
1. No dashboard do Vercel, vá em **Settings → Domains**
2. Adicione seu domínio (ex: `diagnostico.tiagoribeiro.com.br`)
3. Configure o DNS conforme instruções do Vercel

### Opção 2: GitHub Pages

**Passo a passo:**

1. Acesse: https://github.com/tiagoriveira/landing-metalmec-diagnostico/settings/pages
2. Em **"Source"**, selecione:
   - Branch: `master`
   - Folder: `/ (root)`
3. Clique em **"Save"**
4. Aguarde 1-2 minutos
5. ✅ URL de produção: `https://tiagoriveira.github.io/landing-metalmec-diagnostico/`

**Limitação:** GitHub Pages não suporta domínios customizados no plano free para repositórios de usuário.

### Opção 3: Netlify Drop

**Passo a passo:**

1. Baixe os arquivos do repositório
2. Acesse: https://app.netlify.com/drop
3. Arraste a pasta do projeto para a área de drop
4. Aguarde o upload
5. ✅ URL de produção: `https://random-name.netlify.app`

**Configurar domínio customizado:**
1. No dashboard do Netlify, vá em **Domain Settings**
2. Adicione seu domínio customizado

---

## 🧪 Testes - Checklist

### Testes Funcionais

- [ ] Formulário carrega corretamente
- [ ] Todos os campos estão visíveis
- [ ] Validação de campos obrigatórios funciona
- [ ] Validação de email funciona
- [ ] Limite de 2 checkboxes em "áreas urgentes" funciona
- [ ] Botão "Enviando..." aparece durante submit
- [ ] Dados são salvos no Supabase
- [ ] Mensagem de sucesso aparece após envio
- [ ] Formulário é limpo após envio bem-sucedido
- [ ] Mensagem de erro aparece em caso de falha

### Testes de Integração

- [ ] Conexão com Supabase está funcionando
- [ ] Dados aparecem na tabela `leads_diagnostico`
- [ ] Timestamp `created_at` está correto
- [ ] Campo `areas_urgentes` salva como JSONB
- [ ] Campo `funcionarios` salva como INTEGER

### Testes de Responsividade

- [ ] Desktop (1920x1080)
- [ ] Laptop (1366x768)
- [ ] Tablet (768x1024)
- [ ] Mobile (375x667)

### Testes de Navegadores

- [ ] Chrome/Edge (Chromium)
- [ ] Firefox
- [ ] Safari
- [ ] Mobile Safari (iOS)
- [ ] Chrome Mobile (Android)

---

## 📊 Como Acessar os Leads Capturados

### Via Supabase Dashboard (Interface Visual)

1. Acesse: https://supabase.com/dashboard/project/omrodclevaidlijnnqeq
2. Faça login (credenciais do cliente)
3. Vá em **Table Editor** no menu lateral
4. Selecione a tabela **`leads_diagnostico`**
5. Visualize todos os leads em tempo real

### Via SQL Query (Avançado)

**Listar todos os leads:**
```sql
SELECT * FROM leads_diagnostico 
ORDER BY created_at DESC;
```

**Listar apenas leads novos:**
```sql
SELECT * FROM leads_diagnostico 
WHERE status = 'novo'
ORDER BY created_at DESC;
```

**Buscar por empresa:**
```sql
SELECT * FROM leads_diagnostico 
WHERE empresa ILIKE '%nome_da_empresa%';
```

**Estatísticas básicas:**
```sql
SELECT 
    COUNT(*) as total_leads,
    COUNT(*) FILTER (WHERE status = 'novo') as leads_novos,
    COUNT(*) FILTER (WHERE status = 'contatado') as leads_contatados
FROM leads_diagnostico;
```

### Via API (Programático)

```javascript
// Exemplo: Buscar todos os leads
const { data, error } = await supabase
  .from('leads_diagnostico')
  .select('*')
  .order('created_at', { ascending: false });

if (error) console.error(error);
else console.log(data);
```

---

## 🔧 Manutenção e Atualizações

### Como Atualizar o Formulário

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/tiagoriveira/landing-metalmec-diagnostico.git
   cd landing-metalmec-diagnostico
   ```

2. **Edite o arquivo `index.html`**

3. **Teste localmente:**
   ```bash
   python3 -m http.server 8080
   # Acesse: http://localhost:8080
   ```

4. **Commit e push:**
   ```bash
   git add .
   git commit -m "Descrição da alteração"
   git push origin master
   ```

5. **Deploy automático:** Vercel/Netlify detectam o push e fazem deploy automaticamente

### Como Adicionar Novos Campos ao Formulário

**1. Adicionar campo no HTML:**
```html
<div class="form-group">
    <label for="novo_campo">Pergunta nova? *</label>
    <input type="text" id="novo_campo" name="novo_campo" required>
</div>
```

**2. Adicionar coluna no Supabase:**
```sql
ALTER TABLE public.leads_diagnostico
ADD COLUMN novo_campo TEXT;
```

**3. Atualizar o JavaScript (não necessário se usar FormData)**

O código atual já captura automaticamente todos os campos do formulário via `FormData`.

### Como Alterar o Design

Edite a seção `<style>` no `index.html` (linhas 7-382).

**Principais variáveis de cor:**
- Background: `#0f0f0f` e `#1a1a1a`
- Cor de destaque: `#ff6b35`
- Texto: `#e0e0e0` e `#b0b0b0`

---

## 🚨 Troubleshooting - Problemas Comuns

### Problema: Formulário não envia dados

**Possíveis causas:**
1. Credenciais do Supabase incorretas
2. Tabela não existe ou nome está errado
3. Políticas RLS bloqueando inserção
4. CORS bloqueado (improvável com Supabase)

**Solução:**
1. Abra o Console do navegador (F12)
2. Veja erros no console
3. Verifique a aba Network para ver a requisição
4. Teste as credenciais no Supabase Dashboard

### Problema: Erro "Could not insert row"

**Causa:** Violação de constraint (campo obrigatório faltando)

**Solução:**
1. Verifique se todos os campos `NOT NULL` estão sendo enviados
2. Verifique se o tipo de dado está correto (ex: INTEGER para `funcionarios`)

### Problema: Deploy não funciona

**Vercel:**
- Verifique se o repositório está público
- Verifique se o arquivo `index.html` está na raiz
- Veja os logs de build no dashboard do Vercel

**GitHub Pages:**
- Verifique se GitHub Pages está ativado nas configurações
- Aguarde 1-2 minutos após ativar
- Limpe o cache do navegador

---

## 📈 Melhorias Futuras Sugeridas

### Curto Prazo (1-2 semanas)

1. **Notificações por Email**
   - Enviar email para `tiagosantosr59@gmail.com` quando novo lead preencher
   - Usar Supabase Edge Functions + Resend/SendGrid

2. **Google Analytics / Tag Manager**
   - Rastrear conversões
   - Identificar onde os usuários abandonam o formulário

3. **Validação de WhatsApp**
   - Formatar automaticamente: (XX) XXXXX-XXXX
   - Validar número brasileiro

### Médio Prazo (1 mês)

4. **Dashboard de Análise**
   - Visualizar leads em gráficos
   - Estatísticas: taxa de conversão, principais gargalos identificados
   - Usar Chart.js ou Recharts

5. **Exportação de Dados**
   - Botão para exportar leads em CSV/Excel
   - Filtros por data, status, empresa

6. **Sistema de Status**
   - Atualizar status do lead: novo → contatado → proposta_enviada → fechado/perdido
   - Interface administrativa simples

### Longo Prazo (3+ meses)

7. **Integração com CRM**
   - Pipedrive, HubSpot, RD Station
   - Sincronização automática de leads

8. **Automação de Follow-up**
   - Email automático 24h após preenchimento
   - WhatsApp via API (Twilio, Zenvia)

9. **Múltiplos Formulários**
   - Criar versões para outros nichos (não só metalmecânicas)
   - Sistema de templates

10. **Relatório Automático em PDF**
    - Gerar diagnóstico em PDF após preenchimento
    - Enviar por email automaticamente

---

## 📞 Contatos Importantes

**Cliente:**
- Nome: Tiago Ribeiro
- Email: tiagosantosr59@gmail.com
- WhatsApp: (informar se disponível)

**Repositório GitHub:**
- URL: https://github.com/tiagoriveira/landing-metalmec-diagnostico
- Owner: tiagoriveira

**Supabase:**
- Dashboard: https://supabase.com/dashboard/project/omrodclevaidlijnnqeq
- Credenciais: (solicitar ao cliente)

---

## 📚 Recursos e Documentação

**Supabase:**
- Docs: https://supabase.com/docs
- JavaScript Client: https://supabase.com/docs/reference/javascript/introduction
- RLS Policies: https://supabase.com/docs/guides/auth/row-level-security

**Vercel:**
- Docs: https://vercel.com/docs
- Deploy: https://vercel.com/docs/deployments/overview

**GitHub Pages:**
- Docs: https://docs.github.com/en/pages

---

## ✅ Checklist de Handoff

- [x] Código versionado no GitHub
- [x] README.md criado
- [x] HANDOFF.md criado
- [x] Banco de dados configurado
- [x] Tabela criada com todos os campos
- [x] Políticas RLS configuradas
- [x] Formulário testado localmente
- [x] Integração Supabase funcionando
- [ ] Deploy em produção realizado
- [ ] Testes em produção realizados
- [ ] Cliente treinado para acessar leads
- [ ] Documentação entregue ao cliente

---

**Última atualização:** 08/12/2025  
**Versão do documento:** 1.0  
**Desenvolvedor responsável:** Manus AI Assistant
