<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import { Theme } from '../stores/theme';
    import MediaQuery from './shared/MediaQuery.svelte';

    export let theme: Theme;

    const dispatch = createEventDispatcher();

    const notifyToggleTheme = () => {
        dispatch('toggleTheme');
    };
</script>

<nav>
    <a href="/">
        {#if theme == Theme.Dark}
            <img src="/images/logo_darkBackground.svg" alt="Quantos Logo" />
        {:else}
            <img src="/images/logo_lightBackground.svg" alt="Quantos Logo" />
        {/if}
    </a>
    <MediaQuery query="(min-width: 60rem)" let:matches>
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
    <a href="https://app.quantos.online"
        ><button class="nav-button" on:click={notifyToggleTheme}>Launch App</button></a
    >
</nav>

<style lang="scss">
    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: clamp(0.5rem, 3vw, 1.5rem) 3%;
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
