<script>
    // Lista de preguntas con opciones y la respuesta correcta
    let questions = [
      { 
        question: "¿Cuál es la capital de Francia?",
        options: ["Madrid", "Roma", "París", "Berlín"],
        answer: 2 
      },
      { 
        question: "¿Cuál es el lenguaje usado para la web?",
        options: ["Python", "JavaScript", "C++", "Ruby"],
        answer: 1 
      },
      { 
        question: "¿Cuántos planetas hay en el sistema solar?",
        options: ["7", "8", "9", "10"],
        answer: 1 
      }
    ];
  
    // Variables para llevar el progreso del juego
    let currentQuestionIndex = 0; 
    let score = 0; 
    let gameEnded = false; 
    let selectedOption = null; 
  
    // Función para manejar la respuesta elegida
    function handleAnswer(optionIndex) {
      selectedOption = optionIndex;
      if (selectedOption === questions[currentQuestionIndex].answer) {
        score++; 
      }
      
      // Pasar a la siguiente pregunta o terminar el juego
      if (currentQuestionIndex < questions.length - 1) {
        currentQuestionIndex++;
        selectedOption = null; 
      } else {
        gameEnded = true; 
      }
    }
  
    // Reiniciar el juego
    function restartGame() {
      currentQuestionIndex = 0;
      score = 0;
      gameEnded = false;
      selectedOption = null;
    }
  </script>
  
  <!-- Mostrar preguntas -->
  {#if !gameEnded}
    <div>
      <h2>Pregunta {currentQuestionIndex + 1}</h2>
      <p>{questions[currentQuestionIndex].question}</p>
      <ul>
        {#each questions[currentQuestionIndex].options as option, index}
          <li>
            <button on:click={() => handleAnswer(index)}>
              {option}
            </button>
          </li>
        {/each}
      </ul>
    </div>
  {:else}
    <!-- Mostrar resultados -->
    <div>
      <h2>¡Juego terminado!</h2>
      <p>Puntaje: {score} de {questions.length}</p>
      {#if score === questions.length}
        <p>¡Perfecto! Lo lograste.</p>
      {:else if score > questions.length / 2}
        <p>¡Buen trabajo!</p>
      {:else}
        <p>¡Inténtalo de nuevo!</p>
      {/if}
      <button on:click={restartGame}>Jugar de nuevo</button>
    </div>
  {/if}
  
  <style>
    div {
      text-align: center;
      padding: 20px;
    }
    button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 16px;
    }
  </style>