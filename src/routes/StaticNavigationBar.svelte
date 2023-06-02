<script lang="ts">
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    const notifyToggleTheme = () => {
        dispatch("toggleTheme");
    }
</script>

<nav>
    <a href="/"><img src="/images/logo.svg" alt="Quantos Logo"></a>
    <ul class="nav-links">
        <li><a class="nav-link with-hover-transition" href="/why-quantos">Why Quantos?</a></li>
        <li><a class="nav-link with-hover-transition" href="/trainings">Trainings</a></li>
        <li><a class="nav-link with-hover-transition" href="/about">About</a></li>
        <li><a class="nav-link with-hover-transition" href="/contact">Contact</a></li>
    </ul>
    <a href="https://app.quantos.online"><button class="nav-button">Launch App</button></a>
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