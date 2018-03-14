<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////TEMPLATE///////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<template>
  <v-container fluid style="margin-top: 100px">

  <!--"../../assets/Screenshots(ForCommenting)/home/home.png"-->

  <!--//*---------------->
  <!--// *Title Section -->
  <!--//*---------------->
  <!--"../../assets/Screenshots(ForCommenting)/home/home-title.png"-->
                    <v-layout row style="justify-content:center">
                      <h3 style="text-align:center;color:#737373">Bienvenue sur Vocs</h3>
                    </v-layout>
  <!--//!---------------->
  <!--// !END Title Section -->
  <!--//!---------------->




    <v-layout row wrap style="justify-content:center">

  <!--//*---------------->
  <!--// *Class Card Section -->
  <!--//*---------------->
  <!--"../../assets/Screenshots(ForCommenting)/home/home-classSection.png"-->
                    <v-flex lg5 md7 sm12 xs12 class="mr-2 ml-1">
                      <v-card>
                        <!-- Icon Container -->
                        <div style="background-color: #26a4ff">
                          <div class="text-xs-center ml-3 mr-3 mt-4" style="padding-top:15px;padding-bottom:15px" >
                            <v-icon class="white--text" style="font-size: 60px">school</v-icon>
                          </div>
                        </div>
                        <!-- Title -->
                        <div style="text-align:center;">
                          <p style="color:grey;font-size:20px;margin:0">Ma Classe</p>
                        </div>
                        <!-- Subtitle -->
                          <div v-if="user.roles !== 'USER' && user.classes.length === 0" style="color:black;font-size:17px;text-align:center">Pas de classe</div>
                          <div v-else-if="user.roles === 'USER' && user.classes.length === 0" style="color:black;font-size:17px;text-align:center">Pas de classe</div>
                          <div v-else style="color:black;font-size:17px;text-align:center;">{{user.classes[0].name}}</div>
                        <!-- See Class Button -->
                        <v-btn large flat color="primary" style="margin-top: 10px; margin-bottom: 10px;" to="/class">Voir</v-btn>
                      </v-card>
                    </v-flex>
  <!--//!---------------->
  <!--// !END Class Card Section -->
  <!--//!---------------->




  <!--//*---------------->
  <!--// *List Card Section -->
  <!--//*---------------->
       <!--"../../assets/Screenshots(ForCommenting)/home/home-listSection.png"-->
                    <v-flex lg5 md7 sm12 xs12 class="mr-2 ml-1">
                      <v-card>
                        <!-- Icon Container -->
                        <div style="background-color: #B198DA">
                          <div class="text-xs-center ml-3 mr-3 mt-4" style="padding-top:15px;padding-bottom:15px" >
                            <v-icon class="white--text" style="font-size: 60px">description</v-icon>
                          </div>
                        </div>
                        <!-- Title -->
                        <div style="text-align:center;">
                          <p style="color:grey;font-size:20px;margin:0">Mes Listes</p>
                        </div>
                          <!-- Subtitle (number of lists) -->
                          <div style="color:black;text-align:center;font-size:17px">{{user.lists.length}} liste(s)</div>
                        <!-- See Class Button -->
                        <v-btn large flat color="primary" style="margin-top: 10px; margin-bottom: 10px;" to="/lists">Voir</v-btn>
                      </v-card>
                    </v-flex>
  <!--//!---------------->
  <!--// !END List Card Section -->
  <!--//!---------------->
      


      
  <!--//*---------------->
  <!--// *Exercise Card Section -->
  <!--//*---------------->
       <!--"../../assets/Screenshots(ForCommenting)/home/home-exerciseSection.png"-->
                    <v-flex lg5 md7 sm12 xs12 class="mr-2 ml-1">
                      <v-card>
                        <!-- Icon Container -->
                        <div style="background-color: #6FC9C0">
                          <div class="text-xs-center ml-3 mr-3 mt-4" style="padding-top:15px;padding-bottom:15px" >
                            <v-icon class="white--text" style="font-size: 60px">play_arrow</v-icon>
                          </div>
                        </div>
                        <!-- Title -->
                        <div style="text-align:center;">
                          <p style="color:grey;font-size:20px;margin:0">Exercices</p>
                        </div>
                          <!-- Subtitle (number of lists) -->
                          <div style="color:black;text-align:center;font-size:17px">4 exercices disponibles</div>
                        <!-- See Class Button -->
                        <v-btn large flat color="primary" style="margin-top: 10px; margin-bottom: 10px;" to="/games">Voir</v-btn>
                      </v-card>
                    </v-flex>
  <!--//!---------------->
  <!--// !END Exercise Card Section -->
  <!--//!---------------->




  <!--//*---------------->
  <!--// *Settings Card Section -->
  <!--//*---------------->
       <!--"../../assets/Screenshots(ForCommenting)/home/home-settingsSection.png"-->
                    <v-flex lg5 md7 sm12 xs12 class="mr-2 ml-1">
                      <v-card>
                        <!-- Icon Container -->
                        <div style="background-color: #2B333E;">
                          <div class="text-xs-center ml-3 mr-3 mt-4" style="padding-top:15px;padding-bottom:15px" >
                            <v-icon class="white--text" style="font-size: 60px">tune</v-icon>
                          </div>
                        </div>
                        <!-- Title -->
                        <div style="text-align:center;">
                          <p style="color:grey;font-size:20px;margin:0">Réglages</p>
                        </div>
                          <!-- Subtitle (number of lists) -->
                          <div style="color:black;text-align:center;font-size:17px">Changer les réglages</div>
                        <!-- See Class Button -->
                        <v-btn large flat color="primary" style="margin-top: 10px; margin-bottom: 10px;" to="/settings">Voir</v-btn>
                      </v-card>
                    </v-flex>
  <!--//!---------------->
  <!--// !END Settings Card Section -->
  <!--//!---------------->


    </v-layout>

  </v-container>
</template>






<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--///////////////////////////////////////////////////////////SCRIPT////////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->


<script>
import ListBG from "@/assets/HomepageBG4.png";
export default {
	data() {
		return {
			listBG: ListBG
		};
	},
	computed: {
		user() {
			return this.$store.getters.user;
		},
		accountType() {
			if (
				this.user.roles === "STUDENT" ||
				JSON.stringify(this.user.roles) === '["ROLE_STUDENT"]'
			) {
				return "Élève";
			} else if (
				this.user.roles === "PROFESSOR" ||
				JSON.stringify(this.user.roles) === '["ROLE_PROFESSOR"]'
			) {
				return "Professeur";
			} else {
				return "Libre";
			}
		}
	},
	created() {
		// We say that the player isn't playing a game to keep/set the side drawer to open
		this.$store.dispatch("setIsPlayingGame", false);
	}
};
</script>
