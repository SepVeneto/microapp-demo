<template>
  <div ref="imgRef"></div>
</template>

<script setup lang="ts">
import { onMounted, ref, shallowRef, watch } from 'vue'

const imgRef = ref()

const props = defineProps({
  src: {
    type: String,
    required: true,
  },
})

onMounted(() => {
  loadImage()
})
watch(() => props.src, () => {
  loadImage()
})
const _img = shallowRef()
function loadImage() {
  const img = new Image()

  img.onload = () => {
    if (_img.value) {
      _img.value.remove()
    }
    _img.value = img
    imgRef.value.appendChild(img)
  }
  img.src = props.src
}
</script>
