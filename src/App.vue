<template>
  <Renderer ref="renderer" antialias :orbit-ctrl="{ enableDamping: false }" resize="window">
    <Camera :position="{ x: 5, y: 10, z: 5 }" />
    <Scene>
      <PointLight :position="{ y: 50, z: 50 }" />
      <GltfModel src=" /assets/logo.gltf" @load="onReady" ref="logo"
        :rotation="{ x: Math.PI / 9, y: Math.PI / 4, z: 0.0 * Math.PI}" />
    </Scene>
  </Renderer>
</template>

<script>

export default {

  methods: {
    onReady(){
      const renderer = this.$refs.renderer;

      console.log('Ready')
      const logo = this.$refs.logo;

      renderer.onBeforeRender(() => {
        if (logo.o3d) logo.o3d.rotation.y -= 0.003

      });
      
    },
    onProgress() {

      console.log('Progress')
    }
  }
};
</script>

<style>
body {
  margin: 0;
}
canvas {
  display: block;
}
</style>