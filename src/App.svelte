<script>
    import 'bootstrap/dist/css/bootstrap.min.css';
    // Quiz data
    const quizData = [
      {
        question: 'What is the capital of Thamilnadu?',
        options: ['A. Chennai', 'B. Bangalore', 'C. Hyderabad', 'D. Pune'],
        answer: 'A. Chennai'
      },
      {
        question: 'What is the capital of Telangana?',
        options: ['A. Chennai', 'B. Bangalore', 'C. Hyderabad', 'D. Pune'],
        answer: 'C. Hyderabad'
      },
      {
        question: 'What is the capital of Karnataka?',
        options: ['A. Chennai', 'B. Bangalore', 'C. Hyderabad', 'D. Pune'],
        answer: 'B. Bangalore'
      },
      {
        question: 'What is the capital of Maharashtra?',
        options: ['A. Chennai', 'B. Bangalore', 'C. Hyderabad', 'D. Mumbai'],
        answer: 'D. Mumbai'
      },
      {
        question: 'What is the capital of Odisha?',
        options: ['A. Chennai', 'B. Bhuvaneswar', 'C. Hyderabad', 'D. Pune'],
        answer: 'B. Bhuvaneswar'
      }
    ];
  
    let selectedOptions = new Array(quizData.length).fill('');
    let scores = new Array(quizData.length).fill(0);
    let quizCompleted = false;
  
    function checkAnswer() {
      // Check if all questions have been answered
      if (selectedOptions.includes('')) {
        alert('Please answer all the questions before finishing the quiz.');
        return;
      }
  
      selectedOptions.forEach((selectedOption, index) => {
        if (selectedOption === quizData[index].answer) {
          scores[index] = 1;
        }
      });
  
      quizCompleted = true;
    }
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
        <p>Score: {scores[index]}/{scores.length}</p>
      {/each}
  
      <button on:click={checkAnswer}>Finish</button>
    {:else}
      <h1>Quiz Completed!</h1>
      <p>Your total score: {scores.reduce((sum, value) => sum + value, 0)}/{scores.length}</p>
    {/if}
  </main>
  