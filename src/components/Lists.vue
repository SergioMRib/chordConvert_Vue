<-- this is for both chords and modifiers list -->

<template>
    <div class="list">
        <div v-bind:key="item.pos" v-for="item in itemsList">
            <p>{{item.name}}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ["itemsList"],

}
</script>

<style scoped>
    .list {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }

</style>
