<script setup lang="ts">
import "../assets/font_7nqilmsz3m/iconfont.css";
import { computed, onMounted, reactive, ref } from "vue";

const props = defineProps({
  text: {
    type: String,
    default: "placeholder...",
  },
  fontSize: {
    type: Number,
    default: 30,
  },
  textColor: {
    type: String,
    default: "#000000",
  },
  cursorColor: {
    type: String,
    default: "#000000",
  },
});

const textStyle = reactive({
  fontSize: `${props.fontSize}px`,
  color: `${props.textColor}`,
});
const inputText = ref("");
const typing = () => {
  let cacheText = props.text;
  let fromLeft = true;
  let point = 0;

  const changeText = () => {
    setInterval(() => {
      inputText.value = cacheText.substring(0, point);
      if (fromLeft) {
        point++;
        if (point > cacheText.length) {
          fromLeft = false;
        }
      } else {
        point--;
        if (point === 0) {
          fromLeft = true;
          cacheText = props.text;
        }
      }
    }, 200);
  };
  changeText();
};

const cursorStyle = reactive({
  fontSize: `${props.fontSize}px`,
  color: `${props.cursorColor}`,
});
const showCursor = ref(true);
const toggleCursor = () => {
  setInterval(() => {
    showCursor.value = !showCursor.value;
  }, 100);
};

onMounted(() => {
  typing();
  toggleCursor();
});
</script>

<template>
  <div class="auto-typer">
    <span :style="textStyle" v-html="inputText"></span>
    <transition name="fade">
      <i
        v-show="showCursor"
        class="iconfont icon-icursor"
        :style="cursorStyle"
      ></i>
    </transition>
  </div>
</template>

<style scoped>
.fade-leave-active {
  transition: opacity 0.1s;
}

.fade-leave-to {
  opacity: 0;
}
</style>
