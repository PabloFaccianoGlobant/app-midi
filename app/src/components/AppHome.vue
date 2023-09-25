<template>
  <div class="flex flex-col items-center justify-evenly h-screen bg-[#007ACC]">

    <button class="bg-neutral-100 px-4 py-2 rounded" @click="start" v-if="!isConnected">Connect</button>
    
    <PianoSheet v-if="isConnected" />
    
    <PianoOctave :pressedKeys="currentKeys" @noteOn="doNoteOn($event)" @noteOff="doNoteOff($event)" v-if="isConnected" :lowOctave="2" :highOctave="6" />

  </div>
</template>

<script>
import {WebMidi} from "webmidi";
import PianoOctave from './PianoOctave.vue';
import PianoSheet from './PianoSheet.vue';

export default {
  components: { PianoOctave, PianoSheet },
  data(){
    return {
      WebMidi: null,
      synthIn: null,
      synthOut: null,
      isConnected: false,
      currentKeys: {}
    }
  },
  methods: {
    async connect(){
      this.WebMidi = WebMidi;
      await WebMidi.enable();

      if (WebMidi.inputs.length == 0) {
        throw new Error("No device found.")
      }

      this.isConnected = true;

      this.synthIn = WebMidi.inputs[0];
      this.synthOut = WebMidi.outputs[0];

      this.synthIn.channels[1].addListener("noteon", this.onNoteOn);
      this.synthIn.channels[1].addListener("noteoff", this.onNoteOff);
      this.synthOut.sendAllSoundOff()

    },
    onNoteOn(e){
      this.currentKeys[e.note.identifier] = true;
      console.log("onNoteOn", e.note.identifier, e.message.channel)
      // e.note.identified
    },
    onNoteOff(e){
      this.currentKeys[e.note.identifier] = false;
      console.log("onNoteOff", e.note.identifier, e.message.channel)
      // e.note.identified
    },
    doNoteOn(key){
      console.log("DO NoteOn", key)
      this.synthOut.channels[1].playNote(key)

    },
    doNoteOff(key){
      console.log("DO NoteOff", key)
      this.synthOut.channels[1].stopNote(key);
    },
    async start(){
      if(this.isConnected){ return; }
      try {
        this.$notify({
          title: "Connection",
          text: "Loading MIDI devices."
        });
        await this.connect();
        this.$notify({
          clean: true
        });
        this.$notify({
          title: "Connection",
          text: `Connected to [${WebMidi.inputs[0].name}]`,
        });
      } catch (error) {
        this.$notify({
          title: "Connection",
          text: "Error: " + error.message,
          type: "error"
        });
      }
    }
  },
  mounted(){
    console.clear();
    this.start();
  }
}
</script>