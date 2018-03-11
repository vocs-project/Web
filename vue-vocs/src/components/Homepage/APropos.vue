<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////TEMPLATE///////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<template>
  <div v-scroll="scroll">

  <!--//*---------------->
  <!--// *First Section -->
  <!--//*---------------->
  <!--"/assets/Screenshots(ForCommenting)/Homepage/apropos-header.png"-->
                      <v-parallax class="s1-parallax" :src="HomepageBG" style="height:100vh;width:100vw;margin-top: -65px">
                        <v-layout align-center justify-center class="mt-5">
                          <v-flex xs10 sm10 md8 class="text-xs-center" :class="s1TextClass">
                            <h1 class="white--text text-xs-center" >A propos de<br></h1>
                            <h1 class="white--text text-xs-center">Vocs</h1>
                            <v-btn icon class="text-xs-center" large @click="autoScrollDown">
                              <v-icon large color="white">keyboard_arrow_down</v-icon>
                            </v-btn>
                          </v-flex>
                        </v-layout>
                      </v-parallax>
  <!--//!---------------->
  <!--// !END First Section -->
  <!--//!---------------->

    <br>
    <br>
    <br>

  <!--//*---------------->
  <!--// *Text Section -->
  <!--//*---------------->
  <!--"/assets/Screenshots(ForCommenting)/Homepage/apropos-text.png"-->
                      <v-container>
                        <v-layout row wrap class="text-xs-center">
                          <h5><strong>Vocs a pour but de répondre à plusieurs

                            problématiques :</strong><br><br>

                            ➔ Comment apprendre le vocabulaire anglais sur le long terme ?<br><br>

                            ➔ Comment utiliser les technologies mises à disposition (smartphone,

                            ordinateur) des étudiants à des fins pédagogiques ?<br><br>

                            ➔ Comment partager le savoir des professeurs d’anglais à une grande

                            communauté d’étudiants ?<br><br><br>

                            <strong> Les Listes :</strong><br><br>

                            Nous comptons tout d'abord implanter un système de listes. Initialement la plateforme

                            contiendra des listes de vocabulaire sur différentes thématiques que les utilisateurs

                            pourront s’approprier.<br>

                            Ainsi, tout le monde pourra télécharger une liste quand il le souhaitera pour pouvoir réviser

                            où bon lui plaira et surtout, quand le temps le lui permettra.<br>

                            Chaque utilisateur pourra créer ses propres listes de mots traduits qu'il pourra

                            ensuite réviser à sa guise. (Les listes pourront être mises en ligne après être soumises à une

                            correction des traductions par des professeurs ou par les administrateurs).<br>

                            Les listes pourront aussi être mises par des professeurs, et être soumises à leurs élèves,

                            qui devront s'inscrire dans leur classe pour pouvoir les consulter.<br>

                            Par exemple, vous êtes professeur d'une classe de première 4 au lycée Victor Hugo à

                            Caen. Sur internet, un groupe privé sera créé et nommé "1A du lycée Victor Hugo Caen". Le

                            professeur pourra créer la classe, choisir son nom et gérer la classe. Les élèves pourront

                            rejoindre la classe et vous pourrez accepter ou non leur demande d'adhésion (pour éviter les

                            fausses candidatures). Les élèves pourront ainsi faire des tests.<br><br><br>

                            <strong>Les modes d’apprentissage :</strong><br><br>

                            Nous avons aussi pour idée d'implanter différents modes d’apprentissage. Par exemple:

                            - La Traduction: une traduction en français ou en anglais des mots proposés par

                            l'application.<br><br>

                            - Le Time-Attack: à l'image de beaucoup de mini-jeux sur internet, nous proposons un jeu où

                            le but est de traduire le plus de mots possible dans le temps imparti.<br><br>

                            - Le Matching: ce mode propose une liste de mots français et anglais répartis de part et

                            d'autre de l'écran. Ils sont placés au hasard et l'élève doit relier les traductions entre elles.<br><br>

                            - Le QCM: un mot en anglais ou en français est proposé. Plusieurs traductions apparaissent.

                            Il suffit de cocher la ou les bonnes réponses.<br><br>

                            - Le mode Hard: Les mots que chaque utilisateur orthographient le moins bien sont stockés

                            dans une Hard-List personnelle. Nous prenons ensuite ces fameux mots et réalisons un test

                            constitué uniquement de ces mots.<br><br><br>

                            <strong>Les statistiques :</strong><br><br>

                            Nous souhaitons aussi mettre en place un système de statistiques, permettant à

                            chacun de savoir dans quels domaines il est le plus performant et, a contrario, dans lesquels

                            il doit progresser.<br><br><br>

                            <strong>Les fonctionnalités supplémentaires :</strong><br><br>

                            Un système de prononciation sera aussi mis en place, accompagné de symboles

                            phonétiques. Il sera possible de cliquer sur un bouton haut-parleur pour entendre la

                            prononciation du mot choisi, et la phonétique de ce mot apparaîtra juste à côté.</h5>
                        </v-layout>
                      </v-container>
  <!--//!---------------->
  <!--// !END Text Section -->
  <!--//!---------------->




  <!--//*---------------->
  <!--// *Footer Section -->
  <!--//*---------------->
  <!--"/assets/Screenshots(ForCommenting)/Homepage/apropos-footer.png"-->
                      <footer style="height: auto;background-color: rgba(24,24,24,0.85);padding: 2%;padding-top: 40px">
                        <v-layout row wrap>
                          <v-flex lg4 sm12 xs12 style="align-items: center;justify-content: center;margin-bottom: 20px">
                            <div>
                              <h6 style="color: white" class="text-xs-center">A Propos</h6>
                              <p style="color: white" class="text-xs-center">A propos de la plateforme Vocs</p>
                            </div>
                          </v-flex>
                          <v-flex lg4 sm12 xs12 style="align-items: center;justify-content: center;margin-bottom: 20px">
                            <div>
                              <h6 style="color: white" class="text-xs-center">Connexion</h6>
                              <p style="color: white" class="text-xs-center">Connectez-vous à votre compte personnel</p>
                            </div>
                          </v-flex>
                          <v-flex lg4 sm12 xs12 style="align-items: center;justify-content: center;margin-bottom: 20px">
                            <div>
                              <h6 style="color: white" class="text-xs-center">Inscription</h6>
                              <p style="color: white" class="text-xs-center">Inscrivez-vous si vous ne l'avez pas encore fait</p>
                            </div>
                          </v-flex>
                        </v-layout>
                        <v-layout row wrap style="margin-top: 30px;margin-bottom: 20px">
                          <v-flex xs12>
                            <div style="align-items: center;justify-content: center;">
                              <h6 style="color: white" class="text-xs-center">Contact</h6>
                              <p style="color: white" class="text-xs-center">Vocs Inc</p>
                            </div>
                          </v-flex>
                          <v-flex xs12 class="text-xs-center">
                            <img :src="logo" alt="Logo Vocs" style="height: 40px;">
                          </v-flex>
                        </v-layout>
                      </footer>
  <!--//!---------------->
  <!--// !END Footer Section -->
  <!--//!---------------->
  </div>
