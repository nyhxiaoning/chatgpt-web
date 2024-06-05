<script setup lang='ts'>
import { defineAsyncComponent, ref } from 'vue'
import { HoverButton, SvgIcon, UserAvatar } from '@/components/common'

const Setting = defineAsyncComponent(() => import('@/components/common/Setting/index.vue'))

const show = ref(false)
const selectedModel = ref('chatgpt');
  const models = ref([
    { value: 'chatgpt',label:'chatGPT'},
    { value: 'wenxin_yiyan', label: '文心一言' },
    { value: 'tongyi_qianwen', label: '通义千问' },
    { value: 'xunfei_xinghuo', label: '讯飞星火' },
    { value: 'kimi_model', label: 'kimi大模型' },
  ]);

  const handleChange = (value) => {
    console.log('选择的模型是:', value);
  };
</script>

<template>
    <!-- 这是侧边栏底部：设置功能区 -->

  <footer class="flex items-center justify-between min-w-0 p-4 overflow-hidden border-t dark:border-neutral-800">
   
    <div class="flex-1 flex-shrink-0 overflow-hidden">
      <UserAvatar />
    </div>

    <HoverButton @click="show = true">
      <span class="text-xl text-[#4f555e] dark:text-white">
        <SvgIcon icon="ri:settings-4-line" />
      </span>
    </HoverButton>

    <Setting v-if="show" v-model:visible="show" />


  </footer>
  <div>

    <br/>
     <el-select v-model="selectedModel" placeholder="请选择一个模型" @change="handleChange">
      <el-option
        v-for="item in models"
        :key="item.value"
        :label="item.label"
        :value="item.value">
      </el-option>
    </el-select>

    <br/>
    <br/>
    <div>
      当前模型是：{{ selectedModel }}
    </div>
  </div>

</template>
