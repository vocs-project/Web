<template>
  <v-container fluid class="mt-5" style="background-color: #f4f4f4; height: 685px" >
    <v-dialog  v-if="!started" v-model="FirstCountDownBeforeStarting" persistent>
      <v-card>
        <br>
        <h3 class="headline text-xs-center ">Vous êtes prêt? </h3>
        <br>
        <h2 class="text-xs-center mb-4 ">{{FirstCountDownBeforeStartingValue}}</h2>
        <br>
        <br>
      </v-card>
    </v-dialog>
    <v-layout v-if="started" row wrap style="margin-top: 5vh">
      <v-flex xs4 offset-xs4>
        <div class="text-xs-center">
          <form v-if="!finished">
            <div style="background-color: #c9c9c9;width:100%;height:20px">
              <div :style="{backgroundColor: timerColor,width:timer + '%'}" style="height: 20px;">

              </div>
            </div>
            <div class="mt-3">
              <v-icon :style="{color: life1Color}" style="font-size: 60px">favorite</v-icon>
              <v-icon :style="{color: life2Color}" style="font-size: 60px">favorite</v-icon>
              <v-icon :style="{color: life3Color}" style="font-size: 60px">favorite</v-icon></div>
            <v-layout row>
              <v-flex xs12>
                <v-alert
                  v-if="userEnteredCorrectAnswer"
                  color="success"
                  icon="check_circle"
                  :value="userEnteredCorrectAnswer"
                  dismissible
                  transition="scale-transition"
                >
                  Bonne Réponse!
                </v-alert>
                <div v-if="userEnteredWrongAnswer">
                  <v-alert
                    color="error"
                    icon="warning"
                    :value="userEnteredWrongAnswer"
                    transition="scale-transition"
                  >
                    Mauvaise Réponse...<br>
                  </v-alert>
                </div>
                <div v-if="userEnteredSynonym">
                  <v-alert
                    color="info"
                    icon="check_circle"
                    :value="userEnteredSynonym"
                    transition="scale-transition"
                  >
                    C'est correct!<br>
                    La solution attendue est:
                    <h6>{{previousAnswer}}</h6>
                  </v-alert>
                </div>
              </v-flex>
            </v-layout>
            <br>
            <h2>{{question}}</h2>

            <br>
            <v-layout row>
              <v-flex xs12>
                <v-text-field
                  name="answer"
                  label="Réponse"
                  id="Answer"
                  v-model="userAnswer"
                  autofocus
                  clearable
                  hint="Entrez la traduction du mot affiché"
                >
                </v-text-field>
              </v-flex>
            </v-layout>
            <v-layout row>
              <v-flex xs12>
                <v-btn class="blue" dark large @click="testAnswer" >Ok</v-btn>
              </v-flex>
            </v-layout>
          </form>
          <div v-if="finished">
            <h2>Fini!</h2>
            <br>
            <h2>{{correctAnswers}} / {{questionsAsked}} !</h2>
            <br>
            <v-btn class="blue" dark large to=/games>Terminer</v-btn>
          </div>
        </div>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  //import VBtn from "vuetify/src/components/VBtn/VBtn";

  export default {
    //components: {VBtn},
    data () {
      return {
        question: '',
        userAnswer: '',
        answer: '',
        answerObject: {},
        questionsAsked: 0,
        finished: false,
        questionResult: '',
        correctAnswers: 0,
        listSize: 0,
        userEnteredCorrectAnswer : false,
        userEnteredWrongAnswer : false,
        userEnteredSynonym: false,
        synonymes : [],
        previousAnswer: null,
        currentWordStats: null,
        currentWordId: null,
        timer: 100,
        timerColor:'#529bff',
        lives:3,
        FirstCountDownBeforeStarting:true,
        FirstCountDownBeforeStartingValue:3,
        countDownBeforeStartingInterval: null,
        started:false,
        life1Color:'red',
        life2Color:'red',
        life3Color:'red'
      }
    },
    computed: {
      user () {
        return this.$store.getters.user
      },
      list () {
        return JSON.parse(JSON.stringify(this.$store.getters.gameList))
      },
      accountType () {
        if (this.user.roles === 'STUDENT' || JSON.stringify(this.user.roles) === '["ROLE_STUDENT"]') {
          return 'Élève'
        } else if (this.user.roles === 'PROFESSOR' || JSON.stringify(this.user.roles) === '["ROLE_PROFESSOR"]') {
          return 'Professeur'
        } else {
          return 'Libre'
        }
      }
    },
    methods: {
      randomQuestion () {
        this.hasGotItWrong = false;
        var randomNum = Math.floor(Math.random() * this.list.wordTrads.length);
        if(this.list.wordTrads[randomNum].word.language.code === 'EN') {
          this.question = this.list.wordTrads[randomNum].trad.content;
          this.answer = this.list.wordTrads[randomNum].word.content.toLowerCase();
          this.synonymes = this.list.wordTrads[randomNum].trad.trads;
        } else{
          this.question = this.list.wordTrads[randomNum].word.content;
          this.answer = this.list.wordTrads[randomNum].trad.content.toLowerCase();
          this.synonymes = this.list.wordTrads[randomNum].word.trads;
        }
        this.timer=100;
        this.timerColor='#529bff';
        this.currentWordStats = this.list.wordTrads[randomNum].stat;
        console.log('********currentWordStats: ' + JSON.stringify(this.currentWordStats));
        this.currentWordId = this.list.wordTrads[randomNum].id;
        console.log("all synonymes: " + JSON.stringify(this.list.wordTrads[randomNum].word));
        this.answerObject = this.list.wordTrads[randomNum];
        this.userAnswer = '';
      },
      testAnswer () {
        var heEnteredSynonyme = this.testIfUserEnteredASynonyme(this.userAnswer,this.synonymes);
        if (this.userAnswer.toLowerCase() === this.answer) {
            this.correctAnswers++;
            if(this.currentWordStats.level<5){
              this.currentWordStats.level ++;
            }
            this.currentWordStats.goodRepetition ++;
            if(this.currentWordStats.goodRepetition >=2) {
              this.currentWordStats.badRepetition =0;
            }
            var word = {
              stat: this.currentWordStats
            }
            this.$store.dispatch('updateWordStats',word);
          this.userEnteredCorrectAnswer = true;
          this.userEnteredWrongAnswer = false;
          this.userEnteredSynonym = false;
          this.questionResult = 'Bonne Réponse'
          this.questionsAsked++;
          this.randomQuestion()
        } else if(heEnteredSynonyme) {
          this.correctAnswers++
          this.userEnteredCorrectAnswer = false;
          this.userEnteredSynonym = true;
          this.userEnteredWrongAnswer = false;
          this.previousAnswer = this.answer;
          this.questionResult = 'Bonne Réponse'
          this.questionsAsked++;
          this.randomQuestion()
        }else {
          this.questionsAsked++;
          if(this.currentWordStats.level>0){
            this.currentWordStats.level --;
          }
          this.currentWordStats.badRepetition ++;
          this.currentWordStats.goodRepetition=0;
          var word = {
            stat: this.currentWordStats
          }
          this.$store.dispatch('updateWordStats',word);
          this.userEnteredCorrectAnswer = false;
          this.userEnteredWrongAnswer = true;
          this.userEnteredSynonym = false;
          this.lives --;
          this.life3Color = 'grey';
          if(this.lives ==1){
            this.life2Color = 'grey';
          }
          if(this.lives <=0) {
            this.life1Color = 'grey';
            this.finished = true;
          }else{
            this.randomQuestion()
          }
        }

      },
      testIfUserEnteredASynonyme(userInput,synonymes){
        console.log("testing for synonyme");
        for (var s=0;s<synonymes.length;s++){
          console.log("user input: "+userInput+" curent synonyme: "+synonymes[s].content);
          if (userInput.toLowerCase() == synonymes[s].content.toLowerCase()){
            return true;
          }
        }
        return false;
      },
      sendSynonyme () {
        var toSend = {
          userAnswer: this.userAnswer,
          answerObject: this.answerObject
        }
        console.log(this.userAnswer);
        this.$store.dispatch('sendSynonyme', toSend);
        this.alertSignalerMot = false;
      },
      countDown1(){
        setInterval(() => {
          this.timer--;
          if(this.timer<=60 && this.timer>=35){
            this.timerColor ='#ffbd8c';
          }
          if(this.timer<35){
            this.timerColor ='#ff766b';
          }
          if(this.timer<=0){
            this.lives --;
            this.life3Color = 'grey';
            if(this.lives ==1) {
              this.life2Color = 'grey';
            }
            if(this.lives <=0) {
              this.life1Color = 'grey';
              this.finished = true;
            }else{
              this.questionsAsked++;
              this.randomQuestion()
            }
            this.timer = 100;
          }
        },45);
      },
      countDownBeforeStarting(){
        this.countDownBeforeStartingInterval = setInterval(() => {
          this.FirstCountDownBeforeStartingValue--;
          if(this.FirstCountDownBeforeStartingValue<=0){
            this.randomQuestion();
            this.countDown1();
            clearInterval(this.countDownBeforeStartingInterval);
            this.started = true;
          }

        },1000);
      }
    },
    created () {
      this.listSize = this.list.wordTrads.length;
      this.countDownBeforeStarting();
    }
  }
</script>
