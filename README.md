Quero refatorar o projeto para usar React Native Web, Tamagui UI para os componentes visuais e Tailwind-RN para os estilos.

Tarefas:
Substituir todos os componentes do Material UI por equivalentes do Tamagui UI (Button, Input, Card, Sheet, etc.).
Remover todo o CSS puro e converter os estilos para Tailwind-RN, mantendo consistência visual entre plataformas.
Adaptar a estrutura do projeto para funcionar com React Native Web, mantendo a lógica e funcionalidades existentes.
Garantir que o layout continue responsivo e funcional em navegadores e dispositivos móveis.
Implementar suporte ao modo claro/escuro (dark mode) usando o sistema de temas do Tamagui.

Regras de Estilo:
Estilos como margin, padding, flex, text, bg, etc. devem ser convertidos para classes do Tailwind-RN.
Componentes visuais como Button, Card, Dialog, TextField devem ser substituídos por equivalentes do Tamagui UI, aplicando Large Border Radius.
O modo noturno deve ser ativado com base no tema do sistema ou por controle manual, usando o sistema de temas do Tamagui (ThemeProvider, useTheme, etc.).


O algoritmo **SM-2** é um modelo de repetição espaçada criado por **Piotr Wozniak** para o software **SuperMemo**, e é a base do sistema de revisão usado pelo **Anki**. Ele foi projetado para otimizar o aprendizado ao revisar informações no momento ideal — nem cedo demais (o que desperdiça tempo), nem tarde demais (quando já se esqueceu).

 ```text
function updateCard(card, quality) {
  // quality: 0-5 (0 = totalmente errado, 5 = totalmente certo)
  if (quality < 3) {
    card.repetition = 0;
    card.interval = 1;
  } else {
    if (card.repetition === 0) {
      card.interval = 1;
    } else if (card.repetition === 1) {
      card.interval = 6;
    } else {
      card.interval = Math.round(card.interval * card.efactor);
    }
    card.repetition += 1;
  }

  // Atualiza o fator de facilidade (efactor)
  card.efactor = card.efactor + (0.1 - (5 - quality) * (0.08 + (5 - quality) * 0.02));
  if (card.efactor < 1.3) {
    card.efactor = 1.3;
  }

  // Define a próxima data de revisão
  const now = new Date();
  card.nextReview = new Date(now.setDate(now.getDate() + card.interval));

  return card;
}

// Exemplo de uso
let card = {
  repetition: 0,
  interval: 0,
  efactor: 2.5,
  nextReview: null
};

card = updateCard(card, 4); // Qualidade da resposta: boa
console.log(card);
 ```




### 🧠 Como funciona o SM-2?

O SM-2 calcula quando um cartão deve ser revisado com base em:

- **Qualidade da resposta** (de 0 a 5)
- **Número de repetições bem-sucedidas**
- **Intervalo atual entre revisões**
- **Fator de facilidade (E-Factor)** — que representa o quão fácil é lembrar aquele cartão

### 📊 Fórmula principal

Quando você responde um cartão, o algoritmo:

1. **Avalia a qualidade da resposta**:
   - `0-2`: resposta ruim → o cartão volta para o início
   - `3-5`: resposta boa → o cartão avança

2. **Atualiza o intervalo**:
   - Primeira repetição: `interval = 1`
   - Segunda repetição: `interval = 6`
   - A partir da terceira: `interval = interval × efactor`

3. **Ajusta o E-Factor**:
   ```text
   efactor = efactor + (0.1 - (5 - quality) × (0.08 + (5 - quality) × 0.02))
   ```
   - O E-Factor nunca pode ser menor que **1.3**

4. **Define a próxima revisão**:
   - `nextReview = hoje + intervalo`

### 📌 Exemplo prático

Se você respondeu corretamente um cartão com qualidade 4, e ele já foi revisado duas vezes, o intervalo será multiplicado pelo E-Factor (por exemplo, 2.5), e o cartão será agendado para revisão em alguns dias.

### 🛠️ Aplicações

Esse algoritmo é ideal para:
- Flashcards de estudo (como Anki)
- Apps de memorização (idiomas, concursos, etc.)
- Sistemas de treinamento com revisão periódica

Se quiser, posso te ajudar a adaptar o SM-2 para um app em React Native ou até mesmo criar uma API simples em Node.js para gerenciar os cartões. Quer seguir por esse caminho?
