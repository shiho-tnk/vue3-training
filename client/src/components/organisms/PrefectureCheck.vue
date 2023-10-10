<script setup lang="ts">
import { computed } from "vue"
import { PrefectureDisplay } from "@/types/prefecture"

const props = defineProps<{
  prefecture: PrefectureDisplay
}>()

// 親コンポーネントのcheckイベントを呼ぶ
// const emits = defineEmits<{
//   (eventName: "check", arg: PrefectureDisplay): void
// }>()
const emits = defineEmits(["check"])

// 上記処理を呼び出す
const checkBox = computed({
  get: () => props.prefecture.isCheck,
  set: (isCheck: boolean) => emits("check", { ...props.prefecture, isCheck })
})
</script>

<template>
  <div class="prefecture-area">
    <input v-model="checkBox" type="checkbox" />
    <span>{{ prefecture.prefName }}</span>
  </div>
</template>

<style scoped>
.prefecture-area {
  display: flex;
}
</style>
