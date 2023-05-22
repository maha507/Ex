<script>
    import { onMount } from 'svelte';
  
    // Quiz data
    const quizData = [
      {
        question: 'What is the capital of Thamilnadu?',
        options: ['Chennai', 'Bangalore', 'Hyderabad', 'Pune'],
        answer: 'Chennai',
        score: 0
      },
      {
        question: 'What is the capital of Telangana?',
        options: ['Chennai', 'Bangalore', 'Hyderabad', 'Pune'],
        answer: 'Hyderabad',
        score: 0
      },
      {
        question: 'What is the capital of Karnataka?',
        options: ['Chennai', 'Bangalore', 'Hyderabad', 'Pune'],
        answer: 'Bangalore',
        score: 0
      },
      {
        question: 'What is the capital of Maharashtra?',
        options: ['Chennai', 'Bangalore', 'Hyderabad', 'Mumbai'],
        answer: 'Mumbai',
        score: 0
      },
      {
        question: 'What is the capital of Odisha?',
        options: ['Bhuvaneswar', 'Bangalore', 'Hyderabad', 'Mumbai'],
        answer: 'Bhuvaneswar',
        score: 0
      }
    ];
  
    let selectedOptions = new Array(quizData.length).fill('');
    let totalScore = 0;
    let quizCompleted = false;
  
    function checkAnswer() {
      quizData.forEach((question, index) => {
        if (selectedOptions[index] === question.answer) {
          question.score = 1;
          totalScore++;
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
      <p>Your total score: {totalScore}/{quizData.length}</p>
    {/if}
  </main>
  
  <style>
    /* Styles omitted for brevity */
  </style>
  