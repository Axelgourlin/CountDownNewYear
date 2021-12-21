<script setup lang="ts">
import Timer from "@/components/Timer.vue";
import { ref } from "@vue/reactivity";
import { onMounted, onUnmounted } from "@vue/runtime-core";

const years = new Date().getFullYear() + 1;
const newYears = new Date(years, 0, 1).toISOString();
const RemainingDays = ref("");
const RemainingHours = ref("");
const RemainingMinutes = ref("");
const RemainingSeconds = ref("");

function countDown() {
  const newYearsDate: Date = new Date(newYears);
  const currentDate: Date = new Date();

  const totalSeconds = (newYearsDate.getTime() - currentDate.getTime()) / 1000;

  const days = Math.floor(totalSeconds / 3600 / 24);
  const hours = Math.floor(totalSeconds / 3600) % 24;
  const mins = Math.floor(totalSeconds / 60) % 60;
  const seconds = Math.floor(totalSeconds) % 60;

  RemainingDays.value = setTime(days);
  RemainingHours.value = setTime(hours);
  RemainingMinutes.value = setTime(mins);
  RemainingSeconds.value = setTime(seconds);
}

function setTime(value: number) {
  return value >= 10 ? value.toString() : `0${value}`;
}

let timeInterval: ReturnType<typeof setInterval>;
onMounted(() => {
  timeInterval = setInterval(countDown, 1000);
});

onUnmounted(() => {
  clearInterval(timeInterval);
});

const mainColor = "hsl(51, 100%, 45%)";
const secondaryColor = "hsl(276, 98%, 40%)";
</script>

<template>
  <div class="container">
    <div class="filter"></div>
    <div class="title">New Year Count Down</div>
    <div class="timerContainer">
      <Timer :count="RemainingDays" label="Days" :color="mainColor" />
      <Timer :count="RemainingHours" label="Hours" :color="secondaryColor" />
      <Timer :count="RemainingMinutes" label="Minutes" :color="mainColor" />
      <Timer :count="RemainingSeconds" label="Seconds" :color="secondaryColor" />
    </div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Merriweather:ital@1&family=Roboto+Slab&display=swap");

body {
  margin: 0;
  font-family: "Merriweather", serif;
  font-family: "Roboto Slab", serif;
  text-align: center;
  text-shadow: 1px 10px 10px rgba(0, 0, 0, 0.5);
}

.container {
  height: 100vh;
  background: no-repeat url("@/assets/bg-timer.jpg");
  color: hsl(51, 100%, 45%);
  position: relative;
  z-index: -2;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.filter {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: -1;
  background-color: rgba(0, 0, 0, 0.4);
}

.title {
  font-size: 5rem;
  font-weight: bold;
  z-index: 1;
  padding: 90px 0 200px 0;
}

.timerContainer {
  width: 80vw;
  display: flex;
  justify-content: space-around;
}
</style>
