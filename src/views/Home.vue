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
      <div>
        <button
          v-on:click="removeChord">
          Delete chord
        </button>
        <button
          v-on:click="songChords = []">
          Clear all
        </button>
      </div>
      <div>
        <button
          v-on:click="convert(1)">
          UP
        </button>
        <button
          v-on:click="convert(-1)">
          Down
        </button>
      </div>
    </div>

    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import uuid from 'uuid'


// import SongList from '../components/SongList.vue';
import Chord from '../components/Chord.vue';
import Modifier from '../components/Modifier.vue';
/* import HelloWorld from '@/components/HelloWorld.vue' */

export default {
  name: 'home',
  components: {
    /* SongList, */
    Chord,
    Modifier
    /* HelloWorld */
  },
  data() {
    return {
      chords: [{
            pos:0,
            name:"A"
        },
        {
            pos:1,
            name: "A#"
        },
        {
            pos:2,
            name:"B"
        },
        {
            pos:3,
            name:"C"
        },
        {
            pos:4,
            name:"C#"
        },
        {
            pos:5,
            name:"D"
        },
        {
            pos:6,
            name:"D#"
        },
        {
            pos:7,
            name:"E"
        },
         {
            pos:8,
            name:"F"
        },
        {
            pos:9,
            name:"F#"
        },
        {
            pos:10,
            name:"G"
        },
        {
            pos:11,
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
    removeChord: function() {
      console.log("removed the chord")
      if (typeof(this.activeChord) !== 'undefined') {
        let index = this.songChords.findIndex(x => x.id === this.activeChord.id)
        this.songChords.splice(index, 1)
      } else {
        console.log("select a chord");
      }
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
    },
    convert: function(direction) {
      /**
       * for each element of the songChords update its .name and .pos properties
       */
      console.log("raise the chords " + direction);

      // gets the current list of chord positions and increases/decreases
      this.songChords.forEach( element => {

        let val = element.pos + direction;
        if (val > 11) {
          val = 0;
        };
        if (val < 0 ) {
          val = 11;
        };

        element.name = this.chords[val].name;
        element.pos = val;
      });
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
