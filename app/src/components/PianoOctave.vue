<template>
  <div class="flex gap-0 w-auto">
    <button 
      v-for="key in keys"
      :key="key.note"
      @mousedown="noteOn(key.note)"  
      @mouseup="noteOff(key.note)" 
      @mouseleave="noteOff(key.note)" 
      class="key"
      :class="{
        'key-white': !key.black,
        'key-black': key.black,
        'force-active': (this.pressedKeys && this.pressedKeys[key.note]) ?? false
      }"
    ></button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      isMouseDown: false
    }
  },
  props: {
    'lowOctave': Number,
    'highOctave': Number,
    'pressedKeys': Object
  },
  computed: {
    keys(){
      const notes = ['C','C#','D','D#','E','F','F#','G','G#','A','A#','B'];
      let keys = [];
      for (let i = this.lowOctave; i <= this.highOctave; i++){
        notes.forEach(n => {
          let currentKey = {
            note: n + i,
            black: n.includes('#')
          }
          keys.push(currentKey);
        });
      }
      return keys;
    }
  },
  methods: {
    noteOn(note){
      this.isMouseDown = true;
      this.$emit("noteOn", note)
    },
    noteOff(note){
      if (this.isMouseDown){
        this.isMouseDown = false;
        this.$emit("noteOff", note)
      }
    },
    noteEnter(note){
      if (this.isMouseDown){ 
        this.noteOn(note);
      }
    }
  }
}
</script>

<style scoped>
.key {
  cursor: pointer;
}

.key-white {
  width: .75rem;
  height: 5rem;
  background-color: #fff8;
}
.key-white.force-active,
.key-white:active {
  background-color: #fff;
}

.key-black {
  z-index: 10;
  width: .50rem;
  height: 3rem;
  margin-left: -.25rem;
  margin-right: -.25rem;
  background-color: #007ACC;
}
.key-black.force-active,
.key-black:active {
  background-color: #000;
}




</style>