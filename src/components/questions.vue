<template lang="">
<div>
    <div v-if="!result">
        <div class="card col-md-6 mx-auto mt-5 pt-5 pr-5 pl-5 pb-1" style="background-color: #fdbdb1">
            <div v-for="(item,index) in questions" :key="index">
                <!-- {{ item.CorrectAnswer }} -->
                <p class="text-center h1"><b>{{ item.Question }}</b></p>
                    <div class="row">
                        <div class="col-md-6 mt-5" v-for="(option,id) in item.Answers" :key="id">
                            <!-- {{id}} -->
                            <button class="btn btn-lg bg-white p-3 w-100 ansBtn" :disabled="answered" :class="clickedAnswer==id?border:''" @click="verify(id)">{{id}}) {{option}}</button>
                        </div>
                    </div>  
                <p class="text-center mt-5" style="font-weight:500" :class="markStatus?'text-success':'text-danger'">{{mark}}</p>
                <p v-if="!markStatus" class="text-center">Correct Option is {{item.CorrectAnswer}}</p> 
            </div>
        </div>
        <div class="mx-auto">
        <button class="btn btn-primary btn-lg bg-dark d-block mx-auto mt-2" @click="next" :disabled="nextDisabled">NEXT</button>
      </div>
        <!-- <img src="../assets/questions_BG.png" /> -->
    </div>
    <div v-if="result" style="background-color:white">
    <p class="text-center col-md-7 h2">QUIZ RESULT</p>
    <p class="text-right col-md-7">Score:{{total}}/{{result.length}}</p>
    <div class="row">
        <div class="col-md-7" v-for="(slip,index) in result" :key="index">
            <div class="alert" :class="slip.mark=='Correct Answer'?'alert-success':'alert-danger'" role="alert">
                <!-- {{slip}} -->
                Question {{index+1}}: {{slip.question[0].Question}}<br/>
                Correct Answer: {{slip.question[0].CorrectAnswer}}) {{slip.question[0].Answers[slip.question[0].CorrectAnswer]}}
                <!-- {{slip.question[0].Answers}} -->
                <br/>
                Your Answer: {{slip.pickedAnswer}}) {{slip.question[0].Answers[slip.pickedAnswer]}}
            </div>
        </div>
    </div>
    </div>
</div>

</template>
<script>
export default {
    name:"Questions",
    data(){
        return{
            border:'',
            clickedAnswer:"",
            mark:'',
            markStatus:true,
            pickedAnswer:'',
            questionArray:"",
            total:0,
            nextDisabled:true,
            answered:false
        }
    },
    props:{
        questions:Array,
        result:Array,
    },
    methods:{
        verify:function(value){
            this.nextDisabled=false
            this.answered=true
            this.clickedAnswer = value
            this.pickedAnswer=value
            this.questionArray=this.questions
            console.log(this.pickedAnswer)
            if(this.questions[0].CorrectAnswer==value){
                this.border='green-border'
                this.mark="Correct Answer"
                this.markStatus=true
                
            }else{
                this.border='red-border'
                this.mark="Incorrect Answer"
                this.markStatus=false
            }
        },
        next:function(){
            if(this.mark=="Correct Answer"){
                this.total+=1
            }
            this.$emit('sendResult',{question:this.questionArray,pickedAnswer:this.pickedAnswer,mark:this.mark})
            this.border=''
            this.clickedAnswer=''
            this.mark=''
            this.markStatus=true
            this.pickedAnswer=''
            this.nextDisabled=true
            this.answered=false
        }
    }

}
</script>
<style scoped>
    .green-border{
        border-color: green !important;
        background-color: green !important;
        border:1px
    }
    .red-border{
        background-color: red !important;
        border-color: red !important ;
        border:1px
    }
    .ansBtn:disabled{
        opacity:1 !important;
    }
    /* ol#options {
  list-style-type:upper-alpha;
} */
</style>