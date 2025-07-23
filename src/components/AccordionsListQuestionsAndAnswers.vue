<template>
    <div class="accordion" id="accordionStayOpen">
        <AccordionQuestionsAnswers v-for="(questionAndAnswer, index) in questionsAndAnswers" :key="index" 
            v-bind:title="questionAndAnswer.title"
            :description="questionAndAnswer.description"
            :descriptionCollasped="handleDescriptionCollasped"
            :accordionItemId="index"
        ></AccordionQuestionsAnswers>
    </div>
</template>
<script setup>
import AccordionQuestionsAnswers from './AccordionQuestionsAnswers.vue';
const questionsAndAnswers = [
    {
        title: `Q1. : What is my training pace, and why is it important?`,
        description: `A: Your training pace is the speed at which you run during training sessions. It is important because running at the right pace helps optimize your workouts, prevent injuries, and improve overall performance. Different types of runs (easy, tempo, long run) have specific pace ranges that target different aspects of fitness.`,
        descriptionCollasped: false,
    },
    {
        title: `Q2. : How do I determine my ideal training pace for different types of runs?`,
        description: `A: You can determine your ideal training pace by considering your recent race performance or using a training pace calculator. Easy runs should be comfortable and conversational, tempo runs at a challenging but sustainable pace, and speed workouts at a faster pace. Adjust these paces based on your current fitness level and training goals.`,
    },
    {
        title: `Q3. : Should I always run at my maximum training pace to improve quickly?`,
        description: `A: No, running at your maximum pace for every run is not recommended. Consistency is key in training, and incorporating a variety of paces, including easy and recovery runs, helps prevent burnout and reduce the risk of injuries. Training should include a mix of intensities to target different energy systems and build overall endurance.`,
    },
    {
        title: `Q4. : How often should I update my training pace?`,
        description: `A: It's a good practice to reevaluate your training paces every 4-6 weeks or after significant changes in fitness. As you become fitter, your paces may change, and updating them ensures that your training remains effective and aligned with your current abilities.`,
    },
    {
        title: `Q5. : Can I use my race pace as my training pace for all runs?`,
        description: `A: While your race pace is a useful reference, it's not suitable for all training runs. Easy runs should be slower, and tempo or interval runs may be faster. Tailor your training paces to the specific goals of each workout to maximize the benefits of each session and avoid unnecessary fatigue.`,
    },
]
const handleDescriptionCollasped = () => {
    if(questionCollasped.descriptionCollasped == undefined) return true
}
</script>