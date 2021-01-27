<template>
  <div class="animate__animated" :class="fadedOut?['animate__fadeOut','fadeIn','app2']:['still','app']">
    <button id="startBtn" v-if="!fadedOut" class="btn btn-primary" @click="fadedOut=!fadedOut">START QUIZ</button>
    <div v-if="fadedOut">
      <Questions :questions="questions[currentIndex]" :result="result"  v-on:sendResult="next"/>

    </div>
    <!-- <button class="btn btn-primary" @click="findOut">START QUIZ</button> -->
  </div>
</template>

<script>
import Questions from './components/questions';
export default {
  name: 'App',
  components: {
    Questions
  },
  methods:{
    next:function(value){
      if(this.currentIndex<this.questions.length-1){
        this.currentIndex+=1
        console.log(value)
        console.log(this.questions)
        this.script.push(value)
      }else{
        // alert("Quiz Over")
        // this.questions=""
        // for (let index = 0; index < 14; index++) {
        //   // console.log(this.script[index])
          
        // }
        this.script.push(value)
        this.result =this.script
        
        
      }
      
    }
  },
  data(){
    return{
      backGround:'./assets/background.jpg',
      fadedOut:false,
      currentIndex:0,
      result:'',
      script:[],
      questions:[
        [{
          Question: "Who was the first black woman in space?",
          Answers:{
            A:"Mae Jemison",
            B:"Carolyn Conrad",
            C:"Angela Davis",
            D:"Wangari Copeland",
          },
          CorrectAnswer: "A"
        }],
        [{
          Question: "What  was Harriet Tubman's codename?",
          Answers:{
            A:"Franklin",
            B:"Joseph",
            C:"Moses",
            D:"Carter",
          },
          CorrectAnswer:"C"
        }],
        [{
          Question: "According to Greek mythology, who was the first woman on earth?",
          Answers:{
            A:"Medea",
            B:"Aphrodite",
            C:"Pandora",
            D:"Helen of Troy",
          },
          CorrectAnswer:"C"
        }],
        [{
          Question: "Which African country was formerly known as Abyssinia?",
          Answers:{
            A:"Burkina Faso",
            B:"Gambia",
            C:"Cameroon",
            D:"Ethiopia",
          },
          CorrectAnswer:"D"
        }],
        [{
          Question: "Which country consumes the most chocolate per capita?",
          Answers:{
            A:"Netherland",
            B:"Switzerland",
            C:"France",
            D:"German",
          },
          CorrectAnswer:"B"
        }],
        [{
          Question: "Which bone are babies born without?",
          Answers:{
            A:"Elbow Bone",
            B:"Phalanges ",
            C:"Metacarpal bones",
            D:"Knee cap",
          },
          CorrectAnswer:"D"
        }],
        [{
          Question: "Which mammal has no vocal cords?",
          Answers:{
            A:"Rabbits",
            B:"Sloths ",
            C:"Manatee",
            D:"Giraffes",
          },
          CorrectAnswer:"D"
        }],
        [{
          Question: "Who was the first woman to win a Nobel Prize (1903)?",
          Answers:{
            A:"Selma Lagerlöf",
            B:"Marie Curie",
            C:"Bertha von Suttner",
            D:"Emmeline Pankhurst",
          },
          CorrectAnswer:"B"
        }],
        [{
          Question: "How many hearts does an octopus have?",
          Answers:{
            A:"One",
            B:"Two",
            C:"Three",
            D:"Four",
          },
          CorrectAnswer:"C"
        }],
        [{
          Question: "What is the loudest animal on Earth?",
          Answers:{
            A:"Sperm whale",
            B:"Lion",
            C:"Hyena",
            D:"Howler Monkeys",
          },
          CorrectAnswer:"A"
        }],
        [{
          Question: "What is the tiny piece at the end of a shoelace called?",
          Answers:{
            A:"Cord",
            B:"Aglet",
            C:"Drawstring",
            D:"Shoe Tongue",
          },
          CorrectAnswer:"B"
        }],
        [{
          Question: "What is the tallest breed of dog in the world?",
          Answers:{
            A:"The Great Dane",
            B:"German Shepherd",
            C:"Siberian Husky",
            D:"Golden Retriever",
          },
          CorrectAnswer:"A"
        }],
        [{
          Question: "How many ribs are in a human body?",
          Answers:{
            A:"22",
            B:"29",
            C:"24",
            D:"20",
          },
          CorrectAnswer:"C"
        }],
        [{
          Question: "What is the smallest ocean in the world?",
          Answers:{
            A:"The Arctic Ocean",
            B:"The Atlantic Ocean",
            C:"The Pacific Ocean",
            D:"The Indian Ocean",
          },
          CorrectAnswer:"A"
        }],
        [{
          Question: "Which planet is the hottest in the solar system?",
          Answers:{
            A:"Mercury",
            B:"Venus",
            C:"Earth",
            D:"Mars",
          },
          CorrectAnswer:"B"
        }]
      ]
    }
  }
}
</script>

<style scoped>
.app2 {
  background-image: url("./assets/question.png");
  background-attachment: fixed;
        background-position: bottom right;
        background-size: 28em;
        background-repeat:no-repeat;
  /* background-color: #fdbdb1; */

  /* background-image: url("./assets/quiz_BG.jpg"); */
  height: 100vh;
  /* display: flex;
  align-items: center;
  justify-content: center; */
}
.app {
  background-image: url("./assets/background.jpg");
  height: 100vh;
  background-size: cover;
  background-position: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
#startBtn{
  font-size: 3em;
  background: transparent;
  color: white;
}
.still{
  padding: 0;
}
.fadeIn{
  animation:fadeIn;
  animation-duration: 2s;
  /* animation-delay: 2s; */
}
</style>
