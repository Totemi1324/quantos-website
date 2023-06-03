<script lang="ts">
    import { onMount } from 'svelte';

    export let query: string;

    let mediaQueryList: MediaQueryList;
    let mediaQueryListener: any;
    let wasMounted = false;
    let matches = false;

    onMount(() => {
        wasMounted = true;
        return () => {
            removeActiveListener();
        };
    });

    $: {
        if (wasMounted) {
            removeActiveListener();
            addNewListener(query);
        }
    }

    function addNewListener(query: string) {
        mediaQueryList = window.matchMedia(query);
        mediaQueryListener = (event: { matches: boolean }) => (matches = event.matches);
        mediaQueryList.addEventListener('change', mediaQueryListener);
        matches = mediaQueryList.matches;
    }

    function removeActiveListener() {
        if (mediaQueryList && mediaQueryListener) {
            mediaQueryList.removeEventListener('change', mediaQueryListener);
        }
    }
</script>

<slot {matches} />
