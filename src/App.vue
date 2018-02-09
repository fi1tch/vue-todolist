<template>
<v-app dark>
<v-layout row>
   <v-flex xs12 sm6 offset-sm3>
     <v-card>
  <v-toolbar dark color="primary">
    <v-toolbar-side-icon color ="red" ></v-toolbar-side-icon>
    <v-toolbar-title class="red--text">TO-DO</v-toolbar-title>
    <v-spacer></v-spacer>

    <v-dialog v-model="dialog">
    <v-btn icon slot="activator">
      <v-icon color ="red">edit</v-icon>
    </v-btn>
    <v-card>
        <v-card-title>
          <span class="headline">New Task TO-DO</span>
        </v-card-title>
    </v-card>

    <v-card-text >
       <v-flex xs12>
                <v-text-field color ="red" label="tell me" >
                  <input color ="red" v-model="input"  class="name" ></input>
                </v-text-field>         
        </v-flex>
    </v-card-text>

     <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn  @click.native="dialog = false" id="add" @click="addNode">Add</v-btn>
    </v-card-actions>
    </v-dialog>

    <v-btn icon>
      <v-icon color ="red">search</v-icon>
    </v-btn>
    <v-btn icon>
      <v-icon color ="red">apps</v-icon>
    </v-btn>
    <v-btn icon>
      <v-icon color ="red">refresh</v-icon>
    </v-btn>
  </v-toolbar>

    <v-list>
      <template v-for="note in notes">
        <v-list-tile
              avatar
              ripple
              
              :key="note.name">
              <v-list-tile-content>
              <v-list-tile-title text-color="red" v-html="notes.name"></v-list-tile-title>
           </v-list-tile-content>
            <v-list-tile-action>
             <v-btn icon  id="delete" @click="deleteNote">
              <v-icon color="red">delete</v-icon>
            </v-btn>
            </v-list-tile-action>

            </v-list-tile>
          </template>
</v-list>  

  </v-card>
</v-flex>
</v-layout>
</v-app>
</template>



<script>
export default {
  name: 'app',
  data () {
    return {
      dialog: false,
      notes: [],
      size: 0,
      input: ''
    }
  },

  watch: {
    input: function (val) {
      if (val === '') {
        document.getElementById("add").disabled = true
      } else {
        document.getElementById("add").disabled = false
      }
    }
  },
  methods: {
   addNode() {

      var note = {
        name: this.input
      }
      this.notes.splice(++this.size)
      this.$set(this.notes, this.size - 1, note)
      this.input = ''
    },
    deleteNote (index) {
      this.notes.splice(index, 1)
      this.notes.splice(--this.size)
    }
  }
}


</script>

<style>

.input {
  color: red;
}
</style>
