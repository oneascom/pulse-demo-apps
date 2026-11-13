<script setup lang="ts">
import { reactive, ref } from "vue"

import "@pulse/web/button"
import "@pulse/web/divider"
import "@pulse/web/form-field"
import "@pulse/web/icon-button"

const assetPath = "/assets"

const passwordVisible = ref(false)
const username = ref("")
const password = ref("")

const fieldErrors = reactive({
  username: false,
  password: false,
})

const handleSubmit = () => {
  fieldErrors.username = username.value.trim().length === 0
  fieldErrors.password = password.value.length === 0

  if (fieldErrors.username || fieldErrors.password) {
    return
  }

  // An authentication rejection can set both field errors here.
}

const handleUsernameInput = (event: Event) => {
  username.value = (event.currentTarget as HTMLInputElement).value
  fieldErrors.username = false
}

const handlePasswordInput = (event: Event) => {
  password.value = (event.currentTarget as HTMLInputElement).value
  fieldErrors.password = false
}
</script>

<template>
  <main class="login-page">
    <section class="login-content" aria-labelledby="login-title">
      <img
        class="brand-logo"
        :src="`${assetPath}/82a7d.svg`"
        alt="Ascom"
        width="142"
        height="29"
      />

      <form
        class="login-form"
        novalidate
        @submit.prevent="handleSubmit"
      >
        <p id="login-title" class="login-title">
          Sign in to your account
        </p>

        <m3e-button
          class="login-button login-button--provider"
          variant="tonal"
          size="medium"
          shape="rounded"
          type="button"
        >
          Sign in using [service provider]
        </m3e-button>

        <div class="login-divider" aria-hidden="true">
          <m3e-divider></m3e-divider>
          <span>or</span>
          <m3e-divider></m3e-divider>
        </div>

        <div class="login-fields">
          <m3e-form-field
            :class="[
              'login-field',
              { 'login-field--error': fieldErrors.username },
            ]"
            variant="outlined"
            float-label="auto"
            hide-subscript="auto"
            :error="fieldErrors.username"
          >
            <img
              class="field-icon"
              slot="prefix"
              :src="`${assetPath}/646d5.svg`"
              alt=""
              width="24"
              height="24"
            />

            <span slot="label">Username</span>

            <input
              id="username"
              name="username"
              type="text"
              autocomplete="username"
              aria-label="Username"
              :aria-invalid="fieldErrors.username"
              :value="username"
              @input="handleUsernameInput"
            />

            <span slot="error">
              Username is required
              </span>
          </m3e-form-field>

          <m3e-form-field
            :class="[
              'login-field',
              { 'login-field--error': fieldErrors.password },
            ]"
            variant="outlined"
            float-label="auto"
            hide-subscript="auto"
            :error="fieldErrors.username"
          >
            <img
              class="field-icon"
              slot="prefix"
              :src="`${assetPath}/4d49c.svg`"
              alt=""
              width="24"
              height="24"
            />

            <span slot="label">Password</span>

            <input
              id="password"
              name="password"
              :type="passwordVisible ? 'text' : 'password'"
              autocomplete="current-password"
              aria-label="Password"
              :aria-invalid="fieldErrors.password"
              :value="password"
              @input="handlePasswordInput"
            />
            <span slot="error">Password is required"</span>
            

            <m3e-icon-button
              class="field-action"
              slot="suffix"
              variant="standard"
              size="small"
              shape="rounded"
              width="default"
              type="button"
              :aria-label="
                passwordVisible ? 'Hide password' : 'Show password'
              "
              @click="passwordVisible = !passwordVisible"
            >
              <img
                :src="`${assetPath}/c5151.svg`"
                alt=""
                width="24"
                height="24"
              />
            </m3e-icon-button>
          </m3e-form-field>
        </div>

        <div class="login-actions">
          <m3e-button
            class="login-button login-button--submit"
            variant="filled"
            size="medium"
            shape="rounded"
            type="submit"
          >
            Sign in
          </m3e-button>

          <m3e-button
            class="login-button--help"
            variant="text"
            size="extra-small"
            shape="rounded"
            href="#"
          >
            Trouble signing in?
          </m3e-button>
        </div>
      </form>

      <nav class="utility-actions" aria-label="Support links">
        <m3e-icon-button
          variant="standard"
          size="medium"
          shape="rounded"
          width="default"
          aria-label="Information"
        >
          <img
            :src="`${assetPath}/1e398.svg`"
            alt=""
            width="24"
            height="24"
          />
        </m3e-icon-button>

        <m3e-icon-button
          variant="standard"
          size="medium"
          shape="rounded"
          width="default"
          aria-label="Help"
        >
          <img
            :src="`${assetPath}/c7f5f.svg`"
            alt=""
            width="24"
            height="24"
          />
        </m3e-icon-button>
      </nav>
    </section>

    <aside class="login-illustration" aria-hidden="true">
      <img
        class="illustration-image"
        :src="`${assetPath}/a56db.png`"
        alt=""
      />
    </aside>
  </main>
</template>