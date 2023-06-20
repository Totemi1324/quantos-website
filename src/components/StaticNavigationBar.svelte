<script lang="ts">
    import { browser } from '$app/environment';
    import { createEventDispatcher, onMount, onDestroy } from 'svelte';
    import * as rive from '@rive-app/canvas';

    import { Theme } from '../stores/theme';
    import MediaQuery from './shared/MediaQuery.svelte';
    import HoverEffectButton from './shared/HoverEffectButton.svelte';

    export let theme: Theme;
    let lastThemeToggle: Date;
    let lastLowVisionToggle: Date;

    const dateDifference = (first: Date, second: Date) =>
        Math.abs(first.getTime() - second.getTime());

    const dispatch = createEventDispatcher();

    const notifyToggleTheme = () => {
        if (!lastThemeToggle || dateDifference(new Date(), lastThemeToggle) > 1300) {
            lastThemeToggle = new Date();
            dispatch('toggleTheme');
        }
    };
    const notifyToggleLowVision = () => {
        if (!lastLowVisionToggle || dateDifference(new Date(), lastLowVisionToggle) > 1300) {
            lastLowVisionToggle = new Date();
            dispatch('toggleLowVision');
        }
    };

    let toggleThemeRiveInstance: rive.Rive;
    let toggleLowVisionRiveInstance: rive.Rive;
    let toggleThemeCanvas: HTMLCanvasElement;
    let toggleLowVisionCanvas: HTMLCanvasElement;

    onMount(() => {
        if (browser) {
            const init = () => {
                toggleThemeRiveInstance = new rive.Rive({
                    src: '/animations/toggle_theme_button.riv',
                    canvas: toggleThemeCanvas,
                    autoplay: true,
                    stateMachines: 'ListenForPress'
                });
                toggleLowVisionRiveInstance = new rive.Rive({
                    src: '/animations/toggle_lowvision_button.riv',
                    canvas: toggleLowVisionCanvas,
                    autoplay: true,
                    stateMachines: 'ListenForPress'
                });
            };

            init();
        }
    });

    onDestroy(() => {
        if (toggleThemeRiveInstance) {
            toggleThemeRiveInstance.cleanup();
        }
        if (toggleLowVisionRiveInstance) {
            toggleLowVisionRiveInstance.cleanup();
        }
    });
</script>

<nav>
    <a href="/">
        {#if theme != Theme.Light}
            <img src="/images/logo_darkBackground.svg" alt="Quantos Logo" />
        {:else}
            <img src="/images/logo_lightBackground.svg" alt="Quantos Logo" />
        {/if}
    </a>
    <MediaQuery query="(min-width: 70rem)" let:matches>
        {#if matches}
            <ul class="nav-links">
                <li>
                    <a class="nav-link with-hover-transition" href="/why-quantos">Why Quantos?</a>
                </li>
                <li><a class="nav-link with-hover-transition" href="/trainings">Trainings</a></li>
                <li><a class="nav-link with-hover-transition" href="/about">About</a></li>
                <li><a class="nav-link with-hover-transition" href="/contact">Contact</a></li>
            </ul>
        {/if}
    </MediaQuery>
    <div class="interactive">
        <canvas
            id="toggle-theme-button"
            width="57"
            height="57"
            bind:this={toggleThemeCanvas}
            on:click={notifyToggleTheme}
        />
        <canvas
            id="toggle-lowvision-button"
            width="57"
            height="57"
            bind:this={toggleLowVisionCanvas}
            on:click={notifyToggleLowVision}
        />
        <HoverEffectButton href="https://app.quantos.online/">
            Launch App
        </HoverEffectButton>
    </div>
</nav>

<style lang="scss">
    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: clamp(0.5rem, 3vw, 1.5rem) 3%;
    }

    .interactive {
        min-width: clamp(20rem, 30vw, 30rem);
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .interactive > canvas {
        cursor: pointer;
    }

    .nav-links {
        list-style: none;
    }

    .nav-links li {
        display: inline-block;
        padding: 0 20px;
    }

    .with-hover-transition {
        transition: all 0.3s ease 0s;
    }
    .with-hover-transition:hover {
        transition: all 0.3s ease 0s;
        color: var(--theme-text-description);
    }

    .nav-link {
        font-size: 1em;
        font-weight: 600;
        color: var(--theme-text-base);
        text-decoration: none;
    }
</style>
