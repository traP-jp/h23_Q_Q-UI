<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { Icon } from '@iconify/vue'
import { Question } from '/@/apis/parser/question'
import { getFullDayWithTimeString } from '/@/libs/date'

interface Props {
  questions: Question[]
}

defineProps<Props>()
</script>

<template>
  <div>
    <div v-for="question in questions" :key="question.id" class="question">
      <router-link :to="`/${question.id}`"
        ><p class="content">{{ question.content }}</p></router-link
      >
      <div class="subcontent">
        <p class="createdAt">
          {{ getFullDayWithTimeString(new Date(question.createdAt)) }}
        </p>
        <div class="response-num">
          <icon icon="ic:outline-mode-comment" class="icon" />
          <p>{{ question.responseNum }}</p>
        </div>
        <div class="tagsarea">
          <div v-for="tags1 in question.tags" :key="tags1">
            <router-link to="#"
              ><div class="tags">#{{ tags1 }}</div></router-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.question {
  border-top: solid 1px #d9d9d9;
}

.subcontent {
  font-size: 0.875rem;
  display: flex;
  gap: 6px;
  align-items: center;
  width: 100%;
}

.icon {
  width: 16px;
  height: 16px;
}

.content {
  color: #000000;
  padding-left: 20px;
  padding-top: 5px;
  padding-bottom: 5px;
  white-space: nowrap;
  overflow: hidden;
}

.createdAt {
  color: #919191;
  white-space: nowrap;
  padding-top: 3px;
  padding-bottom: 4px;
  padding-left: 20px;
}

.response-num {
  display: flex;
  align-items: center;
  gap: 2px;
  color: #919191;
}

.tagsarea {
  white-space: nowrap;
  display: flex;
  overflow: hidden;
}
.tags {
  font-size: 1rem;
  color: #919191;
  padding-bottom: 5px;
  margin-bottom: 5px;
  margin-left: 10px;
  padding: 0px 5px 0px 5px;
  border: 1px solid #919191;
  border-radius: 8px;
  overflow: hidden;
}
a {
  text-decoration: none;
}
</style>
