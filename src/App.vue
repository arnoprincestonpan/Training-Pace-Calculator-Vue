<template>
  <header class="container">
    <div class="jumbotron m-3 p-3 text-center bg-secondary-subtle">
      <h1 class="fs-1 fw-bold">Training Pace Calculator</h1>
    </div>
  </header>
  <main class="container">
    <section class="d-flex flex-row justify-content-center align-self-stretch mb-3">
      <div v-for="preset in presetsObj" v-bind:key="preset">
        <button class="btn btn-primary text-capitalize m-2">{{ preset.name }}</button>
      </div>
    </section>
    <section class="border">
      <form class="p-3">
        <div class="mb-3 row d-flex flex-row justify-content-end">
          <label
            class="col-sm-2 col-form-label d-flex flex-row justify-content-center align-items-center text-uppercase">Units</label>
          <button type="button" class="btn btn-light col-sm-2 border">
            Metric <span class="badge text-bg-secondary">km</span>
          </button>
          <button type="button" class="btn btn-light col-sm-2 border">
            Imperial <span class="badge text-bg-secondary">mi</span>
          </button>
        </div>
        <div class="mb-3 row">
          <label class="col-sm-9 col-form-label">Recent Race Length (i.e. 26.2mi)</label>
          <input class="col-sm-2" type="number" v-model="formObj.length">
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
import { ref, reactive } from 'vue'

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
const presetsObj = [
  {
    name: "half marathon",
    distance: isMetric ? 21.1 : 13.1,
  },
  {
    name: 'marathon',
    distance: isMetric ? 42.2 : 26.2,
  },
  {
    name: '5k',
    distance: isMetric ? 5 : 3.1,
  },
  {
    name: '10k',
    distance: isMetric ? 10 : 6.2,
  },
  {
    name: '1 Mile',
    distance: isMetric ? 1.61 : 5,
  }
]
</script>
