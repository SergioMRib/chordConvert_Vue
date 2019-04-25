<template>
  <div class="home">
    <div id="container">

      <ul class="song-list">
        <Chord
          v-bind:key="item.id"
          v-for="item in songChords"
          v-bind:item="item"
          v-on:selected="selectChord"
          v-on:click="selectChord"
          v-bind:class="{selected: item.selected}">
        </Chord>
      </ul>

      <ul class="list-of-chords">
        <Chord
          v-bind:key="item.pos"
          v-for="item in chords"
          v-bind:item="item"
          v-on:selected="addChord">
        </Chord>
      </ul>

      <ul classs="list-of-modifiers">
        <Modifier
            v-bind:key="item.pos"
            v-for="item in modifiers"
            v-bind:item="item"
            v-on:selected="addModifier">
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
// import SongList from '../components/SongList.vue';
import Chord from '../components/Chord.vue';
import Modifier from '../components/Modifier.vue';
/* import HelloWorld from '@/components/HelloWorld.vue' */

export default {
  name: 'home',
  components: {
    Lists,
    /* SongList, */
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
      /**
       *
      */
      console.log("added a chord")
      this.songChords.forEach(function (element) {
        element.selected = false;
      });
      const newChord = {
        id: uuid.v4(),
        pos: data.pos,
        name: data.name,
        mod: "",
        selected: true
      };
      this.songChords.push(newChord);
    },
    removeChord: function(data) {
      let index = this.songChords.findIndex(x => x.id === data.id)
      this.songChords.splice(index, 1)
    },
    selectChord: function(data) {
      console.log('selected this chord')
      this.songChords.forEach(function (element) {
        element.selected = false;
      })
      data.selected = true
      console.log(this.activeChord)
    },
    addModifier: function(data) {
      console.log("hello")
      if (typeof(this.activeChord) !== 'undefined') {
        this.activeChord.mod += data.name
      }
    }
  },
  computed: {
    activeChord: function() {
        /* still in development */
      let index = this.songChords.findIndex(x => x.selected === true)
      return this.songChords[index]
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
