<template>
  <div class="relative">
    <!-- Notes -->
    <div class="absolute z-50 border-2 border-transparent">
      <div class="absolute">
        <div class="absolute text-[68px] -mt-[28px] text-black text-start ms-1 w-auto">𝄞</div>
        <div class="absolute text-[48px] mt-[54px] text-black text-start ms-1 w-auto">𝄢</div>
      </div>
      <div class="absolute left-[48px]">
        <div class="flex relative w-auto h-auto">
          <div class="px-[15px]" v-for="(column, colindex) in music.notes" :key="colindex">
            <div
              v-for="(note, noteindex) in column" 
              :key="noteindex" 
              :class="getNoteClass(note)"
              :style="getNoteStyle(note)"
            ></div>
          </div>
        </div>

      </div>

    </div>
    <!-- White lines -->
    <div class="relative flex border-2 border-neutral-800 flex-col min-w-[600px] ">
      <div class="line white"></div>
      <div class="divisor"></div>
      <div class="line white"></div>
      <div class="divisor"></div>
      <div class="line white"></div>
      <div class="divisor"></div>
      <div class="line white"></div>
      <div class="divisor"></div>
      <div class="h-[22px]"></div>
      <div class="divisor"></div>
      <div class="line white"></div>
      <div class="divisor"></div>
      <div class="line white"></div>
      <div class="divisor"></div>
      <div class="line white"></div>
      <div class="divisor"></div>
      <div class="line white"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      music: {
        notes: [
          [ { key: 'C4', duration: 2 } ],
          [ { key: 'C4', duration: 2 } ],
          [ { key: 'D4', duration: 4 } ],
          [ { key: 'C4', duration: 2 } ],
          [ { key: 'G4', duration: 4 } ],
          [ { key: 'F4', duration: 2 } ]
        ]
      }
    }
  },
  methods: {
    getNoteClass(note) {
      let black = false, white = false;
      if (note.duration == 4){
        white = true;
      } else {
        black = true;
      }

      return {
        note: true,
        skew: true,
        black: black,
        white: white
      }
    },
    getNoteStyle(note) {
      let px = 0;
      const noteLocations = {
        C2: 138,
        D2: 132,
        E2: 126,
        F2: 120,
        G2: 114,
        A2: 108,
        B2: 102,
        C3: 96,
        D3: 90,
        E3: 84,
        F3: 78,
        G3: 72,
        A3: 66,
        B3: 60,
        C4: 54,
        D4: 48,
        E4: 42,
        F4: 36,
        G4: 30,
        A4: 24,
        B4: 18,
        C5: 12,
        D5: 6,
        E5: 0,
        F5: -6,
        G5: -12,
        A5: -18,
        B5: -24,
      }
      if (note.key in noteLocations){
        px = noteLocations[note.key];
      }
      return {
        top: px + 'px'
      };
    }
  }
}
</script>

<style scoped>
.line {
  height: 10px;
}

.line.white {
  background-color: #fff;
}

.divisor {
  background-color: #000;
  height: 2px;
}

.note {
  position: absolute;
  border-radius: 50px;
  width: 10px;
  height: 10px;
}

.note.skew {
  transform: skew(-.3rad);
  rotate: x 20deg;
}

.note.black {
  background-color: #000;
  border: 2px solid #000;
}

.note.white {
  background-color: #fff;
  border: 1px solid #000;
}

.note.half-up {
  transform: translateY(-50%);
}</style>