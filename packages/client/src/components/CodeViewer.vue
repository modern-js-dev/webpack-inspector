<script setup lang="ts">
import { guessMode } from '../logic/utils';
import { monaco } from '../logic/customMonaco';
import { isDark } from '../logic/dark';
const props = defineProps<{ code: string }>();
const containerEl = ref<HTMLElement | null>(null);
let editor: monaco.editor.IStandaloneCodeEditor | null = null;
onMounted(() => {
  if (!containerEl.value) {
    return;
  }
  watchEffect(() => {
    editor?.dispose();
    const model = monaco.editor.createModel(props.code, guessMode(props.code));
    console.log(isDark.value);

    editor = monaco.editor.create(containerEl.value!, {
      model,
      fontSize: 15,
      fontFamily: 'Consolas',
      theme: isDark.value ? 'vs-dark' : 'vs-light',
    });
  });
});
</script>

<template>
  <div class="w-300 h-300">
    <div ref="containerEl" class="w-300 h-300"></div>
  </div>
</template>
