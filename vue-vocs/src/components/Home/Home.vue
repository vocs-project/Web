<template>
  <v-container fluid style="margin-top: 100px">
    <v-layout row wrap>



      <!-------------->
      <!-- Classes Card -->
      <!-------------->
      <v-flex xs4 wrap >
        <v-card class="white--text ml-3 mr-3" style="display: flex">
          <!-- Left Side  -->
          <div style="background-color: #26a4ff;">
            <!-- School Icon -->
            <div class="text-xs-center ml-3 mr-3 mt-4" >
              <v-icon class="white--text" style="font-size: 60px">school</v-icon>
            </div>
          </div>
          <!-- Right Side  -->
          <div style="padding-left: 4%">
            <!-- Title -->
            <div v-if="accountType !== 'Professeur' " style="padding-top: 10px;color:#26a4ff;width:100%">Ma Classe</div>
            <div v-else style="padding-top: 10px;font-size: 20px;color:#26a4ff;width:100%">Mes Classes</div>
            <!-- Subtitle -->
            <div v-if="user.roles !== 'USER' && user.classes.length === 0" style="color:black">Pas de classe</div>
            <div v-else-if="user.roles === 'USER' && user.classes.length === 0" style="color:black">Pas de classe</div>
            <div v-else style="color:black">{{user.classes[0].name}}</div>
            <!-- See Class Button -->
            <v-btn small style="margin-top: 10px; margin-bottom: 10px" to="/class">Voir</v-btn>
          </div>
        </v-card>
      </v-flex>



      <!-------------->
      <!-- Lists Card -->
      <!-------------->
      <v-flex xs4 wrap>
        <v-card class="white--text ml-3 mr-3" style="display: flex">
          <!-- Left Side  -->
          <div style="background-color: #B198DA;">
            <!-- List Icon -->
            <div class="text-xs-center ml-3 mr-3 mt-4">
              <v-icon class="white--text" style="font-size: 60px">description</v-icon>
            </div>
          </div>
          <!-- Right Side  -->
          <div style="padding-left: 4%">
            <!-- Title -->
            <div style="padding-top: 10px;color:#B198DA;font-size: 20px;width:100%">Mes Listes</div>
            <!-- Subtitle (number of lists) -->
            <div style="color:black">{{user.lists.length}} liste(s)</div>
            <!-- See Lists Button -->
            <v-btn style="margin-top: 10px; margin-bottom: 10px;" small to="/lists">Voir</v-btn>
          </div>
        </v-card>
      </v-flex>


      <!-------------->
      <!-- Lists Card -->
      <!-------------->
      <v-flex xs4 wrap>
        <v-card class="white--text ml-3 mr-3" style="display: flex">
          <!-- Left Side  -->
          <div style="background-color: #6FC9C0;">
            <!-- List Icon -->
            <div class="text-xs-center ml-3 mr-3 mt-4">
              <v-icon class="white--text" style="font-size: 60px">description</v-icon>
            </div>
          </div>
          <!-- Right Side  -->
          <div style="padding-left: 4%">
            <!-- Title -->
            <div style="padding-top: 10px;color:#6FC9C0;font-size: 20px;width:100%">Mes Listes</div>
            <!-- Subtitle (number of lists) -->
            <div style="color:black">{{user.lists.length}} liste(s)</div>
            <!-- See Lists Button -->
            <v-btn style="margin-top: 10px; margin-bottom: 10px;" small to="/lists">Voir</v-btn>
          </div>
        </v-card>
      </v-flex>


      <!-------------->
      <!-- Lists Card -->
      <!-------------->
      <v-flex xs4 wrap>
        <v-card class="white--text ml-3 mr-3" style="display: flex">
          <!-- Left Side  -->
          <div style="background-color: #FF865E;">
            <!-- List Icon -->
            <div class="text-xs-center ml-3 mr-3 mt-4">
              <v-icon class="white--text" style="font-size: 60px">description</v-icon>
            </div>
          </div>
          <!-- Right Side  -->
          <div style="padding-left: 4%">
            <!-- Title -->
            <div style="padding-top: 10px;color:#FF865E;font-size: 20px;width:100%">Mes Listes</div>
            <!-- Subtitle (number of lists) -->
            <div style="color:black">{{user.lists.length}} liste(s)</div>
            <!-- See Lists Button -->
            <v-btn style="margin-top: 10px; margin-bottom: 10px;" small to="/lists">Voir</v-btn>
          </div>
        </v-card>
      </v-flex>


    </v-layout>


  </v-container>
</template>

<script>
  import ListBG from '@/assets/HomepageBG4.png'
  export default {
    data () {
      return {
        listBG: ListBG
      }
    },
    computed: {
      user () {
        return this.$store.getters.user
      },
      accountType () {
        if (this.user.roles === 'STUDENT' || JSON.stringify(this.user.roles) === '["ROLE_STUDENT"]') {
          return 'Élève';
        } else if (this.user.roles === 'PROFESSOR' || JSON.stringify(this.user.roles) === '["ROLE_PROFESSOR"]') {
          return 'Professeur';
        } else {
          return 'Libre';
        }
      }
    },
    created () {
      this.$store.dispatch('setIsPlayingGame', false)
    }
  }
</script>
