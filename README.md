# Landing Page - Diagnóstico para Metalmecânicas

Landing page completa para captura de leads com formulário de diagnóstico empresarial integrado ao Supabase.

## 🎯 Funcionalidades

- ✅ Formulário completo com 29 perguntas divididas em 6 seções:
  - Informações Gerais
  - Diagnóstico Operacional (Chão de Fábrica)
  - Diagnóstico de Recursos Humanos
  - Diagnóstico de Compras e Fornecedores
  - Diagnóstico Financeiro
  - Diagnóstico de Gestão e Comercial
  - Perguntas Finais

- ✅ Integração com Supabase (banco de dados PostgreSQL)
- ✅ Validação de campos
- ✅ Design responsivo (mobile-friendly)
- ✅ Feedback visual ao usuário
- ✅ Proteção contra duplo envio

## 🗄️ Banco de Dados

**Projeto Supabase:** Plataforma-operacional-industrial
**Tabela:** `leads_diagnostico`

### Campos da tabela:

- Informações gerais: empresa, nome_cargo, email, whatsapp, funcionarios, produto_servico
- Diagnóstico operacional: controle_producao, frequencia_atrasos, visibilidade_producao, etc.
- RH: turnover_funcionarios, dificuldade_mao_obra, treinamento_funcionarios
- Compras: gestao_fornecedores, negociacao_fornecedores, problema_fornecedores
- Financeiro: calculo_custo, dificuldade_financeira, identificacao_lucratividade
- Gestão: comunicacao_areas, motivo_perde_vendas, areas_urgentes
- Metadata: data_preenchimento, created_at, status, observacoes

## 🚀 Deploy

### Opção 1: Vercel (Recomendado)

1. Acesse: https://vercel.com/new
2. Importe o repositório: `tiagoriveira/landing-metalmec-diagnostico`
3. Configure:
   - Framework: Other
   - Build Command: (vazio)
   - Output Directory: ./
4. Deploy!

### Opção 2: GitHub Pages

1. Acesse: https://github.com/tiagoriveira/landing-metalmec-diagnostico/settings/pages
2. Source: Branch `master`, pasta `/`
3. Save
4. URL: https://tiagoriveira.github.io/landing-metalmec-diagnostico/

### Opção 3: Netlify

1. Arraste a pasta do projeto para: https://app.netlify.com/drop
2. Pronto!

## 📊 Como acessar os dados capturados

### Via Supabase Dashboard:
1. Acesse: https://supabase.com/dashboard/project/omrodclevaidlijnnqeq
2. Vá em "Table Editor"
3. Selecione a tabela `leads_diagnostico`

### Via SQL:
```sql
SELECT * FROM leads_diagnostico 
ORDER BY created_at DESC;
```

### Filtrar por status:
```sql
SELECT * FROM leads_diagnostico 
WHERE status = 'novo'
ORDER BY created_at DESC;
```

## 🔧 Configuração

As credenciais do Supabase já estão configuradas no arquivo `index.html`:

```javascript
const SUPABASE_URL = 'https://omrodclevaidlijnnqeq.supabase.co';
const SUPABASE_ANON_KEY = 'eyJhbGci...'; // Chave pública
```

## 📝 Próximos Passos

1. ✅ Deploy no Vercel/GitHub Pages
2. ⏳ Testar formulário em produção
3. ⏳ Configurar domínio customizado (opcional)
4. ⏳ Criar dashboard para visualizar leads
5. ⏳ Configurar notificações por email quando novo lead chegar

## 📧 Contato

**Tiago Ribeiro**
- Email: tiagosantosr59@gmail.com
- Espírito Santo, Brasil

---

**Desenvolvido com:** HTML, CSS, JavaScript, Supabase
