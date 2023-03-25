<script setup lang="ts">
import { PerspectiveCamera, PointLight, Scene, WebGLRenderer } from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader'

interface Props {
  src: string
}

const { src } = defineProps<Props>()

onMounted(() => {
  const scene = new Scene()
  const camera = new PerspectiveCamera(75, 1, 0.1, 1000)

  const renderer = new WebGLRenderer({ alpha: true })
  renderer.setClearColor(0xFFFFFF, 1)
  renderer.setSize(500, 500)
  const cylinderContainer = document.getElementById('cylinder-container')!
  cylinderContainer.appendChild(renderer.domElement)

  const light = new PointLight(0x873919, 1, 100)
  light.position.set(0, 0, 30)
  scene.add(light)

  const loader = new GLTFLoader()
  loader.load(src, (gltf) => {
    scene.add(gltf.scene)
  }, undefined, (error) => {
    console.error(error)
  })

  camera.position.z = 30

  const controls = new OrbitControls(camera, renderer.domElement)

  function animate() {
    requestAnimationFrame(animate)
    controls.update()
    renderer.render(scene, camera)
  }
  animate()
})
</script>

<template>
  <div
    id="cylinder-container"
    border="~ 2"
    overflow="hidden"
    w-500px h-500px
  />
</template>
