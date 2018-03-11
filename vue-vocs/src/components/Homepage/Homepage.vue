<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////VIEW///////////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->


<template>

  <!-- Set Scroll Event To Track Scroll Position-->
  <div v-scroll="scroll">



    <!-------------->
    <!-- First Section -->
    <!-------------->
    <v-parallax class="s1-parallax" :src="BGFrontPageSRC" style="height:100vh;width:100vw;margin-top: -65px">
      <v-layout style="height:100vh;width:100%;">
        <v-flex xs8 md10 lg8 sm10 offset-xs2 offset-lg2 offset-sm1 style="align-self: center;" >
          <h1 class="white--text text-xs-center" style="font-size: 100px">Vocs</h1>
          <h3 class="white--text text-xs-center" style="opacity: 0.7;font-size: 40px">Apprenez, retenez, réussissez.</h3>
          <p class="white--text text-xs-center" style="opacity: 0.7;font-size: 20px" >Une plateforme pour apprendre le vocabulaire en anglais.</p>
          <div class="text-xs-center">
            <v-btn style="border-radius: 10px;background-color: #27629E;color: white;width:200px;height:55px;font-size: 20px" large to="/inscription">
              Commencer
            </v-btn>
          </div>
        </v-flex>
      </v-layout>
    </v-parallax>



    <!-------------->
    <!-- Second Section -->
    <!-------------->
    <v-container>
      <br>
      <br>
      <v-layout row wrap >
        <v-flex md6 sm12 xs12 class="text-xs-center">
          <img :class="s2IphoneClass" :src="iphone" class="s2-iphone" height="420px">
        </v-flex>
        <v-flex :class="s2TextClass" md6 sm12 xs12 class="text-xs-center pt-5">
          <p style="font-size:38px;color: #5a5a5a">Vocs partout où vous êtes.</p>
          <p style="font-size:24px;color: #5a5a5a;opacity: 0.8">Grâce au site Web et à l'application mobile, vous pourrez apprendre l'anglais partout où vous êtes.
            Pas de connexion internet? Avec l'application mobile téléchargez votre vocabulaire sur votre appareil pour toujours l'avoir avec vous.</p>
        </v-flex>
      </v-layout>
      <br>
      <br>
    </v-container>



    <!-------------->
    <!-- Third Section -->
    <!-------------->
    <v-container text-xs-center fluid style="background-color: #f6f6f6">

      <v-layout row wrap >
        <v-flex xs12 style="margin-top: 30px;margin-bottom: 20px" class="text-xs-center" :class="s3MainTextClass">
          <p style="font-size: 38px;color: #5a5a5a">Une superbe façon d'apprendre</p>
        </v-flex>
      </v-layout>

      <v-layout row wrap style="margin-bottom: 20px">

        <v-flex xs12 sm6 md3 class="pa-3" :class="s3TextClassLeft">
          <p><v-icon class="s3-icon">done</v-icon></p>
          <p style="font-size: 26px;color: #5a5a5a">Simple, efficace et facile d'utilisation.</p>
        </v-flex>

        <v-flex xs12 sm6 md3 class="pa-3">
          <p><v-icon :class="s3TextClassMiddle" class="s3-icon">memory</v-icon></p>
          <p :class="s3TextClassMiddle" style="font-size: 26px;color: #5a5a5a">Algorithmes d'apprentissage.</p>
        </v-flex>

        <v-flex xs12 sm6 md3 class="pa-3">
          <p ><v-icon  :class="s3TextClassMiddle" class="s3-icon">school</v-icon></p>
          <p :class="s3TextClassMiddle" style="font-size: 26px;color: #5a5a5a">Rejoingnez une classe.</p>
        </v-flex>

        <v-flex xs12 sm6 md3 class="pa-3" :class="s3TextClassRight">
          <p><v-icon class="s3-icon">language</v-icon></p>
          <p style="font-size: 26px;color: #5a5a5a" >Intéragissez avec votre enseignant.</p>
        </v-flex>

      </v-layout>
    </v-container>



    <!-------------->
    <!-- Fourth Section -->
    <!-------------->
    <v-parallax :src="sky" style="height:auto;padding-top: 80px;padding-bottom: 80px">
      <v-parallax :src="stars" height="11000" style="position:absolute; width:100vw">
      </v-parallax>
      <v-parallax :src="stars" height="5000" style="position:absolute; width:100vw">
      </v-parallax>
      <v-layout row wrap >
        <v-flex xs12 sm12 md6 class="text-xs-center" style="padding: 5%">
          <img :class="s4IphoneImgClass" :src="iphone" height="420px">
          <h3 style="color: #f5f5f5; margin-top: 10px" :class="s4IphoneTextClass">Disponible à télécharger sur votre iPhone.</h3>
          <v-btn :class="s4IphoneTextClass" style="border-radius: 10px;background-color: #27629E;color: white;width:180px;height:50px;font-size: 15px" large>
              AppStore
          </v-btn>
        </v-flex>
        <v-flex xs12 sm12 md6 class="text-xs-center" style="padding: 5%">
          <img :class="s4AndroidImgClass" :src="android" height="420px">
          <h3 style="color: #f5f5f5; margin-top: 10px" :class="s4AndroidTextClass">Ou alors sur votre appareil Android.</h3>
          <v-btn :class="s4AndroidTextClass" style="border-radius: 10px;background-color: #27629E;color: white;width:180px;height:50px;font-size: 15px" large>
              Google Play Store
          </v-btn>
        </v-flex>
      </v-layout>
    </v-parallax>




    <!-------------->
    <!-- Footer -->
    <!-------------->
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

  </div>
