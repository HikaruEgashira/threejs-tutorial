<template>
  <canvas id="canvas" width="600" height="400"></canvas>
</template>
<script lang="ts">
import * as THREE from "three";
import { Component, Vue } from "nuxt-property-decorator";

@Component
export default class RotateBox extends Vue {
  private scene = new THREE.Scene();
  private renderer = new THREE.WebGLRenderer();
  private camera = new THREE.PerspectiveCamera(75, 600 / 400, 0.1, 1000);
  private light = new THREE.DirectionalLight(0xffffff);
  private geometry = new THREE.BoxGeometry(1, 1, 1);
  private material = new THREE.MeshNormalMaterial();
  private cube = new THREE.Mesh(this.geometry, this.material);
  private animate(): void {
    requestAnimationFrame(this.animate);
    this.cube.rotation.x += 0.02;
    this.cube.rotation.y += 0.02;
    this.renderer.render(this.scene, this.camera);
  }
  mounted(): void {
    const canvas = document.getElementById("canvas");
    if (canvas) {
      this.renderer = new THREE.WebGLRenderer({
        canvas,
        antialias: true
      });
    }

    this.camera.position.set(0, 0, 2);
    this.light.position.set(0, 0, 10);
    this.scene.add(this.cube);
    this.scene.add(this.light);

    this.animate();
  }
}
</script>
