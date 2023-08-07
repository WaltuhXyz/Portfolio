<script lang="ts">
	import Header from "./Header.svelte";
	import WorkList from "./WorkList.svelte";
    import dictJson from "$lib/assets/json/dictionary.json";
    import { dictionary, locale, _ } from "svelte-i18n";
	import Footer from "./Footer.svelte";

    // Locales
    dictionary.set(<any>dictJson);
    locale.set("en");
</script>

<svelte:head>
    <title>Waltuh.xyz</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin=true>
    <link href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@300&display=swap" rel="stylesheet">
</svelte:head>

<div class="container">
    <Header />

    <div class="h-top-space">
        <h1>{$_("title")}</h1>
        <p>{$_("brief")}</p>
    </div>

    <div class="h-top-space">
        <h3>{$_("list.title")}</h3>

        <WorkList />
    </div>
</div>

<Footer />

<style>
    .h-top-space {
        margin-top: 7.75rem;
    }
</style>
