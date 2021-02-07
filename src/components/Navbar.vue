<template>
  <nav>
    <v-toolbar app dark>
     <v-toolbar-side-icon class="grey--text"   @click="drawer = !drawer">
       <v-icon>more_hor</v-icon>
     </v-toolbar-side-icon>
       <v-toolbar-title class="text-uppercase grey--text" >
          <span class="font-weight-light">Starfish</span>
          <span>BOOTCAMP</span>
       </v-toolbar-title> 
       <v-spacer></v-spacer>
       <v-btn  color="grey">
        <span>Sign Out</span>
        <v-icon right>exit_to_app</v-icon>
        </v-btn>
    </v-toolbar>
    <v-navigation-drawer app v-model="drawer" dark>
      <span>Hello</span>
    </v-navigation-drawer>
  </nav>
</template>
<script>
export default {
  data () {
    return {
      drawer: false
    }
  }
};
</script>
