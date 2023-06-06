<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions 
        v-if="questionsAnswered < questions.length" 
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>
    
    <button 
      type="button" 
      class="reset-btn" 
      @click.prevent="reset" 
      v-if="this.questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Questions from './components/Questions.vue'
import Result from './components/Result.vue'

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
            {
                q: 'What is the capital of Ukraine?', 
                answers: [
                    {
                        text: 'Kyiv',
                        is_correct: true
                    },
                    {
                        text: 'Warsaw',
                        is_correct: false 
                    },
                    {
                        text: 'Madrid',
                        is_correct: false 
                    },
                    {
                        text: 'Detroit',
                        is_correct: false 
                    }
                ] 
            },
            { 
                q: 'What`s the main river of Ukraine?', 
                answers: [
                    {
                        text: 'Danube',
                        is_correct: false
                    },
                    {
                        text: 'Rhine',
                        is_correct: false 
                    },
                    {
                        text: 'Dnipro',
                        is_correct: true 
                    },
                    {
                        text: 'Loire',
                        is_correct: false 
                    }
                ] 
            },
            { 
                q: 'What`s the most famous Ukrainian soup', 
                answers: [
                    {
                        text: 'Żurek',
                        is_correct: false
                    },
                    {
                        text: 'Borscht',
                        is_correct: true 
                    },
                    {
                        text: 'Gaspacho',
                        is_correct: false 
                    }
                ] 
            },
        ],
        results: [
            {
                min: 0,
                max: 2,
                title: "Try again!",
                desc: "Do a little more studying and you may succeed!"
            },
            {
                min: 3,
                max: 3,
                title: "Wow, you're a genius!",
                desc: "Studying has definitely paid off for you!"
            }
        ]
    }
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style>

</style>
