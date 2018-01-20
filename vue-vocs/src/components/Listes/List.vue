<template>
  <v-container  style="margin-top: 100px">
    <v-layout>
      <v-flex xs10 offset-xs1>
        <v-card>
          <v-toolbar color="light-blue" dark>
            <v-btn flat to="/lists"><v-icon >arrow_back</v-icon>Retour</v-btn>
            <v-toolbar-title>{{list.name}}</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn v-if="isAPersonalList" icon @click.stop="createWordDialog = true">
              <v-icon>add</v-icon>
            </v-btn>
          </v-toolbar>
          <v-list>
            <div class="text-xs-center" v-if="list.wordTrads.length > 0 && Math.floor((nbGreenWords/list.wordTrads.length)*100) <100" style="display: flex;padding: 10px;padding-left: 5%">
              <div style="margin-right: 3%;">Progression: {{Math.floor((nbGreenWords/list.wordTrads.length)*100)}}%</div>
              <div :style="{width: ((nbGreenWords/list.wordTrads.length)*100)*0.7 + '%'}" style="margin-top:6px;background-color: green;height: 10px;"></div>
              <div :style="{width: ((nbOrangeWords/list.wordTrads.length)*100)*0.7 + '%'}" style="margin-top:6px;background-color: orange;height: 10px;"></div>
              <div :style="{width: ((nbRedWords/list.wordTrads.length)*100)*0.7 + '%'}" style="margin-top:6px;background-color: red;height: 10px;"></div>
            </div>
            <div v-if="Math.floor((nbGreenWords/list.wordTrads.length)*100) >=100" class="text-xs-center mt-1 mb-0" ><h5>LIST APPRISE!</h5></div>
            <div v-if="list.wordTrads.length <= 0" class="text-xs-center mt-4"><h5>Liste vide</h5></div>
            <v-list-tile v-for="aWord in list.wordTrads" :key="aWord.id">
              <v-dialog v-model="showWordDeleteConfirmation" persistent>
                <v-card>
                  <v-card-title class="headline">Êtes-vous sûr de vouloir supprimer ce mot?</v-card-title>
                  <v-card-text>En supprimant ce mot vous ne pouvez pas revenir en arrière.</v-card-text>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue" flat @click.native="showWordDeleteConfirmation = false">Annuler</v-btn>
                    <v-btn color="blue" flat @click.native="showWordDeleteConfirmation = false; removeWord(wordRemovalId)">Supprimer</v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
              <v-list-tile-content>
                <div style="display: flex">
                  <div v-if="aWord.stat.level>3" style="background-color: green;border-radius:70px;width: 25px;height: 20px;margin-right:15px;margin-top: 1px"></div>
                  <div v-else-if="aWord.stat.level>1" style="background-color: orange;border-radius:70px;width: 25px;height: 20px;margin-right:15px;margin-top: 1px"></div>
                  <div v-else style="background-color: red;border-radius:70px;width: 25px;height: 20px;margin-right:15px;margin-top: 1px"></div>
                  <v-list-tile-title v-if="aWord.word.language.code=='EN'">{{aWord.word.content}} &rarr; {{aWord.trad.content}}</v-list-tile-title>
                  <v-list-tile-title v-else>{{aWord.trad.content}} &rarr; {{aWord.word.content}}</v-list-tile-title>
                </div>
              </v-list-tile-content>
              <v-btn icon @click="listenToWord(aWord)">
                <v-icon color="grey lighten-1">volume_up</v-icon>
              </v-btn>
              <v-list-tile-action>
                <v-btn icon v-if="isAPersonalList" @click="showWordDeleteConfirmation=true; wordRemovalId=aWord.id; selectWord(aWord)">
                  <v-icon color="grey lighten-1">delete</v-icon>
                </v-btn>
              </v-list-tile-action>
            </v-list-tile>
          </v-list>
        </v-card>
      </v-flex>
    </v-layout>
    <v-dialog v-model="createWordDialog" temporary>
      <v-card>
        <v-toolbar style="flex: 0 0 auto;" class="info">
          <v-btn icon @click.native="createWordDialog = false" dark>
            <v-icon dark>close</v-icon>
          </v-btn>
          <v-toolbar-title style="color: white">Ajouter un mot</v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>
        <v-card-title primary-title>
          <v-flex xs12 sm6>
              <v-form style="width:15vw;margin:0">
                <v-text-field
                  label="Mot (Anglais)"
                  v-model="createWordName"
                  :counter="10"
                  required
                ></v-text-field>
                <v-text-field
                  label="Traduction (Français)"
                  v-model="createWordTranslation"
                  :counter="10"
                  required
                ></v-text-field>
                <v-btn :disabled="createWordName === '' || createWordTranslation === ''" @click="addWord(createWordName, createWordTranslation)">Ajouter</v-btn>
              </v-form>
              <div v-for="createdWord in createdWords">{{createdWord.word.content}} &rarr;  {{createdWord.trad.content}}</div>
          </v-flex>
        </v-card-title>
        <v-card-actions>
          <v-flex xs12 sm6 offset-sm3>
            <v-btn
              @click="addWords(createdWords)"
              @click.stop="createWordDialog = false"
              :disabled="!createWordFormIsValid"
            >
              OK
            </v-btn>
          </v-flex>
        </v-card-actions>
        <div style="flex: 1 1 auto;"></div>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
  export default {
    data () {
      return {
        showWordDeleteConfirmation: false,
        wordRemovalId: '',
        createWordDialog: false,
        createWordName: '',
        createWordTranslation: '',
        createWordId: '',
        createdWords: [],
        createWordFormIsValid: false,
      }
    },
    props: ['id'],
    computed: {
      list () {
        return this.$store.getters.getSelectedList
      },
      isAPersonalList () {
        return this.$store.getters.isAPersonalList
      },
      nbGreenWords(){
        var green = 0;
        for(let i=0;i<this.list.wordTrads.length;i++) {
          if(this.list.wordTrads[i].stat.level>3){
            green ++;
          }
        }
        return green;
      },
      nbOrangeWords(){
        var orange = 0;
        for(let i=0;i<this.list.wordTrads.length;i++) {
          if(this.list.wordTrads[i].stat.level>1 && this.list.wordTrads[i].stat.level<=3 ){
            orange ++;
          }
        }
        return orange;
      },
      nbRedWords(){
        var red = 0;
        for(let i=0;i<this.list.wordTrads.length;i++) {
          if(this.list.wordTrads[i].stat.level<=1){
            red ++;
          }
        }
        return red;
      }
    },
    methods: {
      removeWord (wordId) {
        this.$store.dispatch('removeWord', wordId)
      },
      selectWord (word) {
        return this.$store.dispatch('selectWord', word)
      },
      addWord (word, trad) {
        if (this.createWordId === '') {
          if (this.list.wordTrads.length > 0) {
            this.createWordId = parseInt(this.list.wordTrads[this.list.wordTrads.length - 1].id) + 1
          } else {
            this.createWordId = 1
          }
        } else {
          this.createWordId++
        }
        this.createdWords.push({word: {content: word, language: 'EN'}, trad: {content: trad, language: 'FR'}})
        this.createWordName = ''
        this.createWordTranslation = ''
        this.createWordFormIsValid = true
      },
      addWords (words) {
        this.$store.dispatch('addWords', words)
        this.createdWords = []
        this.createWordId = ''
      },
      listenToWord(word) {
        if(word.word.language.code ==='EN') {
          responsiveVoice.speak(word.word.content,localStorage.getItem('userVoicePreference'), {rate: 0.8});
        } else {
          responsiveVoice.speak(word.trad.content,localStorage.getItem('userVoicePreference'), {rate: 0.8});
        }
      }
    },
    created () {
      this.$store.dispatch('setIsPlayingGame', false)
    }
  }
</script>
