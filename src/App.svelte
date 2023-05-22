<script>
    import { onMount } from 'svelte';
    import 'bootstrap/dist/css/bootstrap.min.css';
    // Quiz data
    const quizData = [
      {
        question: 'What is the capital of Thamilnadu?',
        options: ['Chennai', 'Bangalore', 'Hyderabad', 'Pune'],
        answer: 'Chennai'
      },
      {
        question: 'What is the capital of Telangana?',
        options: ['Chennai', 'Bangalore', 'Hyderabad', 'Pune'],
        answer: 'Hyderabad'
      },
      {
        question: 'What is the capital of Karnataka?',
        options: ['Chennai', 'Bangalore', 'Hyderabad', 'Pune'],
        answer: 'Bangalore'
      }
    ];
  
    let selectedOptions = new Array(quizData.length).fill('');
    let scores = new Array(quizData.length).fill(0);
    let quizCompleted = false;
  
    function checkAnswer() {
      selectedOptions.forEach((selectedOption, index) => {
        if (selectedOption === quizData[index].answer) {
          scores[index] = 1;
        }
      });
  
      quizCompleted = true;
    }
  
    onMount(() => {
      // Shuffle the quiz questions randomly
      quizData.sort(() => Math.random() - 0.5);
    });
  </script>
  
  <main>
    {#if !quizCompleted}
      <h1>Quiz App</h1>
  
      {#each quizData as question, index}
        <h2>Question {index + 1}</h2>
        <p>{question.question}</p>
  
        <ul>
          {#each question.options as option}
            <li>
              <label>
                <input
                  type="radio"
                  bind:group={selectedOptions[index]}
                  value={option}
                />
                {option}
              </label>
            </li>
          {/each}
        </ul>

      {/each}
  
      <button on:click={checkAnswer}>Finish</button>
    {:else}
      <h1>Quiz Completed!</h1>
      <p>Your total score: {scores.reduce((sum, value) => sum + value, 0)}/{scores.length}</p>
    {/if}
  </main>
  
  
  