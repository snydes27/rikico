<template>
  <div id="app">
    <Navigation 
      :user="user"
      @logout="logout"
    />  
    <router-view 
      class="container"
      :user="user"
      :scraps="scraps"
      @logout="logout"
      @saveScrap="saveScrap"
    />
  </div>
</template>

<script>
import Navigation from "@/components/Navigation.vue";
import Firebase from "firebase";
import db from "./db.js";

  export default {
  name: "app",
  data: function() {
    return {
      user: null,
      error: null,
      scraps: []
      
    }
  },
  methods: {
    logout: function() {
      Firebase.auth()
        .signOut()
        .then(() => {
          this.user = null;
          this.$router.push("login");
        });
    },
    saveScrap: function(payload) {
      db.collection("users")
      .doc(this.user.uid)
      .collection("lyricScrap")
      .add({
        title: payload.title,
        scrapBody: payload.scrapBody,
        tag: payload.tag,
        createdAt: Firebase.firestore.FieldValue.serverTimestamp()
      })
      .then(
        () => {
          this.$router.push("/")
        }, error => {
          this.error = error.message;
        }
      );
    }
  },
  mounted() {
    Firebase.auth().onAuthStateChanged(user => {
      if (user) {
        this.user = user;

        db.collection("users")
          .doc(this.user.uid)
          .collection("lyricScrap")
          .onSnapshot(querySnapshot => {
            querySnapshot.forEach(doc => {
              this.scraps.push({
                id: doc.id,
                scrapBody: doc.data().scrapBody,
                //'recorded': doc.data().recorded,
                tag: doc.data().tag,
                title: doc.data().title
              });
              
            });
          });
      }
    });
    
  },
  components: { 
    Navigation
  }
 
};

</script>

<style lang="scss">

$primary: #91B6BF;
@import 'node_modules/bootstrap/scss/bootstrap';
@import 'node_modules/bootstrap-vue/src/index.scss';
</style>

