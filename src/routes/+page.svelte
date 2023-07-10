<script lang="ts">
    import SubscribeForm from '../components/SubscribeForm.svelte';
    //import { browser } from '$app/environment';
    /*import * as rive from '@rive-app/canvas';
    
    import { onMount, onDestroy } from 'svelte';*/
    /*import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';
    import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
    import * as THREE from 'three';

    if (browser) {
        let camera: THREE.PerspectiveCamera;
        let scene: THREE.Scene;
        let renderer: THREE.WebGLRenderer;
        let loader: GLTFLoader;
        let smartphone: THREE.Group;
        let directionalLight: THREE.DirectionalLight;
        let ambientLight: THREE.AmbientLight;
        let controls: OrbitControls;

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
            renderer.setSize(1000, 1000);

            controls = new OrbitControls(camera, renderer.domElement);

            ambientLight = new THREE.AmbientLight(0xcccccc);
            scene.add(ambientLight);

            directionalLight = new THREE.DirectionalLight(0xffffff);
            directionalLight.position.set(0, 1, 1).normalize();
            scene.add(directionalLight);

            loader = new GLTFLoader();
            loader.load(
                '/other/smartphone.glb',
                function (gltf) {
                    smartphone = gltf.scene;
                    smartphone.scale.set(1, 1, 1);
                    smartphone.position.set(0, -15, 0);
                    smartphone.rotation.set(1.3, 0, -0.2);
                    scene.add(smartphone);
                },
                undefined,
                function (error) {
                    console.error(error);
                }
            );
        };

        const render = () => {
            renderer.render(scene, camera);
        };

        const animate = () => {
            requestAnimationFrame(animate);

            if (smartphone) {
                controls.update();
                //smartphone.rotation.x += 0.005;
                //smartphone.rotation.y += 0.005;
            }

            render();
        };

        init();
        animate();
    }*/
    /*let riveInstance: rive.Rive;
    let riveCanvas: HTMLCanvasElement;

    onMount(() => {
        if (browser) {
            const init = () => {
                riveInstance = new rive.Rive({
                    src: '/animations/downloadbutton.riv',
                    canvas: riveCanvas,
                    autoplay: true,
                    stateMachines: 'ListenForPress',
                    onLoad: () => {
                        riveInstance.resizeDrawingSurfaceToCanvas();
                    },
                });
            };

            init();
        }
    });

    onDestroy(() => {
        if (riveInstance) {
            riveInstance.cleanup();
        }
    });*/
</script>

<div class="container">
    <h1>Quantum computing at your fingertips.</h1>
    <p>
        Sign up to be among the first to know about updates to Quantos and the release of the full
        version!
    </p>
    <SubscribeForm />
</div>

<style>
    h1 {
        margin-top: 10vh;
    }
</style>
