# 🔥 Guia de Configuração Firebase

## 🎯 O que é Firebase?

Firebase é um serviço do Google que fornece:
- 🗄️ Banco de dados em tempo real (Firestore)
- 🔐 Autenticação segura
- 📊 Analytics
- 📧 Notificações

**A plataforma de avaliação usa Firebase para salvar e recuperar resultados dos estudantes.**

---

## 🚀 Passo a Passo de Configuração

### PASSO 1: Criar Conta Firebase

1. Acesse: **https://firebase.google.com**
2. Clique em **"Começar"** ou **"Get Started"**
3. Faça login com sua conta Google
4. Clique em **"Criar novo projeto"**

### PASSO 2: Criar um Projeto

1. Dê um nome ao projeto: ex. `Avaliacao-2026`
2. Desmarque as opções extras (Analytics, Google Analytics)
3. Clique em **"Criar projeto"**
4. Aguarde a criação (2-3 minutos)

### PASSO 3: Obter Configurações

1. No painel do Firebase, clique em **"Web"** (ícone </>)
2. Registre seu aplicativo com um nome: ex. `Avaliacao-Bimestral`
3. Copie as credenciais que aparecer:

```javascript
const firebaseConfig = {
  apiKey: "XXXXXXXXXXXXXXXXXXXXXXXXXXX",
  authDomain: "seu-projeto.firebaseapp.com",
  projectId: "seu-projeto",
  storageBucket: "seu-projeto.appspot.com",
  messagingSenderId: "XXXXXXXXXXXXX",
  appId: "1:XXXXXXXXXXXXX:web:XXXXXXXXXXXXX"
};
```

### PASSO 4: Configurar Firestore

1. No menu esquerdo, clique em **"Firestore Database"**
2. Clique em **"Criar banco de dados"**
3. Selecione **"Começar no modo de testes"**
4. Escolha uma região próxima: ex. `southamerica-east1` (São Paulo)
5. Clique em **"Ativar"**

### PASSO 5: Configurar Regras de Segurança

Depois que o Firestore for criado:

1. Vá para **"Regras"**
2. Substitua todo o conteúdo por:

```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Permitir leitura e escrita para todos (modo de testes)
    match /{document=**} {
      allow read, write: if true;
    }
    
    // Para produção, use autenticação:
    // match /{document=**} {
    //   allow read, write: if request.auth != null;
    // }
  }
}
```

3. Clique em **"Publicar"**

### PASSO 6: Integrar no HTML

1. Abra o arquivo `index_completo.html`
2. Procure por `const firebaseConfig` (por volta da linha 477)
3. Substitua as credenciais pelas suas:

```javascript
const firebaseConfig = {
  apiKey: "COLE_SUA_API_KEY_AQUI",
  authDomain: "COLE_SEU_AUTH_DOMAIN",
  projectId: "COLE_SEU_PROJECT_ID",
  storageBucket: "COLE_SEU_STORAGE_BUCKET",
  messagingSenderId: "COLE_SEU_MESSAGING_SENDER_ID",
  appId: "COLE_SEU_APP_ID"
};
```

4. Salve o arquivo

---

## ✅ Testando a Configuração

### Test 1: Realizar uma Avaliação
1. Abra `index_completo.html`
2. Preencha os dados do estudante
3. Responda as questões
4. Clique em "Finalizar Avaliação"

### Test 2: Verificar no Firestore
1. Volte ao console Firebase
2. Vá para **"Firestore Database"**
3. Procure pela coleção **"resultados"**
4. Você verá os documentos com os dados do teste

### Test 3: Consultar Resultados
1. Na plataforma, clique em **"Meus Resultados"**
2. Clique em **"Buscar"**
3. Você verá o registro que acabou de criar

---

## 🔒 Segurança em Produção

⚠️ **IMPORTANTE**: As regras de teste NÃO são seguras para produção!

### Para Ambiente de Produção:

1. **Ative a Autenticação**:
   - Menu > Autenticação
   - Clique em "Ativar Google Sign-in"
   - Configure e ative

2. **Atualize as Regras Firestore**:
```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Apenas usuários autenticados podem ler e escrever
    match /resultados/{document=**} {
      allow read, write: if request.auth != null;
    }
    
    // Escolas podem ler todos os resultados da sua escola
    match /resultados/{document=**} {
      allow read: if request.auth.token.escola == resource.data.escola;
    }
  }
}
```

