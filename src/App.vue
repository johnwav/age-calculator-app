<script setup>
import Input from "@/components/InputComponent.vue"
import Result from "@/components/ResultComponent.vue"
import { ref, watch, reactive } from "vue"
const day = ref()
const month = ref()
const year = ref()
const date = ref('')
const presentDate = ref(new Date())
const output = reactive({
  years: '- -',
  months: '- -',
  days: '- -'
})

const submit = async () => {
  const yourBirthday = ref()
  const diffrence = ref()
  date.value = await `${year.value}, ${month.value}, ${day.value}`
  yourBirthday.value = await new Date(date.value)
  diffrence.value = await yourBirthday.value.getTime() - presentDate.value.getTime();
  diffrence.value && await formatMilliseconds(diffrence?.value)
  return Promise.resolve("Success")
}

const formatMilliseconds = (milliseconds) => {
  const second = 1000;
  const minute = second * 60;
  const hour = minute * 60;
  const day = hour * 24;
  const year = day * 365.25; // accounting for leap years

  const years = Math.floor(milliseconds / year);
  milliseconds = milliseconds % year;

  const months = Math.floor(milliseconds / (day * 30));
  milliseconds = milliseconds % (day * 30);

  const days = Math.floor(milliseconds / day);

  output.years = Math.abs(years)
  output.months = Math.abs(months)
  output.days = Math.abs(days)

}


</script>

<template>
  <div class="modal">
    <div class="container">
      <form @submit.prevent="submit">
        <Input @save-input="(input) => day = input" for="day">DAY</Input>
        <Input @save-input="(input) => month = input" for="month">MONTH</Input>
        <Input @keyup.enter="submit" @save-input="(input) => year = input" for="year">YEAR</Input>
      </form>
      <div class="divider">
      </div>
      <div class="results">
        <Result :value="output.years"> years</Result>
        <Result :value="output.months"> months</Result>
        <Result :value="output.days"> days</Result>
      </div>

    </div>

  </div>
</template>s

<style scoped>
.modal {
  background-color: var(--white);
  width: 842px;
  height: 652px;
  border-radius: 30px 30px 250px 30px;
}

.container {
  width: 100%;
  height: 100%;
  padding-inline: 52px;
}

form {
  display: flex;
  gap: 30px;
  margin-top: 50px;
}

.divider {
  border: 1px solid var(--off-white);
  margin-top: 44px;
}


.results {
  margin-top: 62px;
  line-height: 110px;
}
</style>