<template>
  <div>
    <div v-if="isQuizStarted">
      <div>
        <span>Time: </span>{{time}}
      </div>
      <h4>{{operandLeft}} {{operator}} {{operandRight}}</h4>

      <button
        @click="selectAnswer(answer)"
        v-for="(answer, index) of answers"
        :key="index"
      ><p>{{answer}}</p></button>
    </div>

    <div v-if="!isQuizStarted">
      <button @click="startQuiz"><p>Start</p></button>
    </div>
    <button @click="$emit('onBack')"><p>Back</p></button>
  </div>
</template>

<script>
export default {
  props: ["operator"],
  data() {
    return {
      isQuizStarted: false,
      operandLeft: null,
      operandRight: null,
      answers: [],
      expectedAnswer: null,
      time: 60
    };
  },
  methods: {
    selectAnswer(answerSelected) {
      if (answerSelected !== this.expectedAnswer) {
        alert("WRONG ANSWER");
      }
      this.time = 60;
      this.startQuiz();
    },
    Timer(){
      if(this.time){
        return setTimeout(()=>{
          --this.time
          this.Timer()
        }, 1000)
      }else{
        alert("TIME IS OUT");
        this.time = 60;
        this.Timer();
        this.startQuiz();
      }
      
    },
    startQuiz() {
      this.isQuizStarted = true;
      this.operandLeft = parseInt(Math.random() * 13);
      this.operandRight = parseInt(Math.random() * 13);
      const methods = {
        "+": (a, b) => a + b,
        "-": (a, b) => a - b,
        "/": (a, b) => a / b,
        "*": (a, b) => a * b
      };
      const methodToUse = methods[this.operator];
      this.answers = [];
      this.answers.push(methodToUse(this.operandLeft, this.operandRight + 1));
      this.answers.push(methodToUse(this.operandLeft + 1, this.operandRight));
      this.answers.push(
        methodToUse(this.operandLeft + 1, this.operandRight + 1)
      );
      this.answers.push(
        methodToUse(this.operandLeft - 1, this.operandRight + 1)
      );
      this.answers.push(methodToUse(this.operandLeft, this.operandRight - 1));
      const expectedAnswer = methodToUse(this.operandLeft, this.operandRight);
      this.answers[
        parseInt(Math.random() * this.answers.length)
      ] = expectedAnswer;
      this.expectedAnswer = expectedAnswer;
    }
    
  },
  mounted(){
    this.Timer();
  }
};
</script>