</template>





<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////SCRIPT///////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<script>
import HomepageBG from "@/assets/HomepageBG.png";
import logo from "@/assets/logoFlatWhite.png";

export default {
	data() {
		return {
			logo: logo,
			HomepageBG: HomepageBG,
			s1TextClass: "s1-text-hide"
		};
	},
	methods: {
		autoScrollDown() {
			do {
				document.documentElement.scrollTop =
					document.documentElement.scrollTop + 1;
			} while (document.documentElement.scrollTop < 745);
		}
	},
	mounted() {
		this.$nextTick(function() {
			this.offsetTop = window.pageYOffset || document.documentElement.scrollTop;
			if (this.offsetTop >= 0) {
				this.s1TextClass = "s1-text-show";
			}
		});
	},
	created() {
		// We say that the player isn't playing a game to keep/set the side drawer to open
		this.$store.dispatch("setIsPlayingGame", false);
	}
};
</script>










<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////STYLE///////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->

<style scoped>
.textSlide {
	color: white;
	font-size: 4em;
}
.textMain {
	margin-top: 22vh;
	color: white;
	font-size: 6rem;
}
.s1-parallax {
	background-size: contain;
}
.s1-text-hide {
	transform: translateY(-150%);
	opacity: 0;
	transition: transform 1.2s ease, opacity 3s;
}
.s1-text-show {
	transition: transform 1.2s ease, opacity 3s;
}
.s1-btn :hover {
	height: 90px !important;
	transition: height 2s;
}
.s2-iphone {
	width: auto;
}
.s2-iphone-hide {
	transform: translateX(-300%);
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s2-iphone-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s2-text {
	height: 350px;
}
.s2-text-hide {
	transform: translateX(300%);
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s2-text-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s3-headline {
	height: 180px;
}
.s3-box {
	height: 220px;
}
.s3-text-left-hide {
	transform: translateX(-300%);
	opacity: 0;
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1), opacity 2s;
}
.s3-text-left-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1), opacity 2s;
}
.s3-text-middle-hide {
	font-size: 26px;
	opacity: 0.1;
	transition: font-size 1.2s cubic-bezier(0.6, 0, 0.07, 1), opacity 1.2s;
}
.s3-text-middle-show {
	transition: font-size 1.2s cubic-bezier(0.6, 0, 0.07, 1), opacity 1.2s;
}
.s3-text-right-hide {
	transform: translateX(300%);
	opacity: 0;
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1), opacity 2s;
}
.s3-text-right-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1), opacity 2s;
}
.s3-main-text-hide {
	opacity: 0;
	transition: opacity 2s cubic-bezier(0.6, 0, 0.07, 1);
}
.s3-main-text-show {
	transition: opacity 2s cubic-bezier(0.6, 0, 0.07, 1);
}
</style>
