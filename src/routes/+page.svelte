<script lang="ts">
    /*import { browser } from "$app/environment";
    import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';
    import * as THREE from 'three';

    if (browser) {
        let camera : THREE.PerspectiveCamera;
        let scene : THREE.Scene;
        let renderer : THREE.WebGLRenderer;
        let loader : GLTFLoader;
        let smartphone : THREE.Group;
        let directionalLight : THREE.DirectionalLight;
        let ambientLight : THREE.AmbientLight;

        const init = () => {
            scene = new THREE.Scene();
            scene.background = null;
            camera = new THREE.PerspectiveCamera(75, 1, 0.1, 1000);
            camera.position.setZ(30);


            renderer = new THREE.WebGLRenderer({
                canvas: document.querySelector('#smartphone') as HTMLCanvasElement,
                alpha: true
            });
            renderer.setPixelRatio(window.devicePixelRatio);
            renderer.setSize(500, 500);

            ambientLight = new THREE.AmbientLight(0xcccccc);
            scene.add(ambientLight);
			
            directionalLight = new THREE.DirectionalLight(0xffffff);
            directionalLight.position.set(0, 1, 1).normalize();
            scene.add(directionalLight);

            loader = new GLTFLoader();
            loader.load('/smartphone.glb', function (gltf) {
                smartphone = gltf.scene;
                smartphone.scale.set(2, 2, 2);
                smartphone.position.set(0, 0, 0);
                scene.add(smartphone);
            }, undefined, function (error) {
                console.error(error);
            });
        }

        const render = () => {
            renderer.render(scene, camera);
        }

        const animate = () => {
            requestAnimationFrame(animate);

            if (smartphone) {
                smartphone.rotation.x += 0.005;
                smartphone.rotation.y += 0.005;
            }

            render();
        }

        init();
        animate();
    }*/
</script>

<div class="container">
    <h1>Hello World!</h1>
</div>

<style>
    
</style>