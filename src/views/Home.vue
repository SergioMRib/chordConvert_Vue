<template>
  <div class="home">
    <div id="container">

      <ul>
        <SongList
          v-bind:key="item.id"
          v-for="item in songChords"
          v-bind:item="item"
          v-on:selected="removeChord">
        </SongList>
      </ul>

      <ul>
        <Chord
          v-bind:key="item.pos"
          v-for="item in chords"
          v-bind:item="item"
          v-on:selected="addChord">
        </Chord>
      </ul>

      <ul>
        <Modifier
            v-bind:key="item.pos"
            v-for="item in modifiers"
            v-bind:item="item">
        </Modifier>
      </ul>
    </div>

    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import uuid from 'uuid'

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
      ],
      songChords: []
    }
  },
  methods: {
    hello: function(data) {
      console.log(data.name + " and position is: " + data.pos)
    },
    addChord: function(data) {
      const newChord = {
        id: uuid.v4(),
        pos: data.pos,
        name: data.name,
        mod: "",
      };
      this.songChords.push(newChord)
    },
    removeChord: function(data) {
      let index = this.songChords.findIndex(x => x.id === data.id)
      this.songChords.splice(index, 1)
    }
  }
}
</script>

<style scoped>
  #container {
    display: grid;
    grid-template-columns: 7fr 1fr 1fr;
  }

  ul {
    list-style-type: none;
  }
</style>
