<script lang="ts">
    import { browser } from '$app/environment';
    import { createEventDispatcher, onMount, onDestroy } from 'svelte';
    import * as rive from '@rive-app/canvas';

    import { Theme } from '../stores/theme';
    import MediaQuery from './shared/MediaQuery.svelte';

    export let theme: Theme;

    const dispatch = createEventDispatcher();

    const notifyToggleTheme = () => {
        dispatch('toggleTheme');
    };

    let toggleThemeRiveInstance: rive.Rive;
    let toggleThemeCanvas: HTMLCanvasElement;

    onMount(() => {
        if (browser) {
            const init = () => {
                toggleThemeRiveInstance = new rive.Rive({
                    src: '/animations/toggle_theme_button.riv',
                    canvas: toggleThemeCanvas,
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
    });
</script>

<nav>
    <a href="/">
        {#if theme == Theme.Dark}
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
        <canvas id="toggle-theme-button" width="50" height="50" bind:this={toggleThemeCanvas} on:click={notifyToggleTheme}/>
        <a href="https://app.quantos.online">
            <button class="nav-button">Launch App</button>
        </a>
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

    .nav-button {
        @extend .nav-link;
        font-family: 'Josefin Sans';
        font-size: 1.3em;
        padding: 0.7em 1em;
    }
</style>
