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
  
  <!--"/assets/Screenshots(ForCommenting)/Classe/Class-TopSection.png"-->
                      <v-layout row wrap >
                        <v-flex xs6 offset-xs3 class="mb-4">
                        <!-- Class Icon Section -->
                        <!--"/assets/Screenshots(ForCommenting)/Classe/Class-TopSection-Icon.png"-->
                            <div class="text-xs-center mt-3">
                              <v-icon class="white--text" style="font-size: 120px; margin-right: 1%; margin-top: 3%">school</v-icon>
                            </div>
                        </v-flex>
                      </v-layout>
                      <!-- My Class Title Section -->
                      <!--"/assets/Screenshots(ForCommenting)/Classe/Class-TopSection-Title.png"-->
                      <v-layout row wrap>
                        <v-flex class="text-xs-center">
                          <h2 class="white--text">Ma classe</h2>
                        </v-flex>
                      </v-layout>
  <!--//!---------------->
  <!--// !END Top Section -->
  <!--//!---------------->


  <!--//*---------------->
  <!--// *Lower Section -->
  <!--//*---------------->
 <!--"/assets/Screenshots(ForCommenting)/Classe/Class-LowerSection.png"-->
                      <v-layout style="background-color: #ebebeb" row wrap>
                    <!-- Class name Section -->
                  <!--"/assets/Screenshots(ForCommenting)/Classe/Class-LowerSection-Top.png"-->
                        <v-card style="width:100%; height: 100px" class="gray--text text-xs-center">
                          <div style="padding-top: 20px" class="headline text-xs-center">{{classes[0].name}}</div>
                          <div>{{classes[0].users.length}} Élèves</div>
                          <div class="text-xs-center mt-2">
                          </div>
                        </v-card>
                      <!-- Students And Teacher Info Section -->
                      <!--"/assets/Screenshots(ForCommenting)/Classe/Class-LowerSection-middle.png"-->
                        <v-card style="width:100%; margin-top: 30px; margin-bottom: 30px" class="gray--text text-xs-center ml-3 mr-3">
                          <br>
                          <div style="padding-top: 10px" class="headline text-xs-center"><h4>Professeur: {{theTeacherInTheClass.firstname}} {{theTeacherInTheClass.surname}}</h4></div>
                          <div class="text-xs-center mt-2">
                          </div>
                          <!-- List Of Students Section -->
                          <!--"/assets/Screenshots(ForCommenting)/Classe/Class-LowerSection-middle-StudentsList.png"-->
                          <v-list>
                            <template v-for="(student,index) in classes[0].users">
                              <!--Render only if the current user in class is not a teacher-->
                              <v-list-tile v-if="isNotTeacher(index)" two-line  v-bind:key="student.name" class="mt-3 mb-3">
                                <v-list-tile-avatar>
                                  <img src="https://www.practicepanther.com/wp-content/uploads/2017/02/user.png">
                                </v-list-tile-avatar>
                                <v-list-tile-content class="ml-3">
                                  <v-list-tile-title style="font-size: 20px">{{student.firstname}} {{student.surname}}</v-list-tile-title>
                                </v-list-tile-content>
                                <v-list-tile-action>
                                  <v-icon color="grey lighten-1">arrow_right</v-icon>
                                </v-list-tile-action>
                              </v-list-tile>
                              <v-divider style="width:90%" inset v-if="index + 1 < classes[0].users.length"></v-divider>
                            </template>
                          </v-list>
                        </v-card>
                      <!--Quit Class Section -->
                      <!--"/assets/Screenshots(ForCommenting)/Classe/Class-LowerSection-Lower.png"-->
                        <v-flex class="text-xs-center">
                          <v-card style="margin-top: 30px; height: 130px; margin-bottom: 30px" class="gray--text text-xs-center ml-3 mr-3">
                            <v-btn large color="error" style="margin-top: 40px " @click="confirmClassLeaveDialog=true">Quitter ma classe</v-btn>
                          </v-card>
                        </v-flex>
                      </v-layout>
  <!--//!---------------->
  <!--// !END Lower Section -->
  <!--//!---------------->


  <!--//*---------------->
  <!--// *First Time Student Dialog Section -->
  <!--//*---------------->
                      <v-dialog v-model="firstTimeStudent" persistent>
                        <v-card>
                          <v-card-title class="headline">Vous êtes élève!</v-card-title>
                          <v-card-text>Vous pouvez maintenant voir votre classe, ainsi que ses listes et jouer dessus!</v-card-text>
                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="blue darken-1" flat @click.native="setFirstTimeStudentFalse">OK!</v-btn>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>
  <!--//!---------------->
  <!--// !First Time Student Dialog Section -->
  <!--//!---------------->



  <!--//*---------------->
  <!--// *Confirm Quit Class Dialog Section -->
  <!--//*---------------->
  <!--"/assets/Screenshots(ForCommenting)/Classe/Class-Dialogs-QuitClass.png"-->
                      <v-dialog v-model="confirmClassLeaveDialog" max-width="300" persistent>
                        <v-card>
                          <v-card-title class="headline">Quitter Ma Classe</v-card-title>
                          <v-card-text>Voulez-vous garder les listes de cette classe?</v-card-text>
                          <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="blue darken-1" flat @click.native="removeStudentButKeepLists">Oui</v-btn>
                            <v-btn color="blue darken-1" flat @click.native="removeStudent">Non</v-btn>
                            <v-btn color="blue darken-1" flat @click.native="confirmClassLeaveDialog = false">Annuler</v-btn>
                          </v-card-actions>
                        </v-card>
                      </v-dialog>
  <!--//!---------------->
  <!--// !Confirm Quit Class Dialog Section -->
  <!--//!---------------->


  </v-container>
</template>





<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////SCRIPT////////////////////////////////////////////////////::///// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<script>
export default {
	data() {
		return {
			// The dialog before leaving the class
			confirmClassLeaveDialog: false
		};
	},
	// We get all our properties from the store
	computed: {
		firstTimeStudent() {
			return this.$store.getters.firstTimeStudent;
		},
		// Get the classes of the student
		classes() {
			return this.$store.getters.classes;
		},
		theTeacherInTheClass() {
			return this.$store.getters.theTeacherInTheClass;
		},
		theUser() {
			return this.$store.getters.user;
		}
	},
	methods: {
		// When we have seen the dialog and pressed ok we set firsttimestudent to false
		setFirstTimeStudentFalse() {
			this.$store.dispatch("setFirstTimeStudent", false);
		},
		// We filter out the teacher(s) in the class to not display them
		isNotTeacher(index) {
			if (
				JSON.stringify(this.classes[0].users[index].roles) !==
				'["ROLE_PROFESSOR"]'
			) {
				return true;
			} else {
				return false;
			}
		},
		// When the student decides to leave the class without keeping the lists of that class
		removeStudent() {
			this.$store.dispatch("removeStudent", this.theUser.id);
		},
		// When the student decides to leave the class and keep the lists of that class
		removeStudentButKeepLists() {
			this.$store.dispatch("removeStudentButKeepLists", this.theUser.id);
		}
	},
	// We say that the player isn't playing a game to keep/set the side drawer to open
	created() {
		this.$store.dispatch("setIsPlayingGame", false);
	}
};
</script>