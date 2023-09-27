<script lang="ts" setup>
import { onMounted, ref, computed } from "vue"
import axiosInstance from "@/utils/axiosSettings"
import {
  Prefecture,
  PrefectureDisplay,
  PrefectureList
} from "@/types/prefecture"

// const prefecture1 = ref("千葉県")

// TODO: prefectureで千葉県を表示してみましょう
// const prefecture = ref<PrefectureDisplay>({
//   prefName: "千葉県",
//   prefNo: 1,
//   isCheck: false
// })

const prefectureList = ref<PrefectureList[]>([
  {
    prefName: "千葉県",
    prefNo: 1,
    isCheck: false,
    done: false
  },
  {
    prefName: "東京都",
    prefNo: 2,
    isCheck: false,
    done: false
  },
  {
    prefName: "神奈川県",
    prefNo: 3,
    isCheck: false,
    done: false
  },
  {
    prefName: "埼玉県",
    prefNo: 4,
    isCheck: false,
    done: false
  }
])

// isCheck の true/false
function click(bool: boolean) {
  prefectureList.value[0].isCheck = bool
}

// isCheck の結果が true を返す要素だけを新しい配列に
const unDoneprefectureList = computed(() => {
  return prefectureList.value.filter((item) => item.isCheck)
})

onMounted(async () => {
  // TODO: 全県取得のAPIへリクエストを送ってみましょう!
  const response = await axiosInstance.get<Prefecture[]>(
    "https://opendata.resas-portal.go.jp/api/v1/prefectures"
  )
  console.log(response.data)
})
</script>

<template>
  <div class="prefecture-container">
    <h3>都道府県</h3>
    <div class="prefecture-flex">
      <!-- TODO: 県を表示してみましょう -->
      <!-- <div>
        <input type="checkbox" @click="click(!prefecture.isCheck)" />
        <label>千葉県</label>
      </div> -->
      <div v-for="prefecture in prefectureList" :key="prefecture.prefNo">
        <input v-model="prefecture.isCheck" type="checkbox" />
        <label>{{ prefecture.prefName }}</label>
      </div>
      <div
        v-for="unDoneprefecture in unDoneprefectureList"
        :key="unDoneprefecture.prefNo"
      >
        {{ unDoneprefecture.prefName }}
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
