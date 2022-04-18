<script lang="ts" setup>
import 'bootstrap';
import { computed, ref } from 'vue';

const blueNum = ref<number>(0);
const redNum = ref<number>(0);
const yellowNum = ref<number>(0);
const whiteNum = ref<number>(0);
const blueDisabled = ref<boolean>(false);
const redDisabled = ref<boolean>(false);
const yellowDisabled = ref<boolean>(false);
const whiteDisabled = ref<boolean>(false);
const msTimeout = 500;

const isBlue = computed(() => {
  return blueNum.value > Math.max(redNum.value, yellowNum.value, whiteNum.value);
});

const isRed = computed(() => {
  return redNum.value > Math.max(blueNum.value, yellowNum.value, whiteNum.value);
});

const isYellow = computed(() => {
  return yellowNum.value > Math.max(redNum.value, blueNum.value, whiteNum.value);
});

const isWhite = computed(() => {
  return whiteNum.value > Math.max(redNum.value, yellowNum.value, blueNum.value);
});

function addBlue() {
  blueDisabled.value = true;
  blueNum.value++;
  setTimeout(() => {
    blueDisabled.value = false;
  }, msTimeout);
}

function addRed() {
  redDisabled.value = true;
  redNum.value++;
  setTimeout(() => {
    redDisabled.value = false;
  }, msTimeout);
}

function addYellow() {
  yellowDisabled.value = true;
  yellowNum.value++;
  setTimeout(() => {
    yellowDisabled.value = false;
  }, msTimeout);
}

function addWhite() {
  whiteDisabled.value = true;
  whiteNum.value++;
  setTimeout(() => {
    whiteDisabled.value = false;
  }, msTimeout);
}
</script>

<template>
  <div class="host">
    <div class="box card">
      <div class="num card-body">
        <span class="fs-2" :class="{ 'span-green': isBlue }">{{ blueNum }}</span>
      </div>
      <div class="addel card-footer">
        <button class="btn btn-blue m-1 fs-3" @click="addBlue()" :disabled="blueDisabled">+</button>
      </div>
    </div>
    <div class="box card">
      <div class="num card-body">
        <span class="fs-2" :class="{ 'span-green': isRed }">{{ redNum }}</span>
      </div>
      <div class="addel card-footer">
        <button class="btn btn-red m-1 fs-3" @click="addRed()" :disabled="redDisabled">+</button>
      </div>
    </div>
    <div class="box card">
      <div class="num card-body">
        <span class="fs-2" :class="{ 'span-green': isYellow }">{{ yellowNum }}</span>
      </div>
      <div class="addel card-footer">
        <button class="btn btn-yellow m-1 fs-3" @click="addYellow()" :disabled="yellowDisabled">+</button>
      </div>
    </div>
    <div class="box card">
      <div class="num card-body">
        <span class="fs-2" :class="{ 'span-green': isWhite }">{{ whiteNum }}</span>
      </div>
      <div class="addel card-footer">
        <button class="btn btn-white m-1 fs-3" @click="addWhite()" :disabled="whiteDisabled">+</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "~bootstrap/scss/bootstrap";

.host {
  display: flex;
  align-items: center;
  justify-content: center;

  @media (orientation: landscape) {
    flex-direction: row;
  }

  @media (orientation: portrait) {
    flex-direction: column;
  }
}

.box {
  width: 180px;

  @media (orientation: landscape) {
    margin: 10px 2px;
  }

  @media (orientation: portrait) {
    margin: 2px 10px;
  }
}

.num {
  display: flex;
  justify-content: center;
  align-items: center;
}

.addel {
  display: flex;
}

.btn-blue {
  @include button-variant($blue, $gray-500);
  width: 100%;
}

.btn-red {
  @include button-variant($red, $gray-500);
  width: 100%;
}

.btn-yellow {
  @include button-variant($yellow, $gray-500);
  width: 100%;
}

.btn-white {
  @include button-variant($white, $gray-500);
  width: 100%;
}

.btn-black {
  @include button-variant($black, $gray-500);
}

.span-green {
  color: $green;
}
</style>
