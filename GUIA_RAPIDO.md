# 🚀 Guia de Início Rápido

## Para Começar em 5 Minutos

### ✅ Passo 1: Preparar o Ambiente
```bash
# Se desejar extrair questões novamente dos DOCX:
python3 extrair_questoes.py
```

### ✅ Passo 2: Abrir a Plataforma
1. Abra o arquivo `index_completo.html` em um navegador web
2. Ou hospede em um servidor web (Apache, Nginx, etc)

### ✅ Passo 3: Configurar Firebase (Opcional)
Se quiser salvar resultados em banco de dados:
1. Crie uma conta em https://firebase.google.com
2. Crie um novo projeto
3. Copie as credenciais
4. Cole no HTML (linha ~477)

---

## 📱 Testando Localmente

### No Windows
```cmd
# Abra o prompt de comando e execute:
python -m http.server 8000
# Depois acesse: http://localhost:8000/index_completo.html
```

### No Mac/Linux
```bash
# Terminal:
python3 -m http.server 8000
# Depois acesse: http://localhost:8000/index_completo.html
```

---

## 🎮 Usando a Plataforma

### Para Estudantes
1. Clique em **"Realizar Atividade"**
2. Preencha seus dados (Nome, Matrícula, Escola, etc)
3. Selecione a Série e Disciplina
4. Clique em **"Iniciar Atividade"**
5. Responda as questões
6. Clique em **"Finalizar Avaliação"**
7. Veja seu resultado com percentual de acertos

### Para Professores/Administradores
1. Clique em **"Meus Resultados"** para ver resultados individuais
2. Use os filtros para buscar por aluno, escola ou série
3. Clique em **"Administrador"** para ver o dashboard geral

---

## 📊 Dados Disponíveis

### Língua Portuguesa
- **6º Ano**: 5 questões sobre leitura e compreensão de textos
- **9º Ano**: 5 questões sobre análise de crônicas e literatura
- **3ª Série**: 5 questões sobre interpretação textual

### Matemática
- **6º Ano**: 4 questões (conteúdo variado)
- **9º Ano**: 3 questões (conteúdo variado)
- **3ª Série**: 6 questões (conteúdo variado)

---

## ⚙️ Customizações Comuns

### Mudar Cores do Tema
Abra o arquivo HTML e procure por `<style>`:
```css
/* Cor principal (azul) */
color: #0a2f6c;

/* Mude para sua cor desejada */
color: #seu_codigo_hex;
```

### Adicionar Novas Questões
1. Modifique o arquivo DOCX original
2. Execute: `python3 extrair_questoes.py`
3. Atualize o HTML com o novo `questoes.json`

### Mudar Nome da Instituição
Procure por "URE-CAIEIRAS" e "Avaliação Bimestral" no HTML e customize conforme necessário.

---

## 🐛 Solução de Problemas

### Questões não aparecem
- ✓ Verifique se está usando `index_completo.html`
- ✓ Limpe o cache do navegador (Ctrl+Shift+Delete)
- ✓ Verifique o console (F12 > Console) para erros

### Firebase não salva dados
- ✓ Verifique as credenciais no código
- ✓ Ative o Firestore no console do Firebase
- ✓ Configure as regras de segurança corretamente

### Página lenta no mobile
- ✓ Reduza o número de gráficos/animações
- ✓ Otimize imagens
- ✓ Use compressão gzip no servidor

---

## 📈 Acompanhando Resultados

### Dashboard
- **KPI 1**: Total de atividades realizadas
- **KPI 2**: Média de acertos percentual
- **KPI 3**: Quantidade de estudantes únicos
- **KPI 4**: Taxa de aprovação (>60%)

### Gráfico
Mostra distribuição dos estudantes por faixa de desempenho:
- 0-20%: Crítico (vermelho)
- 21-40%: Baixo (laranja)
- 41-60%: Regular (amarelo)
- 61-80%: Bom (verde claro)
- 81-100%: Excelente (verde)

---

## 💾 Backup de Dados

### Exportar Resultados
1. Vá para **"Administrador"**
2. Clique em **"Exportar para CSV"** (para planilha)
3. Clique em **"Exportar Relatório PDF"** (para relatório)

---

## 🔗 Links Úteis

- Firebase: https://firebase.google.com
- MDN JavaScript: https://developer.mozilla.org/pt-BR/
- Chart.js (Gráficos): https://www.chartjs.org
- Font Awesome (Ícones): https://fontawesome.com

---

## 📞 Contato de Suporte

Para dúvidas ou problemas, consulte:
- Documentação Firebase
- Console do navegador (F12)
- Repositório do projeto

---

**Versão**: 2.0  
**Atualizado**: 25 de maio de 2026
