<-- This will be used for chords -->

<template>
    <li v-on:click="selected(item)">
        {{item.name}}
    </li>
</template>

<script>
export default {
    name: 'chord-item',
    props: ['item'],
    data() {
        return {}
    },
    methods: {
        selected: function(data) {
            this.$emit('selected', data)
        }
    }
}
</script>

<style scoped>
li {
    margin-top: 3px;
    margin-bottom: 3px;
    border-top: 1px solid #96d1f8;
    background: #65a9d7;
    background: -webkit-gradient(linear, left top, left bottom, from(#3e779d), to(#65a9d7));
    background: -webkit-linear-gradient(top, #3e779d, #65a9d7);
    background: -moz-linear-gradient(top, #3e779d, #65a9d7);
    background: -ms-linear-gradient(top, #3e779d, #65a9d7);
    background: -o-linear-gradient(top, #3e779d, #65a9d7);
    padding: 5px 10px;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    border-radius: 8px;
    -webkit-box-shadow: rgba(0,0,0,1) 0 1px 0;
    -moz-box-shadow: rgba(0,0,0,1) 0 1px 0;
    box-shadow: rgba(0,0,0,1) 0 1px 0;
    text-shadow: rgba(0,0,0,.4) 0 1px 0;
    color: white;
    font-size: 15px;
    font-family: Helvetica, Arial, Sans-Serif;
    text-decoration: none;
    vertical-align: middle;
}
li:hover {
   border-top-color: #28597a;
   background: #28597a;
   color: #ccc;
   cursor: pointer;
}

li:active {
   border-top-color: #1b435e;
   background: #1b435e;
}

</style>

