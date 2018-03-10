<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////TEMPLATE///////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<template>
  <v-container fluid style="padding-top: 90px; background-color: #8BC3DC; padding-right: 0px; padding-left: 0px; padding-bottom: 0px">

  <!--//*---------------->
  <!--// *Top Section -->
  <!--//*---------------->
  <!--"/assets/Screenshots(ForCommenting)/Classe/JoinClass-TopSection.png"-->
                      <v-layout row wrap >
                        <v-flex xs6 offset-xs3 class="mb-4">
                        <!-- Class Icon Section -->
                        <!--"/assets/Screenshots(ForCommenting)/Classe/JoinClass-TopSection-Icon.png"-->
                            <div class="text-xs-center mt-3">
                              <v-icon class="white--text" style="font-size: 120px; margin-right: 1%; margin-top: 3%">school</v-icon>
                            </div>
                        </v-flex>
                      </v-layout>
                      <!-- My Class Title Section -->
                      <!--"/assets/Screenshots(ForCommenting)/Classe/JoinClass-TopSection-Title.png"-->
                      <v-layout row wrap>
                        <v-flex class="text-xs-center">
                          <h2 class="white--text">Rejoindre une classe</h2>
                        </v-flex>
                      </v-layout>
  <!--//!---------------->
  <!--// !END Top Section -->
  <!--//!---------------->


  <!--//*---------------->
  <!--// *Form Section -->
  <!--//*---------------->
  <!--"/assets/Screenshots(ForCommenting)/Classe/JoinClass-LowerSection.png"-->
                      <v-layout style="background-color: #ebebeb" row wrap>
                        <v-card style="width:100%; height: 309px" class="gray--text text-xs-center">
                          <v-select
                            style="width: 30%; margin: auto; margin-top: 13px"
                            :items="allSchools"
                            v-model="schoolSearch"
                            label="Enter un établissement"
                            autocomplete
                            required
                          ></v-select>
                          <v-select
                            style="width: 30%; margin: auto; margin-top: 13px"
                            :items="theClasses"
                            v-model="classSearch"
                            label="Enter une class"
                            required
                          ></v-select>
                          <br>
                          <v-btn :disabled="classSearch === ''" @click="showJoinClassDialog = true">Envoyer une demande</v-btn>
                          <!--<div v-if="notifications.demandSend.length > 0" >Vous avez déjà envoyé une demande</div>-->
                        </v-card>
                      </v-layout>
  <!--//!---------------->
  <!--// !END Form Section -->
  <!--//!---------------->


  <!--//*---------------->
  <!--// *Confirm Invitation Send Dialog -->
  <!--//*---------------->
                      <v-dialog v-model="showJoinClassDialog" persistent>
                        <v-card>
                          <v-card-title class="headline">Êtes-vous sûr de vouloir envoyer une demande à cette class?</v-card-title>
                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="blue darken-1" flat @click.native="showJoinClassDialog = false">Annuler</v-btn>
                            <v-btn color="blue darken-1" flat @click.native="acceptClassJoin">Envoyer</v-btn>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>
  <!--//!---------------->
  <!--// !Confirm Invitation Send Dialog -->
  <!--//!---------------->


  </v-container>
</template>






<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////SCRIPT///////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<script>
export default {
	data() {
		return {
			theClasses: [],
			allSchools: [],
			schoolSearch: "",
			classSearch: "",
			showJoinClassDialog: false
		};
	},
	computed: {
		allClasses() {
			return this.$store.getters.allClasses;
		},
		schools() {
			return this.$store.getters.schools;
		},
		notifications() {
			return this.$store.getters.myDemands;
		}
	},
	methods: {
		acceptClassJoin() {
			/*this.$store.dispatch('setFirstTimeStudent', true)
      this.$store.dispatch('setRoles', 'STUDENT')*/
			this.showJoinClassDialog = false;
			var id = null;
			for (var i = 0; i < this.allClasses.length; i++) {
				// *! NOT GREAT WAY IF THERE ARE CLASSES WITH THE SAME NAME
				if (this.allClasses[i].name === this.classSearch) {
					id = this.allClasses[i].id;
				}
			}
			var theClassToSendOff = {
				id: id,
				name: this.classSearch
			};
			this.$store.dispatch("setUserClass", theClassToSendOff);
		}
	},
	created() {
		// We say that the player isn't playing a game to keep/set the side drawer to open
		this.$store.dispatch("setIsPlayingGame", false);
		// Create an array an only put in the names of the classes for the list
		for (var i = 0; i < this.allClasses.length; i++) {
			this.theClasses[i] = this.allClasses[i].name;
		}
		// Create an array an only put in the names of the schools for the list
		for (var y = 0; y < this.schools.length; y++) {
			this.allSchools[y] = this.schools[y].nom;
		}
	}
};
</script>
