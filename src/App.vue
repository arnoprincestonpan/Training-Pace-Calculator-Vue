<template>
  <header class="container">
    <div class="jumbotron mt-2 p-3 text-center bg-secondary-subtle rounded border">
      <h1 class="fs-1 fw-bold">Training Pace Calculator</h1>
    </div>
  </header>
  <main class="container">
    <section class="d-flex flex-row justify-content-center align-self-stretch m-3">
      <div v-for="preset in presetsObj" v-bind:key="preset">
        <button v-on:click="formObj.length = isMetric ? preset.distanceMetric : preset.distanceImperial"
          class="btn btn-primary text-capitalize m-2">{{ preset.name }}</button>
      </div>
    </section>
    <section class="border">
      <form class="p-3" v-on:click.prevent="">
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
          <input class="col-sm-2" type="number" step="0.01" v-model.number="formObj.length">
          <label class="col-sm-1 col-form-label d-flex flex-row justify-content-center align-items-center">{{ isMetric ?
            "km" : "mi" }}</label>
        </div>
        <div class="mb-3 row d-flex flex-row justify-content-center align-items-center">
          <label class="col-sm-3 col-form-label">My time in (Hours : Minutes : Seconds)</label>
          <input class="col-sm-2" type="number" step="0.01" v-model.number="formObj.timeInHours" />
          <label class="col-sm-1 d-flex flex-row justify-content-center align-items-center">HH</label>
          <input class="col-sm-2" type="number" step="0.01" v-model.number="formObj.timeInMinutes" />
          <label class="col-sm-1 d-flex flex-row justify-content-center align-items-center">MM</label>
          <input class="col-sm-2" type="number" step="0.01" v-model.number="formObj.timeInSeconds" />
          <label class="col-sm-1 d-flex flex-row justify-content-center align-items-center">SS</label>
        </div>
        <div class="mb-3 row d-flex flex-row justify-content-end">
          <label
            class="col-sm-8 col-form-label d-flex flex-row justify-content-end align-items-center text-capitalize">Display
            Training Pace in: </label>
          <div class="col-sm-4 d-flex flex-row justify-content-end">
            <button @:click="isMetricPace = !isMetricPace" class="btn btn-light col-sm border" type="button">
              {{ isMetricPace ? "min/km" : "min/mi" }}&nbsp;
              <span class="badge text-bg-secondary">
                {{ isMetricPace ? "metric" : "imperial" }}
              </span>
              <IconToggle></IconToggle>
            </button>
            <button @click="handleCalculation" class="col-sm btn btn-success">Calculate</button>
          </div>
        </div>
      </form>
    </section>
    <section>
      <div class="row mt-1">
        <div class="col-md-4" v-for="(placeHolderPace, index) in placeHolderPaces" :key="index">
          <CardPaceResult class="col mt-1 mb-1" :title="placeHolderPace.name" :item="placeHolderPace.pace"></CardPaceResult>
        </div>
      </div>
    </section>
    <section>
      <h2 class="text-center bg-light border p-1 mt-1 mb-1 rounded">Training Pace Tips</h2>
      <AccordionsListQuestionsAndAnswers></AccordionsListQuestionsAndAnswers>
    </section>
  </main>
</template>
<script setup>
import { ref, reactive, computed } from 'vue'
import IconToggle from './components/icons/IconToggle.vue';
import AccordionsListQuestionsAndAnswers from './components/AccordionsListQuestionsAndAnswers.vue';
import CardPaceResult from './components/CardPaceResult.vue';

const isMetric = ref(true);
const isMetricPace = ref(true);

const placeHolderPaces = [
  {
    name: "Easy Pace",
    pace: "69.69 min/hr"
  },
  {
    name: "Easy Pace",
    pace: "69.69 min/hr"
  },
  {
    name: "Easy Pace",
    pace: "69.69 min/hr"
  },
  {
    name: "Easy Pace",
    pace: "69.69 min/hr"
  },
  {
    name: "Easy Pace",
    pace: "69.69 min/hr"
  },
  {
    name: "Easy Pace",
    pace: "69.69 min/hr"
  },
]

const initialFormObj = {
  length: 0,
  metric: isMetric,
  metricPace: isMetricPace,
  timeInHours: 0,
  timeInMinutes: 0,
  timeInSeconds: 0,
  easyRun: "",
  tempoRun: "",
  vo2Max: "",
  speedForm: "",
  longRun: "",
  yasso800s: "",
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
  if (formObj.length) {
    if (isMetric.value) {
      formObj.length = formObj.length / 1.609
    } else {
      formObj.length = formObj.length * 1.609
    }
  }
  isMetric.value = !isMetric.value;
}

const handleCalculation = () => {
  const runDurationInSeconds = formObj.timeInHours * 3600 + formObj.timeInMinutes * 60 + formObj.timeInSeconds
  formObj.easyRun = runDurationInSeconds / formObj.length
  formObj.tempoRun = (runDurationInSeconds - 20) / formObj.length
  formObj.vo2Max = (runDurationInSeconds - 75) / formObj.length
  formObj.speedForm = (runDurationInSeconds - 105) / formObj.length
  formObj.longRun = (runDurationInSeconds + 15) / formObj.length

  console.log('results: ', formObj)
}

</script>
