<script lang="ts">
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    const notifyToggleTheme = () => {
        dispatch("toggleTheme");
    }
</script>

<style>

</style>