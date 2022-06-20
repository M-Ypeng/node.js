<template>
  <div id="app" ref="vantaRef">
    <router-view />

    <div class="switchThemes">
      <el-select @change="themesChange" v-model="themes" placeholder="请选择">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
    </div>
  </div>
</template>

<script>
import FOG from "vanta/src/vanta.fog";
import NET from "vanta/src/vanta.net";
import GLOBE from "vanta/src/vanta.globe.js";
import * as THREE from "three";
export default {
  data() {
    return {
      themes: "GLOBE",
      options: [
        {
          value: "GLOBE",
          label: "GLOBE",
        },
        {
          value: "FOG",
          label: "FOG",
        },
        {
          value: "NET",
          label: "NET",
        },
      ],
    };
  },
  methods: {
    themesChange(e) {
      console.log(e);
      if (e) {
        this.vantaEffect.destroy();
        switch (e) {
          case "GLOBE":
            this.vantaEffect = GLOBE({
              el: this.$refs.vantaRef,
              THREE: THREE,
            });
            break;
          case "FOG":
            this.vantaEffect = FOG({
              el: this.$refs.vantaRef,
              THREE: THREE,
            });
            break;
          case "NET":
            this.vantaEffect = NET({
              el: this.$refs.vantaRef,
              THREE: THREE,
            });
            break;
          default:
            break;
        }
      }
    },
  },
  mounted() {
    this.vantaEffect = GLOBE({
      el: this.$refs.vantaRef,
      THREE: THREE,
    });
  },
  beforeDestroy() {
    if (this.vantaEffect) {
      this.vantaEffect.destroy();
    }
  },
};
</script>
<style>
body,
html {
  height: 100%;
  overflow: hidden;
}
#app {
  width: 100%;
  height: 97.6%;
  background-color: pink;
}
.switchThemes {
  width: 120px;
  position: fixed;
  top: 20px;
  right: 20px;
}
</style>
