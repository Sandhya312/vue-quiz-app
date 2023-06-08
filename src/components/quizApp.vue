<template>
  <div id="app">
    <div v-bind:class="{d_none:!display}" id="quizApp">
      <div class="questionElem" v-if="display && questions[i]">
        <h1>Q.{{ i+1}} {{ questions[i].question }}</h1>
        <h3 class="score">score- <span>{{ score }}</span>/10</h3>
      </div>
      <div class="answerElem" v-if="display && questions[i]">
        <button 
          class="btn"  
          v-for="answer in questions[i].answers" :disabled="isBtn"
          :key="answer.text" @click=" checkoutCorrectAns($event,answer.correct)"> 
          {{ answer.text }} 
        </button>
      </div>
      <button @click="nextQuestion()" v-show="isBtn" class="submit" v-if="display && questions[i]">Next</button>
    </div>
    <div v-bind:class="{d_none:display}" class="scoreBoard">
       <div class="totalScore">
        <h1>You have finished the quiz!</h1>
        <h2>You scored {{ score }} out of {{ questions.length }} </h2>
        <h3 v-if="score>5">😃 Hurrah! You have passed the test</h3>
        <h3 v-else>☹️ Oops.. You haven't pass the test. Play again!! </h3>

       </div>
       <button v-if="score<=5" @click="playAgain()" class="scoreBtn btn" >Play Again</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "quizApp",
  data() {
    return {
      questions: [
        {
          question: "What does HTML stand for?",
          answers: [
            { text: "Hyperlinks and Text Markup Language", correct: false },
            { text: "Home Tool Markup Language", correct: false },
            {
              text: "Hyperlinks and Text Markup Markup Language",
              correct: false,
            },
            { text: "Hyper Text Markup Language", correct: true },
          ],
        },
        {
          question: "Which tag is used to create a hyperlink in HTML?",
          answers: [
            { text: "img", correct: false },
            { text: "div", correct: false },
            { text: "a", correct: true },
            { text: "p", correct: false },
          ],
        },
        {
          question:
            "Which property is used to change the font size of an element in CSS?",
          answers: [
            { text: "font-weight", correct: false },
            { text: "font-size", correct: true },
            { text: "text-size", correct: false },
            { text: "size", correct: false },
          ],
        },
        {
          question: "Which tag is used to define a table in HTML?",
          answers: [
          { text: "table", correct: true },
            { text: "div", correct: false },
           
            { text: "img", correct: false },
            { text: "p", correct: false },
          ],
        },
        {
          question:
            "Which property is used to change the background color of an element in CSS?",
          answers: [
            { text: "background-image", correct: false },
            { text: "background-color", correct: true },
            { text: "background-style", correct: false },
            { text: "background", correct: false },
          ],
        },
        {
          question: "Which tag is used to define an unordered list in HTML?",
          answers: [
            { text: "ol", correct: false },
            { text: "li", correct: false },
            { text: "ul", correct: true },
            { text: "ulist", correct: false },
          ],
        },
        {
          question:
            "Which property is used to change the text color of an element in CSS?",
          answers: [
            { text: "color", correct: true },
            { text: "text-color", correct: false },
            { text: "font-color", correct: false },
            { text: "text-style", correct: false },
          ],
        },
        {
          question: "Which tag is used to define a paragraph in HTML?",
          answers: [
            { text: "p", correct: true },
            { text: "div", correct: false },
            { text: "para", correct: false },
            { text: "paragraph", correct: false },
          ],
        },
        {
          question:
            "Which property is used to change the font family of an element in CSS?",
          answers: [
            { text: "font-family", correct: true },
            { text: "text-family", correct: false },
            { text: "family", correct: false },
            { text: "font-type", correct: false },
          ],
        },
        {
          question: "In HTML, how do we insert an image?",
          answers:[
          { text: "<img src = “jtp.png” />", correct: true },
            { text: "<img href = “jtp.png” />", correct: false },
            { text: "<img link = “jtp.png” />", correct: false },
            { text: "<img link = “jtp.png” />", correct: false },
          ]
        }
      ],
      i: 0,
      display:true,
      score:0,
      isBtn:false,
    };
  },
  methods: {
    nextQuestion() {
      this.isBtn=false;
      if (this.i < this.questions.length-1) {
        this.i++;
        this.display=true;

      }else{
        this.display=false;
      }
    },
    checkoutCorrectAns(e,item){
      this.isBtn=true;
      let selectedBtn = e.target;
      console.log(selectedBtn,item);
       if(item){
        selectedBtn.classList.add("correct");
        this.score++;
       }else{
        selectedBtn.classList.add("incorrect");
       

       }

    },
    playAgain(){
      this.i = 0;
      this.display=true;
      this.score=0;
    }
  },
};
</script>

<style scoped>
#app{
  position: relative;
}
#quizApp {
 
  padding: 2%;
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 50rem;
  height: 35rem;
  background: linear-gradient(284deg, #ffc0cb69, #0000ff80);
  backdrop-filter: blur(10px);
}

.questionElem {
  height: 20%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding: 2%;
}
.answerElem {
  height: 80%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}
.btn {
  border-radius: 5px;
  height: 4.5rem;
  width: 90%;
  border: transparent;
  outline: none;
  cursor: pointer;
  text-align: center;
}
.incorrect{
  background-color: #e98892;

}
.correct{
  background-color: aquamarine ;
}
.submit {
  cursor: pointer;
  height: 10%;
  width: 10rem;
  border: transparent;
  outline: none;
  border-radius: 5rem;
  margin-bottom: 20px;
}
.scoreBoard{
  width: 50rem;
  height: 35rem;
  background: #0a021a7a;
    backdrop-filter: blur(10px);
  position:absolute;
  top: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  
}
.totalScore{
  text-align: center;
}
.scoreBtn{
  width: 50%;
}
.d_none{
  display: none !important;

}
</style>
