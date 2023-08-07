<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"></div>
      <div class="status">{{ questionsAnswered + 1 }} out of {{ questions.length }} questions answered</div>
    </div>
    <TransitionGroup name="fade">
      <div class="single-question" v-for="(question, qi) in questions" :key="question.q" v-show="questionsAnswered === qi">
        <div class="question">{{ question.q }}</div>
        <div class="answers" v-for="answer in question.answers" :key="answer.text">
          <div class="answer" @click.prevent="$emit('question-answered', answer.is_correct)">{{ answer.text }}</div>
        </div>
      </div>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  name: "Questions",
  props: ["questions", "questionsAnswered"],
  emits: ["question-answered"],
};
</script>