</template>



<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--//////////////////////////////////////////////////////////SCRIPT/////////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->



<script>
import BGFrontPage from "@/assets/HomepageBackgroundFinal.png";
import Iphone from "@/assets/iphone.png";
import Android from "@/assets/android.png";
import sky from "@/assets/sky.png";
import stars from "@/assets/stars.png";
import logo from "@/assets/logoFlatWhite.png";

export default {
	data() {
		return {
			BGFrontPageSRC: BGFrontPage,

			iphone: Iphone,
			android: Android,
			sky: sky,
			logo: logo,
			stars: stars,
			s1TextClass: "s1-text-hide",
			s2IphoneClass: "s2-iphone-hide",
			s2TextClass: "s2-text-hide",
			s3MainTextClass: "s3-main-text-hide",
			s3TextClassLeft: "s3-text-left-hide",
			s3TextClassRight: "s3-text-right-hide",
			s3TextClassMiddle: "s3-text-middle-hide",
			s4IphoneTextClass: "s4-iphone-text-hide",
			s4IphoneImgClass: "s4-iphone-img-hide",
			s4AndroidTextClass: "s4-android-text-hide",
			s4AndroidImgClass: "s4-android-img-hide",
			headlineTexts: ["Le Vocabulaire", "La Grammaire", "L'Orthographe", "Vocs"]
		};
	},
	methods: {
		/*************/
		/* Method To Test The Scroll Level To Play Animations */
		/*************/
		scroll(e) {
			this.offsetTop = window.pageYOffset || document.documentElement.scrollTop;
			if (this.offsetTop > 300) {
				this.s2IphoneClass = "s2-iphone-show";
				this.s2TextClass = "s2-text-show";
			} else if (this.offsetTop < 280) {
				this.s2IphoneClass = "s2-iphone-hide";
				this.s2TextClass = "s2-text-hide";
			}
			if (this.offsetTop > 750) {
				this.s3MainTextClass = "s3-main-text-show";
			}
			if (this.offsetTop > 800) {
				this.s3TextClassLeft = "s3-text-left-show";
				this.s3TextClassRight = "s3-text-right-show";
			}
			if (this.offsetTop > 900) {
				this.s3TextClassMiddle = "s3-text-middle-show";
			}
			if (this.offsetTop < 700) {
				this.s3MainTextClass = "s3-main-text-hide";
				this.s3TextClassLeft = "s3-text-left-hide";
				this.s3TextClassRight = "s3-text-right-hide";
				this.s3TextClassMiddle = "s3-text-middle-hide";
			}
			if (this.offsetTop > 1300) {
				this.s4IphoneTextClass = "s4-iphone-text-show";
				this.s4IphoneImgClass = "s4-iphone-img-show";
				this.s4AndroidTextClass = "s4-android-text-show";
				this.s4AndroidImgClass = "s4-android-img-show";
			}
			if (this.offsetTop < 1300) {
				this.s4IphoneTextClass = "s4-iphone-text-hide";
				this.s4IphoneImgClass = "s4-iphone-img-hide";
				this.s4AndroidTextClass = "s4-android-text-hide";
				this.s4AndroidImgClass = "s4-android-img-hide";
			}
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
		this.$store.dispatch("setIsPlayingGame", false);
	}
};
</script>



<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--///////////////////////////////////////////////////////////STYLE/////////////////////////////////////////////////////////// -->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->
<!--////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////-->



<style scoped>
.textSlide {
	color: white;
	font-size: 4em;
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
.s2-text-hide {
	transform: translateX(300%);
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s2-text-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s3-box {
	height: 220px;
}
.s3-icon {
	font-size: 100px;
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
	opacity: 0;
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
.s4-iphone-text-hide {
	transform: translateX(-300%);
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s4-iphone-text-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s4-iphone-img-hide {
	transform: translatex(-300%);
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s4-iphone-img-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s4-android-text-hide {
	transform: translateX(300%);
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s4-android-text-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s4-android-img-hide {
	transform: translateX(300%);
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
.s4-android-img-show {
	transition: transform 0.7s cubic-bezier(0.6, 0, 0.07, 1);
}
</style>
