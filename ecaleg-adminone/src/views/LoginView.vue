<script setup>
import { reactive } from "vue";
import { ref } from "vue";
import { useRouter } from "vue-router";
import { mdiAccount, mdiAsterisk } from "@mdi/js";
import SectionFullScreen from "@/components/SectionFullScreen.vue";
import CardBox from "@/components/CardBox.vue";
import FormCheckRadio from "@/components/FormCheckRadio.vue";
import FormField from "@/components/FormField.vue";
import FormControl from "@/components/FormControl.vue";
import BaseButton from "@/components/BaseButton.vue";
import BaseButtons from "@/components/BaseButtons.vue";
import LayoutGuest from "@/layouts/LayoutGuest.vue";

import axios from 'axios'

const form = ref({
  email: '',
  password: '',
});

const submitLogin = async () => {
  await axios.post('/login', {
    email: form.value.email,
    password: form.value.password,
    remember: true,
  });
}
// const form = reactive({
//   login: "john.doe",
//   pass: "highly-secure-password-fYjUw-",
//   remember: true,
// });
const user = reactive({
  email: "john.doe",
  password: "highly-secure-password-fYjUw-",
  remember: true,
});

const router = useRouter();

const submit = () => {
  router.push("/dashboard");
};

</script>

<template>
  <LayoutGuest>
    <SectionFullScreen v-slot="{ cardClass }" bg="purplePink">
      <CardBox :class="cardClass" is-form @submit.prevent="submitLogin">
        <FormField label="Login" help="nama@domain.com">
          <FormControl
            v-model="form.email"
            :icon="mdiAccount"
            name="user"
            autocomplete="username"
            placeholder="email"
          />
        </FormField>

        <FormField label="Password" help="min. 8 huruf">
          <FormControl
            v-model="form.password"
            :icon="mdiAsterisk"
            type="password"
            name="password"
            autocomplete="current-password"
          />
        </FormField>

        <FormCheckRadio
          v-model="form.remember"
          name="remember"
          label="Remember"
          :input-value="true"
        />

        <template #footer>
          <BaseButtons>
            <BaseButton type="submit" color="info" label="Login" />
            <!-- <BaseButton to="/dashboard" color="info" outline label="Back" /> -->
          </BaseButtons>
        </template>
      </CardBox>
    </SectionFullScreen>
  </LayoutGuest>
</template>
