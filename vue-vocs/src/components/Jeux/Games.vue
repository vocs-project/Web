<template>
  <v-container fluid style="padding-top: 100px; background-color: #8bc3dc; padding-right: 0px; padding-left: 0px; padding-bottom: 0px">
    <v-layout row style="justify-content:center">
      <v-icon class="white--text mt-5 mb-5" style="font-size: 120px;">gamepad</v-icon>
    </v-layout>
    <v-layout style="background-color: #ebebeb" row wrap>
      <v-card style="width:100%; height: 100px" class="gray--text text-xs-center">
        <div style="padding-top: 20px" class="headline text-xs-center">Exercices</div>
        <div>Entraînez-vous grâce à 5 modes d'exercices</div>
        <div class="text-xs-center mt-2">
        </div>
      </v-card>
      <v-card style="width:100%; margin-top: 30px" class="gray--text text-xs-center ml-3 mr-3">
        <br>
        <div style="padding-top: 10px" class="headline text-xs-center"><h4>Selectionnez Votre Mode D'exercices</h4></div>
        <div><h5>Cliquez sur l'icône d'aide pour plus d'informations sur chaque mode d'exercices</h5></div>
        <div class="text-xs-center mt-2">
        </div>
        <v-container fluid style="margin-top: 50px; margin-left: 15%">
          <v-layout row wrap>
            <v-flex lg4 sm8 md8 class="mb-3 mr-2 ml-2" v-for="gameMode in gameModes" :key="gameMode.name">
              <div  class="white--text game-box elevation-6 ma-1" :style="{ backgroundColor: gameMode.color }">
                <v-layout row>
                  <v-flex xs12>
                    <div class="text-xs-center mt-4">
                      <v-icon color="white" style="font-size: 50px">
                        {{gameMode.icon}}
                      </v-icon>
                    </div>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs12 class="mt-2">
                    <div class="headline text-xs-center">{{gameMode.name}}</div>
                  </v-flex>
                </v-layout>
                <v-layout row v-if="gameMode.showInfo">
                  <v-flex xs12>
                    <div class="text-xs-center mt-2">{{gameMode.description}}</div>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs12>
                    <div class="text-xs-center">
                      <v-btn icon @click="gameMode.showInfo=!gameMode.showInfo">
                        <v-icon large>help</v-icon>
                      </v-btn>
                    </div>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex xs12>
                    <div class="text-xs-center">
                      <v-btn flat dark @click="testIfUserHasSelectedAList (gameMode.link, gameMode.name)" >S'entrainer</v-btn>
                    </div>
                  </v-flex>
                </v-layout>
              </div>
              <v-layout row justify-center>
                <v-dialog max-width="500" v-model="dialogConfirmation">
                  <v-card>
                    <v-card-title class="headline">Selectionnez une liste</v-card-title>
                    <v-list>
                      <template v-for="list in lists">
                        <v-list-tile v-if="!(SelectedListForGameIsLessThanFour && selectedGameMode === 'QCM') || !(SelectedListForGameIsLessThanTen && selectedGameMode === 'Matching')" v-bind:key="list.name" class="mt-3 mb-3">
                          <v-list-tile-content style="cursor: pointer;background-color:#26A4FF;padding:10px;border-radius:4px" @click="setGameList(list);">
                            <v-list-tile-title style="font-size: 20px; color:white">{{list.name}} </v-list-tile-title>
                          </v-list-tile-content>
                        </v-list-tile>
                      </template>
                  </v-list>
                  </v-card>
                </v-dialog>
              </v-layout>
              <v-layout row justify-center>
                <v-dialog v-model="dialogConfirmation2" v-if="SelectedListForGameIsLessThanFour && selectedGameMode === 'QCM'">
                  <v-card>
                    <v-card-title class="headline">Votre liste {{selectedListForGame.name}} a moins de 4 mots.</v-card-title>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn flat to="/lists" color="primary" @click.native="dialogConfirmation2 = false">Choisir une autre liste</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
                <v-dialog v-model="dialogConfirmation2" v-else-if="SelectedListForGameIsLessThanTen && selectedGameMode === 'Matching'">
                  <v-card>
                    <v-card-title class="headline">Votre liste {{selectedListForGame.name}} a moins de 10 mots.</v-card-title>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn flat to="/lists" color="primary" @click.native="dialogConfirmation2 = false">Choisir une autre liste</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
                <v-dialog v-model="dialogConfirmation2" v-else>
                  <v-card>
                    <v-card-title class="headline">S'entrainer avec la liste {{selectedListForGame.name}}?</v-card-title>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn flat @click.native="dialogConfirmation2 = false">Annuler</v-btn>
                      <v-btn flat color="primary" @click.native="setGameList(selectedListForGame)" >S'entrainer</v-btn>
                      <v-btn flat color="primary" @click.native="chooseAnotherList()" >Choisir une autre liste</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </v-layout>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    data () {
      return {
        gameModes: [
          {name: 'Traduction', icon: 'gamepad', description: 'Traduire une série de mots qui s\'affichent en l\'écrivant dans la boîte indiquée', link: '/games/classic', color: '#6FC9C0', showInfo: false},
          {name: 'QCM', icon: 'gamepad', description: 'Choisir parmis plusieurs mots la traduction correcte ', link: '/games/QCM', color: '#26A4FF', showInfo: false},
          {name: 'Matching', icon: 'gamepad', description: 'Lier le mot français à sa traduction correspondante', link: '/games/matching', color: '#B198DA', showInfo: false},
          {name: 'Time Attack', icon: 'gamepad', description: 'Ecriver les mots correspondants mais avec une contrainte de temps!', link: '/games/timeattack', color: '#FF865E', showInfo: false}
        ],
        dialogConfirmation: false,
        dialogConfirmation2: false,
        tempLink: '',
        selectedGameMode: ''
      }
    },
    computed: {
      lists () {
        /* loadedLists doesn't take parenthese it is a property (even though it is a method in the store */
        return this.$store.getters.loadedLists
      },
      selectedListForGame () {
        return this.$store.getters.getSelectedListForGame
      },
      SelectedListForGameIsLessThanFour () {
        if (this.$store.getters.getSelectedListForGame === '') {
          return false
        } else {
          return this.$store.getters.getSelectedListForGame.wordTrads.length < 4
        }
      },
      SelectedListForGameIsLessThanTen () {
        if (this.$store.getters.getSelectedListForGame === '') {
          return false
        } else {
          return this.$store.getters.getSelectedListForGame.wordTrads.length < 10
        }
      },
      gameList () {
        return this.$store.getters.gameList
      }
    },
    methods: {
      testIfUserHasSelectedAList (link, gameMode) {
        this.selectedGameMode = gameMode
        this.tempLink = link
        if (this.selectedListForGame === '') {
          this.dialogConfirmation = true
        } else {
          this.dialogConfirmation2 = true
        }
      },
      setGameList (list) {
        this.$store.dispatch('setGameList', list)
        this.$store.dispatch('setIsPlayingGame',  true)
        this.$router.push(this.tempLink)
      },
      chooseAnotherList(){
        this.$store.dispatch('selectListForGame', '');
        this.dialogConfirmation2 = false;
        this.dialogConfirmation = true;
      }
    },
    created () {
      this.$store.dispatch('setIsPlayingGame', false)
    }
  }
</script>


<style>
  .game-box {
    height: 275px;
    border-radius: 10px;
  }
</style>
