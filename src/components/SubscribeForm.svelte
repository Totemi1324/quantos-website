<script lang="ts">
    import HoverEffectButton from './shared/HoverEffectButton.svelte';
    import { onMount } from 'svelte';

    import {
        type DocumentData,
        type CollectionReference,
        collection,
        addDoc
    } from 'firebase/firestore';
    import { initializeApp } from 'firebase/app';
    import { getFirestore } from 'firebase/firestore';

    let firstName: string = '';
    let email: string = '';
    let success: boolean = false;

    let subscriberCollection: CollectionReference<Subscriber>;

    const firebaseConfig = {
        apiKey: 'AIzaSyB98oT0lmcKov_YPxF99mTLqVt6FPDUI0s',
        authDomain: 'quantos-website.firebaseapp.com',
        projectId: 'quantos-website',
        storageBucket: 'quantos-website.appspot.com',
        messagingSenderId: '465073767089',
        appId: '1:465073767089:web:23254e7d37fe63a5089890',
        measurementId: 'G-9MN1ZPV5EB'
    };
    interface Subscriber {
        firstName: string;
        email: string;
    }

    onMount(() => {
        const app = initializeApp(firebaseConfig);
        const firestore = getFirestore(app);

        const createCollectionRef = <T = DocumentData>(collectionName: string) => {
            return collection(firestore, collectionName) as CollectionReference<T>;
        };

        subscriberCollection = createCollectionRef<Subscriber>('newsletter-subscribers');
    });

    const onSubmit = async () => {
        if (!validate() || success) return;

        const data: Subscriber = {
            firstName: firstName,
            email: email
        };

        const documentReference = await addDoc(subscriberCollection, data);
        if (documentReference) success = true;
    };

    const validate = (): boolean => {
        return true;
    };
</script>

<div>
    {#if !success}
        <input type="text" bind:value={firstName} placeholder="First name" />
        <input type="email" bind:value={email} placeholder="Email address" />
        <HoverEffectButton on:click={onSubmit}>Submit</HoverEffectButton>
    {:else}
        <p class="confirmation-text">
            Thanks for taking interest in Quantos! We received your submission. Should you change
            your mind about this, please drop us a message at help@quantos.online.
        </p>
    {/if}
</div>

<style>
    input {
        color: var(--theme-text-base);
        font-size: 1em;
        margin: 1em 0;
        display: block;
        width: 60%;
        padding: 12px;
        border: 3px solid var(--theme-primary);
        border-radius: 100vmin;
        background: none;
    }

    .confirmation-text {
        color: rgb(67, 186, 115);
    }
</style>
