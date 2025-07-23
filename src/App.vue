<template>
  <header class="container">
    <div class="jumbotron m-3 p-3 text-center bg-secondary-subtle">
      <h1 class="fs-1 fw-bold">Training Pace Calculator</h1>
    </div>
  </header>
  <main class="container">
    <section class="d-flex flex-row justify-content-center align-self-stretch mb-3">
      <div v-for="preset in presetsObj" v-bind:key="preset">
        <button v-on:click="formObj.length = isMetric ? preset.distanceMetric : preset.distanceImperial"
          class="btn btn-primary text-capitalize m-2">{{ preset.name }}</button>
      </div>
    </section>
    <section class="border">
      <form class="p-3">
        <div class="mb-3 row d-flex flex-row justify-content-end">
          <label
            class="col-sm-2 col-form-label d-flex flex-row justify-content-center align-items-center text-uppercase">Units</label>
          <button v-on:click="handleMeasurementSystemToggle" v-if="isMetric" type="button"
            class="btn btn-light col-sm-2 border">Metric&nbsp;<span class="badge text-bg-secondary">km</span>&nbsp;
            <IconToggle></IconToggle>
          </button>
          <button v-on:click="handleMeasurementSystemToggle" v-else type="button"
            class="btn btn-light col-sm-2 border">Imperial&nbsp;<span class="badge text-bg-secondary">mi</span>&nbsp;
            <IconToggle></IconToggle>
          </button>
        </div>
        <div class="mb-3 row">
          <label class="col-sm-9 col-form-label">Recent Race Length (i.e. 26.2mi)</label>
          <input class="col-sm-2" type="number" step="0.01" v-model="formObj.length" v-on:change="formObj.preset = false">
          <label class="col-sm-1 col-form-label d-flex flex-row justify-content-center align-items-center">{{ isMetric ?
            "km" : "mi" }}</label>
        </div>
        <div class="mb-3 row d-flex flex-row justify-content-center align-items-center">
          <label class="col-sm-3 col-form-label">My time in (Hours : Minutes : Seconds)</label>
          <input class="col-sm-2" type="number" />
          <label class="col-sm-1 d-flex flex-row justify-content-center align-items-center">HH</label>
          <input class="col-sm-2" type="number" />
          <label class="col-sm-1 d-flex flex-row justify-content-center align-items-center">MM</label>
          <input class="col-sm-2" type="number" />
          <label class="col-sm-1 d-flex flex-row justify-content-center align-items-center">SS</label>
        </div>
      </form>
    </section>
  </main>
</template>
<script setup>
import { ref, reactive, computed } from 'vue'
import IconToggle from './components/icons/IconToggle.vue';

const isMetric = ref(true);

const initialFormObj = {
  length: "",
  metric: isMetric,
  timeInHours: "",
  timeInMinutes: "",
  timeInSeconds: "",
  easyRun: "",
  tempoRun: "",
}

const formObj = reactive({
  ...initialFormObj
})
const presetsObj = computed(() => [
  {
    name: "half marathon",
    distanceMetric: 21.10,
    distanceImperial: 13.10,
  },
  {
    name: 'marathon',
    distanceMetric: 42.20,
    distanceImperial: 26.20,
  },
  {
    name: '5k',
    distanceMetric: 5.00,
    distanceImperial: 3.10,
  },
  {
    name: '10k',
    distanceMetric: 10.00,
    distanceImperial: 6.20,
  },
  {
    name: '1 Mile',
    distanceMetric: 1.61,
    distanceImperial: 1.00,
  }
])

const handleMeasurementSystemToggle = () => {
  if(formObj.length){
    if(isMetric.value){
      formObj.length = formObj.length / 1.609
    } else {
      formObj.length = formObj.length * 1.609
    }
  }
  isMetric.value = !isMetric.value;
}

</script>
