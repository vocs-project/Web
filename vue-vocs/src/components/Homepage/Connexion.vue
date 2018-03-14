<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////TEMPLATE///////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<template>
  <v-parallax class="s1-parallax" :src="HomepageBG" style="height:100vh;width:100vw;margin-top: -65px">
    <v-container>

  <!--//*---------------->
  <!--// *First Section -->
  <!--//*---------------->
  <!--"../../assets/Screenshots(ForCommenting)/Homepage/connection-maincard.png"-->
                      <v-layout row>
                        <v-flex style="margin-top: 180px" xs12 sm6 offset-sm3>
                          <!--Toolbar Section -->   
                          <!--"../../assets/Screenshots(ForCommenting)/Homepage/connection-maincard-topbar.png"-->    
                          <v-toolbar color="light-blue" dark>
                            <v-toolbar-title>Connexion</v-toolbar-title>
                            <v-spacer></v-spacer>
                            <v-btn to="/inscription" flat>
                              pas inscrit?
                            </v-btn>
                          </v-toolbar>  
                          <v-card>
                            <v-card-text>
                              <v-container>
                                <form @submit.prevent="onSignin">
                                  <!--Inputs Section -->   
                                  <!--"../../assets/Screenshots(ForCommenting)/Homepage/connection-maincard-inputs.png"-->   
                                  <v-layout row>
                                    <v-flex xs12>
                                      <v-text-field
                                        name="email"
                                        label="Email"
                                        id="email"
                                        v-model="info.email"
                                        type="email"
                                        required>
                                      </v-text-field>
                                      <v-text-field
                                        name="password"
                                        label="Mot de passe"
                                        id="password"
                                        v-model="info.password"
                                        type="password"
                                        required>
                                      </v-text-field>
                                    </v-flex>
                                  </v-layout>
                                  <!--Button Section -->   
                                  <!--"../../assets/Screenshots(ForCommenting)/Homepage/connection-maincard-button.png"-->   
                                  <v-layout row>
                                    <v-flex xs12>
                                      <v-btn type="submit" >Connexion</v-btn>
                                    </v-flex>
                                  </v-layout>
                                </form>
                              </v-container>
                            </v-card-text>
                          </v-card>
                        </v-flex>
                      </v-layout>
  <!--//!---------------->
  <!--// !END First Section -->
  <!--//!---------------->




  <!--//*---------------->
  <!--// *First Section -->
  <!--//*---------------->
                      <v-layout row justify-center>
                        <v-dialog v-model="theConnectionErrorMessageIsOn">
                          <v-card>
                            <v-card-title class="headline">{{theConnectionErrorMessage}}</v-card-title>
                            <v-card-actions>
                              <v-spacer></v-spacer>
                              <v-btn flat @click.native="resetSignInErrorMessages">OK</v-btn>
                            </v-card-actions>
                          </v-card>
                        </v-dialog>
                      </v-layout>
  <!--//!---------------->
  <!--// !END First Section -->
  <!--//!---------------->
    </v-container>
  </v-parallax>
</template>








<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////SCRIPT/////////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<script>
import HomepageBG from "@/assets/HomepageBG.png";
export default {
	data() {
		return {
			HomepageBG: HomepageBG,
			users: [],
			info: {
				email: "",
				password: ""
			}
		};
	},
	computed: {
		comparePasswords() {
			return this.password !== this.confirmPassword
				? "Passwords do not match"
				: "";
		},
		user() {
			return this.$store.getters.user;
		},
		theConnectionErrorMessage() {
			return this.$store.getters.connectionErrorMessage;
		},
		theConnectionErrorMessageIsOn() {
			return this.$store.getters.connectionErrorMessage !== "";
		}
	},
	methods: {
		onSignin() {
			this.$store.dispatch("signUserIn", this.info);
		},
		resetSignInErrorMessages() {
			this.$store.dispatch("resetSignInAndUpErrorMessages");
		}
	},
	created() {
		// We say that the player isn't playing a game to keep/set the side drawer to open
		this.$store.dispatch("setIsPlayingGame", false);
		// Should have used this for my requests
		/*const customActions = {
        saveList: {method: 'POST', url: '/users.json'},
        saveClasse: {method: 'POST', url: '/classes.json'},
        saveUser: {method: 'POST', url: '/users.json'},
        getList: {method: 'GET', url: '/users.json'},
        getClasse: {method: 'GET', url: '/classes.json'},
        getUser: {method: 'GET', url: '/users.json'}
      }
      this.resource = this.$resource('users.json', {}, customActions)*/
	}
};
</script>
