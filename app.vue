<template></template>

<script setup lang="ts">
import {
  WebGLRenderer,
  PerspectiveCamera,
  Scene,
  BoxGeometry,
  Mesh,
  MeshBasicMaterial,
  Color,
} from "three";

let scene: Scene, camera: PerspectiveCamera, renderer: WebGLRenderer;
let cube: Mesh;

onMounted(() => {
  init();
});

function init() {
  scene = new Scene();
  scene.background = new Color(0xcce0ff);

  camera = new PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  camera.position.z = 5;

  renderer = new WebGLRenderer();
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  const geometry = new BoxGeometry(1, 1, 1);
  const material = new MeshBasicMaterial({ color: 0x000000 });
  cube = new Mesh(geometry, material);
  scene.add(cube);

  animate();
}

function animate() {
  requestAnimationFrame(animate);

  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;

  renderer.render(scene, camera);
}
</script>

<style>
body {
  margin: 0;
}
</style>