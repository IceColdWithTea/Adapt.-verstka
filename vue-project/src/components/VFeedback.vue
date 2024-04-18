<script setup>

import {ref} from "vue";

const name = ref('');
const question = ref('');
const phone = ref('');
const email = ref('');
const  cool = ref(false)

async function onsubmit() {
  console.log(name.value,
      question.value,
      phone.value,
      email.value)
  const botToken = '7029884370:AAFHSU6kmwrGr-4vLA9gmTMHIcwxxsan6OU';
  const chatId = '-1002131235305';
  const text = 'Новое сообщение:%0A%0A ' +
      `Вопрос: ${question.value}%0A` +
      `Имя: ${name.value}%0A` +
      `Телефон: ${phone.value}%0A` +
      `Email: ${email.value}`;
  await fetch(`https://api.telegram.org/bot${botToken}/sendMessage?chat_id=${chatId}&text=${text}`)
      .then((response) => {
        if (response.status === 200) {
          cool.value = true;
        }
      })
      .catch((error) => {
        cool.value = false;
        console.log(error)
      })
  const  message = cool.value ? 'Отправлено' : 'Произошла ошибка, попробуйте еще раз';
  alert(message);
}
</script>



<template>
  <section class="feedback">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-xl-6">
          <div class="feedback__text">
            <h2>Остались вопросы?</h2>
            <p>Свяжитесь с нами!</p>
          </div>
        </div>
        <div class="col-lg-9 col-xl-6">
          <form class="form" method="post" @submit.prevent="onsubmit()">
            <label class="mb-3">
                <textarea id="textarea" placeholder="Введите ваш вопрос" title="Ваш вопрос"
                          v-model="question"
                          required
                ></textarea>

            </label>
            <div class="form__group">
              <label>
                <input type="text"
                       placeholder="Ваше имя"
                       title="Ваше имя"
                       v-model="name"
                       required>
              </label>
              <label>
                <input type="tel"
                       placeholder="+7(___)___-____"
                       pattern="[0-9]{11}"
                       maxlength="11"
                       title="Номер телефона"
                       v-model="phone"
                       required
                >
              </label>
              <label>
                <input type="email"
                       placeholder="Электронная почта"
                       title="Электронная почта"
                       v-model="email"
                       required
                >
              </label>
            </div>
            <button class="button-primary" type="submit">Отправить</button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>