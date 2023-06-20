<script lang="ts">
    import { createEventDispatcher } from 'svelte';

    export let href: string | undefined = undefined;

    const dispatch = createEventDispatcher();

    const notifyClick = () => dispatch('click');
</script>

{#if href}
<a href={href ? href : ""}>
    <div class="container">
        <button class="button-body button-text" on:click={notifyClick}>
            <slot/>
        </button>
    </div>
</a>
{:else}
<div class="container">
    <button class="button-body button-text" on:click={notifyClick}>
        <slot/>
    </button>
</div>
{/if}

<style>
    .button-text {
        text-decoration: none;
        font-family: 'Josefin Sans';
        color: var(--theme-text-base);
        font-size: 1.3em;
        padding: 0.7em 1em;
        transition: color 350ms ease;
    }
    .button-text:hover {
        color: white;
    }

    .container {
        position: relative;
    }

    .button-body {
        cursor: pointer;
        border: 2px solid var(--theme-primary);
        border-radius: 100vmin;
        background: none;
        position: relative;
        z-index: 10;
    }

    .button-body:before {
        background: linear-gradient(
            130deg,
            transparent 0% 33%,
            var(--theme-primary) 66%,
            var(--theme-secondary) 100%
        );
        background-position: 0% 0%;
        background-size: 300% 300%;
        transition: background-position 350ms ease, transform 350ms ease;
        content: "";
        position: absolute;
        left: -5px;
        top: -5px;
        width: calc(100% + 10px);
        height: calc(100% + 10px);
        border-radius: 100vmin;
        z-index: -1;
    }
    .button-body:hover:before {
        background-position: 100% 100%;
        transform: scale(1.08, 1.03);
    }
</style>