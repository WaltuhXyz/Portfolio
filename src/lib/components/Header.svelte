<script lang="ts">
    import { locale } from "svelte-i18n";
    import Logo from "$lib/assets/images/logo.png"

    function switchLocales() {
        if ($locale == "en") {
            locale.set("ru");
        } else {
            locale.set("en");
        }
    }
</script>

<div>
    <img src={Logo} alt="Logo" />
    <p>Waltuhs</p>
    <a href={null} on:click={switchLocales}>{$locale?.toUpperCase()}</a>
</div>

<style>
    img {
        border-radius: 2.5px;
    }

    div {
        width: 100%;
        height: 1.75rem;
        display: flex;
        flex-shrink: 0;
    }

    p, a {
        padding: 0 0 0 0.62rem;
        margin: 0;
        font-size: 1.5rem;
        font-style: normal;
        font-weight: 500;
        line-height: normal;
    }

    a {
        margin-left: auto;
    }

    a:hover {
        cursor: pointer;
    }
</style>
