<-- this is for both chords and modifiers list -->

<template>
    <ul>
        <slot></slot>
    </ul>
</template>

<script>
import Chord from './Chord.vue'

export default {
    name: 'lists',
    components: {
        Chord
    },
    props: ["itemsList"],

}
</script>

<style scoped>
    .list {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }

</style>
