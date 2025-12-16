# 🧨 ConflictLab – Laboratório de Conflitos Pesados em Staging

## 📋 Objetivo do Exercício

Este projeto foi criado **exclusivamente para estudo**, com foco total em **conflitos de merge na branch `staging`**.

Aqui você irá praticar:

* Merges simultâneos de várias branches de funcionalidades
* Conflitos severos no **mesmo arquivo**
* Resolução manual de conflitos em JSON e JavaScript
* Decisões de integração (o que manter, adaptar ou descartar)
* Mentalidade de *integrador / tech lead*

> ⚠️ **Atenção:** este exercício foi projetado para quebrar o código várias vezes. Isso é intencional.

---

## 🎓 Público-Alvo

* Estudantes de Git/Gitflow
* Desenvolvedores iniciantes e intermediários
* Quem quer perder o medo de conflitos em merge

---

## 🏗️ Estrutura Inicial do Projeto

```
project/
├── config/
│   └── app.config.json
├── src/
│   ├── core/
│   │   └── app.js
│   ├── services/
│   │   └── logger.js
│   └── features/
│       └── README.md
└── README.md
```

### 📄 config/app.config.json (Base)

```json
{
  "appName": "ConflictLab",
  "version": "1.0.0",
  "environment": "staging"
}
```

### 📄 src/core/app.js (Base)

```js
function startApp() {
    console.log("App iniciado");
}

startApp();
```

---

## 🎭 Simulação de Equipes (Branches)

Cada branch representa uma **feature crítica** que será integrada em `staging`.

| Branch             | Feature       |
| ------------------ | ------------- |
| feat/auth          | Autenticação  |
| feat/payments      | Pagamentos    |
| feat/notifications | Notificações  |
| feat/analytics     | Analytics     |
| feat/settings      | Configurações |

⚠️ **Todas as branches alteram os mesmos arquivos**, propositalmente.

---

## 🚀 RODADA 1: Criação das Branches

Todas as branches devem ser criadas a partir da `main`:

```bash
git checkout main

git checkout -b feat/auth
git checkout -b feat/payments
git checkout -b feat/notifications
git checkout -b feat/analytics
git checkout -b feat/settings
```

---

## 🧩 RODADA 2: Implementações (INTENCIONALMENTE CONFLITANTES)

Cada branch deve editar:

* `config/app.config.json`
* `src/core/app.js`

### 🔐 feat/auth

json
```json
{
  "auth": {
    "jwt": true,
    "tokenExpiration": 3600
  }
}
```
app.js
```js

function startApp() {
    console.log("Auth carregado");
}
```

---

### 💳 feat/payments

json
```json
{
  "payments": {
    "provider": "stripe",
    "currency": "BRL"
  }
}
```
app.js
```js
function startApp() {
    console.log("Payments inicializados");
}
```

---

### 🔔 feat/notifications

json
```json
{
  "notifications": {
    "email": true,
    "sms": false
  }
}
```
app.js
```js
function startApp() {
    console.log("Notificações ativas");
}
```

---

### 📊 feat/analytics

json
```json
{
  "analytics": {
    "enabled": true,
    "provider": "GA"
  }
}
```
app.js
```js
function startApp() {
    console.log("Analytics ativo");
}
```

---

### ⚙️ feat/settings

json
```Json
{
  "settings": {
    "darkMode": true,
    "language": "pt-BR"
  }
}
```
app.js
```js
function startApp() {
    console.log("Settings carregados");
}
```

---

## 🔥 RODADA 3: Merge Caótico em Staging

Crie a branch `staging`:
bash
```bash
git checkout -b staging
```

Agora faça o merge **sem resolver nada automaticamente**:

bash
```bash
git merge feat/auth
git merge feat/payments
git merge feat/notifications
git merge feat/analytics
git merge feat/settings

```

💥 **Conflitos esperados em:**

* `config/app.config.json`
* `src/core/app.js`

---

## 🧠 RODADA 4: Resolução dos Conflitos

### ✅ Resultado Esperado – app.config.json

O arquivo final deve conter **todas as configurações consolidadas**:

json
```json
{
  "appName": "ConflictLab",
  "version": "1.0.0",
  "environment": "staging",
  "auth": {
    "jwt": true,
    "tokenExpiration": 3600
  },
  "payments": {
    "provider": "stripe",
    "currency": "BRL"
  },
  "notifications": {
    "email": true,
    "sms": false
  },
  "analytics": {
    "enabled": true,
    "provider": "GA"
  },
  "settings": {
    "darkMode": true,
    "language": "pt-BR"
  }
}
```

---

### ✅ Resultado Esperado – app.js

O conflito **não deve ser resolvido escolhendo apenas uma versão**.

Refatore para integrar todas as intenções:

```javascript
function startApp() {
    console.log("Auth carregado");
    console.log("Payments inicializados");
    console.log("Notificações ativas");
    console.log("Analytics ativo");
    console.log("Settings carregados");
}

startApp();
```

---

## 🧪 MODO HARDCORE (Opcional)

Introduza novos problemas:

* Uma branch altera `version` para `2.0.0`
* Outra remove `environment`
* Duas branches usam chaves diferentes (`analytics` vs `metrics`)

👉 Decida conscientemente o que entra no código final.

---

## 🎯 Aprendizados Esperados

* [ ] Resolver conflitos múltiplos no mesmo arquivo
* [ ] Ler conflitos com calma e intenção
* [ ] Unificar configurações sem perder dados
* [ ] Entender que merge é decisão técnica
* [ ] Pensar como integrador de sistemas

---

## 🏁 Finalização

Após resolver todos os conflitos:

```bash
git add .
git commit -m "merge(staging): resolve conflitos pesados entre features"
```

Se quiser, faça o merge para `main` como simulação de produção.

---

🚀 **Este laboratório não é sobre velocidade, é sobre domínio de conflitos.**
