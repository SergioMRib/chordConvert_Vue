<template>
  <div class="home">
    <div id="container">
      <SongList />

      <Lists
          v-bind:key="item.pos"
          v-for="item in chords">
        <Chord v-bind:item="item"/>
      </Lists>

      <Lists
          v-bind:key="item.pos"
          v-for="item in modifiers">
        <Modifier v-bind:item="item"/>
      </Lists>
    </div>

    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import Lists from '../components/Lists.vue';
import SongList from '../components/SongList.vue';
import Chord from '../components/Chord.vue';
import Modifier from '../components/Modifier.vue';
/* import HelloWorld from '@/components/HelloWorld.vue' */

export default {
  name: 'home',
  components: {
    Lists,
    SongList,
    Chord,
    Modifier
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
        {
          pos:1,
          name:"m"},
        {
          pos:2,
          name: "M"
        },
        {
          pos:3,
          name:"7"},
        {
          pos:4,
          name:"9"
        },
        {
          pos:5,
          name:"sus"
          },
        {
          pos:6,
          name:"dim"
        }
      ]
    }
  }
}
</script>

<style scoped>
  #container {
    display: grid;
    grid-template-columns: 5fr 1fr 1fr;
  }
</style>
