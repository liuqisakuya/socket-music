<template>
  <div class="container">
    <i class="material-icons md-36" @click="prev">skip_previous</i>
    <i class="material-icons md-36" @click="pauseAudio">{{audio.playing ? 'pause' : 'play_arrow'}}</i>
    <i class="material-icons md-36" @click="changePlayMode">{{playList.playMode}}</i>
    <i class="material-icons md-36" @click="next">skip_next</i>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  computed: mapState(['audio', 'playList']),
  methods: {
    ...mapActions(['pauseAudio', 'listGoNext', 'listGoPrev', 'changePlayMode', 'randomPlay']),
    next() {
      const { playMode } = this.playList;
      switch (playMode) {
        case 'shuffle':
          this.randomPlay();
          break;
        default:
          this.listGoNext();
      }
    },
    prev() {
      const { playMode } = this.playList;
      switch (playMode) {
        case 'shuffle':
          this.randomPlay();
          break;
        default:
          this.listGoPrev();
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../assets/stylesheets/base/_vars.scss";

  .container {
    display: inline-block;
    height: 65px;
    line-height: 65px;
    float: right;
    margin-right: 20px;
  }
  .material-icons {
    margin: 0 5px;
    cursor: pointer;
    color: #475669;
  }
</style>
