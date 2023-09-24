<template>
  <div class="flex flex-col items-center justify-evenly h-screen bg-[#007ACC]">
    
    <PianoSheet />
    
    <PianoOctave :count="5" />

  </div>
</template>

<script>
import PianoOctave from './PianoOctave.vue';
import PianoSheet from './PianoSheet.vue';

export default {
  components: { PianoOctave, PianoSheet }
}
</script>