<template>
  <div class="inputComponent">
    <div class="hsk-input">
      <label for="hsk-input">HSK Input: </label>
      <input type="text" v-model="message" placeholder="Input HSK words..." class="hsk-input" />
    </div>
    <div id="hsk-zoom" class="hsk-zoom">
      {{message}}
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';
import HanziWriter from 'hanzi-writer';

let hanziWriter = null;
const message = ref('');

onMounted(() => {
  hanziWriter = HanziWriter.create('hsk-zoom', message.value || '你', {
    width: 300,
    height: 300,
    padding: 5,
  });
});

watch(message, (newValue) => {
  if (newValue) {
    hanziWriter.setCharacter(newValue);
    hanziWriter.loopCharacterAnimation();
    componentKey.value++;
  }
});
</script>


<style scoped>
.inputComponent {
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: space-between;
  margin: 2%;
  height: 100%;
}

.hsk-input {
  font-size: 1.3rem;
}

.hsk-zoom {
  width: 100%;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  background: #C8C8C8;
  padding: 2%;
  margin-left: 10px;
  font: 20em sans-serif;
}
</style>
