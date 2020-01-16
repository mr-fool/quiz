<template>
    <div class="question-bux-container">
        <b-jumbotron>

        <template v-slot:lead>
            {{currentQuestion.question}}
        </template>

        <hr class="my-4">


        <b-list-group>
            
            <b-list-group-item
                v-for="(answer, index) in answers"
                :key="index"
                @click="selectAnswer(index)"
                :class="[selectedIndex === index ? 'selected' : '']"
            >
                 {{answer}}
            </b-list-group-item>


        </b-list-group>


        <b-button variant="primary" href="#">Submit</b-button>
        <b-button @click="next" variant="success" href="#">Next</b-button>
        
        </b-jumbotron>
  </div>
</template>
<script>
    import _ from 'lodash'
    export default {
        props: {
            currentQuestion: Object,
            next: Function
        },
        data() {
            return {
                selectedIndex: null,
                shuffledAnswers: []
            }
        },
        computed: {
            answers() {
                let answers = [...this.currentQuestion.incorrect_answers];
                answers.push(this.currentQuestion.correct_answer);
                return answers;
            }
        },
        watch: {
            currentQuestion() {
                this.selectedIndex = null
                this.shuffleAnswers()
            }
        },
        methods: {
          selectAnswer(index) {
              this.selectedIndex = index;
          },
          shuffleAnswers() {
              let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
              this.shuffleAnswers = _.shuffle(answers);

          } 
        }

    }

</script>
<style scoped> 
.list-group {
    margin-bottom: 15 px;
}

.list-group-item:hover {
    background: #EEE;
    cursor: pointer;
}

.btn {
    margin: 0 5px;
}
.selected {
    background-color: aqua;
}
.correct{
    background-color: green;
}
.incorrect {
    background-color: red;
}

</style>