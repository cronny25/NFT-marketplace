<template>
  <div>
    <img v-if="fileType === 'image'" :src="asset.file">
    <video v-if="fileType === 'video'" controls>
      <source :src="asset.file" :type="asset.type"/>
    </video>
    <audio v-if="fileType === 'audio'" controls>
      <source :src="asset.file" :type="asset.type"/>
    </audio>

    <div v-if="fileType === 'gltf-binary'">
      <model-viewer
          :src="asset.file"
          auto-rotate
          camera-controls
      ></model-viewer>
    </div>
  </div>
</template>

<script>
import {computed} from "vue"

let knownExt = ['application', 'model']

export default {
  name: "AssetPreview",

  props: {
    asset: Object
  },

  setup(props) {
    let fileType = computed(() => {
      let mime = props.asset.type.split('/')
      return knownExt.includes(mime[0])
          ? mime[1]
          : mime[0]
    })

    return {
      fileType
    }
  }
}
</script>