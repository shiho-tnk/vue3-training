<script lang="ts" setup>
import { onMounted, ref } from "vue"
import axiosInstance from "@/utils/axiosSettings"
import { PrefectureDisplay } from "@/types/prefecture"

// const prefecture1 = ref("千葉県")

// TODO: prefectureで千葉県を表示してみましょう
const prefecture = ref<PrefectureDisplay>({
  prefName: "千葉県",
  prefNo: 1,
  isCheck: false
})
console.log(prefecture.value.isCheck)

function click(bool: boolean) {
  prefecture.value.isCheck = bool
}

onMounted(() => {
  // TODO: 全県取得のAPIへリクエストを送ってみましょう!
  const response = axiosInstance.get("")
})
</script>
<template>
  <div class="prefecture-container">
    <h3>都道府県</h3>
    <div>
      <input type="checkbox" @click="click(!prefecture.isCheck)" />
      <label>千葉県</label>
    </div>
    <div v-if="prefecture.isCheck">true</div>
    <div class="prefecture-flex">
      <!-- TODO: 県を表示してみましょう -->
    </div>
  </div>
</template>
<style scoped>
.prefecture-container {
  max-width: 900px;
  width: 100%;
}

.prefecture-flex {
  display: grid;
  grid-template-columns: 33% 33% 33%;
}
</style>
