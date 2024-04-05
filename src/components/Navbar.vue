<script setup lang="ts">
import {
  Button,
  Progress,
  Divider,
  InputSearch,
  Tree,
  Checkbox,
  CheckboxGroup
} from 'ant-design-vue'
import { TreeDataItem } from 'ant-design-vue/es/tree/Tree'
import { ref, reactive, computed } from 'vue'

const props = defineProps<{
  imageList: { id: number; url: string }[]
}>()

const emit = defineEmits(['search','photoby'])
const searchValue = ref('')
const expandedKeys = ref<string[]>(['0-0-0', '0-0-1'])
const selectedKeys = ref<string[]>(['0-0-0', '0-0-1'])
const checkedKeys = ref<string[]>(['0-0-0', '0-0-1'])
const checkedList = ref('')
const treeData: TreeDataItem[] = [
  {
    title: 'Uploads',
    key: '0-0',
    children: [
      {
        title: 'Images',
        key: '0-0-0'
      },
      {
        title: 'Documents',
        key: '0-0-1'
      },
      {
        title: 'Videos',
        key: '0-0-2'
      }
    ]
  }
]

const totalPhysicalSize = computed(() => {
  let totalSize = 0

  for (const image of props.imageList) {
    try {
      const sizeInBytes = parseSizeString(image.physicalSize)
      totalSize += sizeInBytes
    } catch (error) {
      console.error(`Error calculating size for image ${image.id}: ${error.message}`)
    }
  }

  const total2GB = 2 * 1024 * 1024 * 1024

  const percentage = (totalSize / total2GB) * 100

  return percentage.toFixed(2)
})

function parseSizeString(sizeString: string): number {
  const regex = /^(\d+(\.\d+)?)\s*(kb|mb|gb)$/i
  const match = sizeString.match(regex)

  if (!match) {
    throw new Error('Invalid size string format')
  }

  const value = parseFloat(match[1])
  const unit = match[3].toLowerCase()

  switch (unit) {
    case 'kb':
      return value * 1024
    case 'mb':
      return value * 1024 * 1024
    case 'gb':
      return value * 1024 * 1024 * 1024
    default:
      throw new Error('Unsupported unit')
  }
}

const handleCheckboxChange = (checkedValue) => {
  if (checkedValue && checkedValue.length > 0) {
    const selected = checkedValue[0];
    emit('photoby', selected); 
    checkedList.value = selected;
  }
};

function onSearch() {
  emit('search', searchValue.value)
}
</script>

<template>
  <div class="navbar">
    <Button class="navbar_upload-btn" type="primary" size="large" style="margin: 20px;">Import Documents</Button>
    <div class="navbar_list">
      <div class="navbar_item">
        <h2 class="navbar_item-title">Storage</h2>
        <Progress :percent="totalPhysicalSize" />
        <p class="navbar_item-progess">{{ totalPhysicalSize }}% used of 2GB</p>
      </div>
      <Divider />
      <div class="navbar_item">
        <h2 class="navbar_item-title">Search</h2>
        <InputSearch
          v-model:value="searchValue"
          placeholder="e.g. image.png"
          style="width: 200px"
          @search="onSearch"
        />
      </div>
      <Divider />
      <div class="navbar_item">
        <h2 class="navbar_item-title">Folder</h2>
        <Tree
          :tree-data="treeData"
          v-model:expandedKeys="expandedKeys"
          v-model:selectedKeys="selectedKeys"
          v-model:checkedKeys="checkedKeys"
        >
          <template #title0010><span style="color: #1890ff">sss</span></template>
        </Tree>
      </div>
      <Divider />
      <div class="navbar_item">
        <h2 class="navbar_item-title">Member</h2>
        <CheckboxGroup
          v-model:value="checkedList"
          @change="handleCheckboxChange"
          style="width: 100%; display: flex; flex-direction: column"
        >
          <a-col>
            <Checkbox value="all">All</Checkbox>
          </a-col>
          <a-col>
            <Checkbox value="admin">Admin</Checkbox>
          </a-col>
        </CheckboxGroup>
      </div>
      <Divider />
    </div>
  </div>
</template>

<style scoped>
@media (min-width: 1024px) {
}
</style>
