<template>
  <main class="main prose">
    <h1>Prettier Format Generator</h1>
    <div class="flex min-w-[50%] min-h-full">
      <form class="card">
        <label class="label cursor-pointer">
          <span class="label-text">Semicolons</span>
          <input
            type="checkbox"
            v-model="options.semi"
            :value="true"
            checked
            class="checkbox checkbox-secondary"
          />
        </label>
      </form>
      <textarea
        class="mockup-code border-none outline-none resize min-w-full min-h-full p-4"
        id="code"
        v-model="code"
        @focusout="code = formatCode(code)"
      ></textarea>
    </div>
    <button class="btn btn-primary">Generate config</button>
  </main>
</template>

<script setup lang="ts">
import prettier from 'prettier';
import type { Options } from 'prettier';
import { ref, type Ref } from 'vue';
import parserBabel from 'prettier/parser-babel';

const options: Ref<Options> = ref({
  semi: true,
  singleQuote: true,
  plugins: [parserBabel],
  parser: 'babel'
});

const code = ref('');

const formatCode = (code: string) => {
  return prettier.format(code, options.value);
};
</script>

<style scoped>
.main {
  min-height: 100vh;
  min-width: 100vw;
  display: grid;
  place-items: center;
}
</style>
