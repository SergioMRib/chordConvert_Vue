<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <div id="container">
      <Lists />
      <Lists />
      <SongList />
    </div>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import Lists from '../components/Lists.vue';
import SongList from '../components/SongList.vue';
/* import HelloWorld from '@/components/HelloWorld.vue' */

export default {
  name: 'home',
  components: {
    Lists,
    SongList
    /* HelloWorld */
  },
  data() {
    return {
      chords: [{
            pos:1,
            name:"A"
        },
        {
            pos:2,
            name: "A#"
        },
        {
            pos:3,
            name:"B"
        },
        {
            pos:4,
            name:"C"
        },
        {
            pos:5,
            name:"C#"
        },
        {
            pos:6,
            name:"D"
        },
        {
            pos:7,
            name:"D#"
        },
        {
            pos:8,
            name:"E"
        },
        {
            pos:9,
            name:"F"
        },
        {
            pos:10,
            name:"F#"
        },
        {
            pos:11,
            name:"G"
        },
        {
            pos:12,
            name:"G#"
        }
      ],
      modifiers: [
        {}
      ]
    }
  }
}
</script>

