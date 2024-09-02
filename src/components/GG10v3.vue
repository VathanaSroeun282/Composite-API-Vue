<template>
  <div>
    <p>Hello kon ah papa</p>
    <p class="font-bold text-xl">{{ myRef[0].ggg.g2 }}</p>
    <button :onclick="gggg">GGGG</button>
    <p>{{ myCount }}</p>
  </div>
</template>

<script setup>
import { reactive, watch } from "vue";

const myRef = reactive([
  {
    gg: "3",
    ggg: {
      g1: "12",
      g2: 12,
    },
  },
]);

function gggg() {
  myRef[0].ggg.g2 += 4;
}
// Deep watcher for changes in `myRef`
let myCount = 1;
watch(
    () => myRef[0], // Directly watch the `g2` property
    (newMyRef) => {
        myCount++;
        console.log("This is the new value of myRef[0].ggg.g2 =", newMyRef.ggg.g2);
    },
    { deep: true }
);
setInterval(() => {
  myRef[0].ggg.g2 += 4;
}, 1000);
</script>
