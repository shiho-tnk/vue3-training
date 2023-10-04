<script lang="ts" setup>
import { onMounted, ref, computed } from "vue"
import PrefectureCheck from "./PrefectureCheck.vue"
import axiosInstance from "@/utils/axiosSettings"
import { PrefectureDisplay } from "@/types/prefecture"
import { PrefectureResponse } from "@/types/api"

// TODO: prefectureで千葉県を表示してみましょう
// const prefecture = ref<PrefectureDisplay>({
//   prefName: "千葉県",
//   prefNo: 1,
//   isCheck: false
// })

const prefectureList = ref<PrefectureDisplay[]>([
  {
    prefName: "千葉県",
    prefCode: 1,
    isCheck: false
  }
])

// Clickイベント
// function click(bool: boolean) {
//   prefectureList.value[0].isCheck = bool
// }

// isCheck の結果が true を返す要素だけを新しい配列に
// const unDoneprefectureList = computed(() => {
//   return prefectureList.value.filter((item) => item.isCheck)
// })

onMounted(async () => {
  // TODO: 全県取得のAPIへリクエストを送ってみましょう!
  const response = await axiosInstance.get<PrefectureResponse>(
    "https://opendata.resas-portal.go.jp/api/v1/prefectures"
  )
  prefectureList.value = response.data.result.map((pref) => {
    return {
      ...pref, // ...オブジェクトの型(PrefectureResponse型)にオブジェクトを足すことができる
      isCheck: false
    }
  })
  // prefectureList.value = response.data.result
})
function check(value: PrefectureDisplay) {
  const index = prefectureList.value.findIndex(
    (x) => x.prefCode === value.prefCode
  )
  prefectureList.value[index] = value
}
</script>

<template>
  <div class="prefecture-container">
    <h3>都道府県</h3>
    <div class="prefecture-flex">
      <!-- TODO: 県を表示してみましょう -->
      <!-- <div v-for="prefecture in prefectureList" :key="prefecture.prefCode">
        <input v-model="prefecture.isCheck" type="checkbox" />
        <label>{{ prefecture.prefName }}</label>
      </div>
    </div> -->
      <!-- <div
        v-for="unDoneprefecture in unDoneprefectureList"
        :key="unDoneprefecture.prefCode"
      >
        {{ unDoneprefecture.prefName }}
      </div> -->
      <div v-for="prefecture in prefectureList" :key="prefecture.prefCode">
        <PrefectureCheck :prefecture="prefecture" @check="check" />
      </div>
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
