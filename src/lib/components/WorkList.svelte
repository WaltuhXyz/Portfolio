<script lang="ts">
	import type { Repository } from "$lib/helpers/ghtypes";
    import Missing from "$lib/assets/images/missing.png";
	import { onMount } from "svelte";
    import { fly } from "svelte/transition";

    let repos: Array<Repository> = [];

    onMount(async () => {
        const endpoint = "https://api.github.com/orgs/WaltuhXyz/repos"

        async function fetchRepositories(): Promise<Repository[]> {
            console.debug("Fetching repos from Github API");
            const r = await fetch(endpoint, {
                headers: {
                    "Accept": "application/vnd.github+json",
                    "X-GitHub-Api-Version": "2022-11-28",
                },
            });

            // Validate
            console.debug("Validating response");
            if (!r.ok) {
                console.error(`Fetch failed with ${r.status}`);
                return [];
            }

            return await r.json();
        }

        repos = (await fetchRepositories()).slice(0, 20);
    });

    function getRawCoverURL(repo: Repository): string {
        return `https://raw.githubusercontent.com/${repo.full_name}/waltuh/meta/cover.png`
    }

    function getTitle(repo: Repository): string {
        return repo.name.replaceAll("-", " ");
    }

    function getActualURL(repo: Repository): string {
        if (repo.homepage) {
            return repo.homepage;
        }
        return `https://github.com/${repo.full_name}`;
    }

    function imgErrorHandler(event: Event, repo: Repository) {
        (<HTMLImageElement>event.target).src = Missing;
    }
</script>

<div class="worklist grid">
    {#each repos as repo}
        <a href={getActualURL(repo)} title={repo.full_name}>
            <div transition:fly={{
                delay: 250,
                duration: 2500,
                y: "1rem"
            }} class="repo">
                <img loading="lazy" class="cover" on:error={(event) => imgErrorHandler(event, repo)}
                                                                src={getRawCoverURL(repo)} alt="cover">
                <p>{getTitle(repo)}</p>
            </div>
        </a>
    {/each}
</div>

<style>
    .cover {
        border-radius: 5px;
        display: block;
        max-width: 100%;
        height: auto;
    }

    .worklist {
        margin-top: 1.94rem;
        max-width: 100%;
    }

    .repo {
        transition: all 3s;
    }

    .repo:hover {
        transform: translateY(-1.5rem)
    }
</style>
