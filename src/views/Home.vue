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
          v-bind:class="{selected: item.selected, fullLine: item.fullLine}"
          class="song-list-chord">
        </Chord>
      </ul>

      <div id="usables">
        <ul class="list-of-chords">
          <Chord
            v-bind:key="item.pos"
            v-for="item in chords"
            v-bind:item="item"
            v-on:selected="addChord"
            class="chord-selectable">
          </Chord>
        </ul>

        <ul class="list-of-modifiers">
          <Modifier
              v-bind:key="item.pos"
              v-for="item in modifiers"
              v-bind:item="item"
              v-on:selected="addModifier"
              class="modifier-selectable">
          </Modifier>
        </ul>
        <div class="action-buttons">
          <button
            v-on:click="removeChord">
            <font-awesome-icon icon="eraser" />
          </button>
          <button
            v-on:click="convert(1)">
            <font-awesome-icon icon="arrow-alt-circle-up" />
          </button>
          <button
            v-on:click="songChords = []">
            <font-awesome-icon icon="trash" />
          </button>
          <button
            v-on:click="convert(-1)">
            <font-awesome-icon icon="arrow-alt-circle-up" />
          </button>
          <button id="add-line-button"
            v-on:click="addLine">
            <font-awesome-icon icon="level-down-alt" />
          </button>
        </div>
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
        // remove it
        let index = this.songChords.findIndex(x => x.id === this.activeChord.id)
        this.songChords.splice(index, 1)

        // select the next chord
        this.songChords[index].selected = true;

      } else {
        console.log("select a chord");
      }
    },
    selectChord: function(data) {
      console.log('selected this chord')
      this.songChords.forEach(function (element) {
        element.selected = false;
      })
      data.selected = !data.selected // toggles true and false
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
        if (element.fullLine != true) {

          let val = element.pos + direction;
          if (val > 11) {
            val = 0;
          }
          if (val < 0 ) {
            val = 11;
          }

          element.name = this.chords[val].name;
          element.pos = val;
        }
      });
    },
    addLine: function() {
      /* Creates a new empty chord object that fills all cells of the grid
       *
       */
      let emptyChord = {
        id: uuid.v4(),
        pos: "",
        name: "_",
        mod: "",
        fullLine: true,
        selected: false
      };
      this.songChords.push(emptyChord);

      console.log("added line");
    }
  },
  computed: {
    activeChord: function() {
        /* still in development */
      let index = this.songChords.findIndex(x => x.selected === true)
      return this.songChords[index]
    }
  },
  mounted() {
    if (localStorage.chords) {
        this.songChords = JSON.parse(sessionStorage.chords)
    }
  },
  watch: {
    songChords: function () {
      if (typeof(Storage) !== "undefined") {
        sessionStorage.setItem('chords', JSON.stringify(this.songChords))
      }
    },
  }
}
</script>

<style scoped>

  #container {
    background-color: rgb(57, 73, 96);
  }

  .song-list {
    display: grid;
    box-sizing: border-box;
    padding: 5px;
    grid-template-columns: repeat(8,1fr);
    grid-gap: 7px;
  }

  .song-list-chord {

    font-size: 1.3em;
    color: #fd9800;
    font-weight: bold;
  }
  .fullLine {
    grid-column-end: -1;

  }
  #usables {
    position: fixed;
    bottom: 5px;
    width: 100%;
    padding: 1px;
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    grid-gap: 3px;
    background-color: #70480c;
  }

  .chord-selectable, .modifier-selectable {
    font-size: 1em;
    vertical-align: middle;
    line-height: 2em;
    border-right: 2px solid #555f72;
    border-bottom: 2px solid #555f72;
    border-radius: 5px;
    background-color: #26334a;
  }

  .modifier-selectable {
    color: rgb(54, 184, 166);
    background-color: #698c7b;
  }

  .list-of-chords, .list-of-modifiers, .action-buttons {
    display: grid;
    grid-gap: 2px;
    justify-items: stretch;
    align-items: stretch;
    margin: 0;
  }
  .list-of-chords {
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-template-rows: repeat(3, 2em);
  }
  .list-of-modifiers {
    grid-template-columns: 1fr 1fr;
    grid-template-rows: repeat(3, 2em);
  }

  .action-buttons{
    grid-template-columns: 1fr 1fr;
    grid-template-rows: repeat(3, 2em);
    margin: 0;
  }
  .svg-inline--fa {
    font-size: 1.5em;
  }
  #add-line-button {
    grid-column: span 2;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }
</style>