3. **Configure Variáveis de Ambiente**:
   - Nunca deixe credenciais no código em produção
   - Use variáveis de ambiente

---

## 📊 Estrutura do Banco de Dados

### Coleção: `resultados`
```
resultados/
├── documento1/
│   ├── nome: "João Silva"
│   ├── matricula: "2024001"
│   ├── escola: "EMEF Exemplo"
│   ├── serie: "6"
│   ├── disciplina: "lp"
│   ├── turma: "A"
│   ├── acertos: 18
│   ├── total: 25
│   ├── percentual: 72
│   ├── respostas: [...]
│   ├── timestamp: 2026-05-25T10:30:00Z
│   └── dataHora: "25/05/2026 10:30:00"
│
└── documento2/
    └── ...
```

---

## 🐛 Resolução de Problemas

### Problema: "Firebase is not defined"
**Solução**: Verifique se os scripts do Firebase estão carregados corretamente
```html
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
```

### Problema: "Permission denied" ao salvar
**Solução**: Verifique as regras de segurança do Firestore
- Modo teste: `allow read, write: if true;`
- Modo produção: Ative autenticação

### Problema: Resultados não aparecem
**Solução**:
1. Verifique se a coleção "resultados" foi criada no Firestore
2. Limpe o cache do navegador (Ctrl+Shift+Delete)
3. Abra o Console (F12) e verifique erros

### Problema: Dados aparecendo como "undefined"
**Solução**: Aguarde o carregamento do Firebase antes de usar

---

## 💰 Custos Firebase

### Plano Gratuito (Spark)
- ✅ Grátis para testar
- ❌ Não serve para produção
- ❌ Sem autenticação
- ❌ Sem segurança

### Plano Pago (Blaze - pay-as-you-go)
- 💲 US$0 até certo limite
- ✅ Ideal para produção
- ✅ Escalável
- ✅ Suporte

**Para um projeto educacional com 500-1000 estudantes:**
- Custo estimado: US$0-10/mês

---

## 📱 Exemplos de Consultas

### Buscar resultados de um estudante
```javascript
const snap = await db.collection('resultados')
  .where('matricula', '==', '2024001')
  .get();
```

### Buscar resultados por escola
```javascript
const snap = await db.collection('resultados')
  .where('escola', '==', 'EMEF Exemplo')
  .get();
```

### Buscar resultados de uma série
```javascript
const snap = await db.collection('resultados')
  .where('serie', '==', '6')
  .where('disciplina', '==', 'lp')
  .get();
```

### Ordenar por data (mais recentes primeiro)
```javascript
const snap = await db.collection('resultados')
  .orderBy('timestamp', 'desc')
  .limit(10)
  .get();
```

---

## 🔧 Customizações Avançadas

### Adicionar Mais Campos
Se quiser adicionar mais informações, modifique o código:

```javascript
await db.collection('resultados').add({
  // Campos existentes...
  nome: estudante.nome,
  matricula: estudante.matricula,
  
  // Novos campos
  professor: "Nome do Professor",
  periodo: "Matutino",
  observacoes: "Observações do professor",
  
  timestamp: firebase.firestore.FieldValue.serverTimestamp(),
});
```

### Criar Subcoleções
Para estrutura mais complexa:

```javascript
// Adicionar resposta individual
await db.collection('resultados')
  .doc(docId)
  .collection('respostas')
  .add({
    questao: 1,
    resposta: 'a',
    correta: 'b',
    acertou: false
  });
```

---

## 📚 Recursos Adicionais

- **Firebase Docs**: https://firebase.google.com/docs
- **Firestore Guide**: https://firebase.google.com/docs/firestore
- **Video Tutorial**: https://www.youtube.com/watch?v=lw7DWV8U_ro

---

## ✅ Checklist Final

- [ ] Criou conta Firebase
- [ ] Criou novo projeto
- [ ] Obteve credenciais
- [ ] Ativou Firestore
- [ ] Configurou regras de segurança
- [ ] Atualizou credenciais no HTML
- [ ] Testou criando um resultado
- [ ] Verificou no Firestore
- [ ] Testou buscar resultados

---

**Se tudo estiver funcionando: ✅ Parabéns!**

Você pode agora usar a plataforma com armazenamento completo em nuvem!

---

**Versão**: 1.0  
**Atualizado**: 25 de maio de 2026  
**Status**: ✅ Completo
