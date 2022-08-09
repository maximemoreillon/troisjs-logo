<template>
  <Renderer ref="renderer" antialias :orbit-ctrl="{ enableDamping: false }" resize="window">
    <Camera :position="{ x: 5, y: 10, z: 5 }" />
    <Scene>
      <AmbientLight :intensity="0.2" />


      <PointLight :position="{x: 0, y: 10, z: 0}" />
      <GltfModel src="assets/logo.gltf" @load="onReady" ref="logo" />

      <Mesh :position="{ y: -1 }" :rotation="{x: - Math.PI/2}">
        <PlaneGeometry :width="100" :height="100" />
        <PhysicalMaterial color="#111111" />
      </Mesh>
    </Scene>
  </Renderer>
</template>
<script>

export default {
  data(){
    return {
      
    }
  },
  methods: {

    onReady(){
      const renderer = this.$refs.renderer;

      console.log('Ready')
      const logo = this.$refs.logo;

      renderer.onBeforeRender(() => {
        if (logo.o3d) logo.o3d.rotation.y -= 0.003
      })
    },
  }
}
</script>

<style>
body {
  margin: 0;
}
canvas {
  display: block;
}
</style>