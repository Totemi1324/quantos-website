<script lang="ts">
    import HoverEffectButton from './shared/HoverEffectButton.svelte';
    import { onMount } from 'svelte';

    import { type DocumentData, type CollectionReference, collection } from 'firebase/firestore';
    import { initializeApp } from 'firebase/app';
    import { getFirestore } from 'firebase/firestore';

    import { firebaseConfig } from '../lib/firebase';
    import type { Subscriber } from '../lib/types';

    let firstName: string = '';
    let email: string = '';

    let subscriberCollection: CollectionReference<Subscriber>;

    onMount(() => {
        const app = initializeApp(firebaseConfig);
        const firestore = getFirestore(app);

        const createCollectionRef = <T = DocumentData>(collectionName: string) => {
            return collection(firestore, collectionName) as CollectionReference<T>;
        };

        subscriberCollection = createCollectionRef<Subscriber>('newsletter-subscribers');
    });

    const onSubmit = () => {};
</script>

<div>
    <input type="text" bind:value={firstName} placeholder="First name" />
    <input type="text" bind:value={email} placeholder="Email address" />
    <HoverEffectButton on:click={onSubmit}>Submit</HoverEffectButton>
</div>

<style>
</style>
