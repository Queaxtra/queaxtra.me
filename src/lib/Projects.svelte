<script lang="ts">
    import { onMount } from "svelte";

    let url = "https://api.github.com/users/Queaxtra/repos";
    let repos: any[] = [];

    onMount(async () => {
        let response = await fetch(url);
        repos = await response.json();
        console.log(repos);
    });
</script>

<div class="relative mt-36">
    <h2 class="relative ml-10 md:ml-20 lg:ml-60 text-2xl md:text-4xl lg:text-4xl">Projects</h2>

    {#if !repos.length}
    <div class="transition-all duration-300 relative inline-block ml-10 md:ml-20 lg:ml-60 md:-mx-44 lg:-mx-44 border-2 border-[#1c1c1c] w-72 md:w-[35rem] lg:w-80 p-5 rounded bg-[#18181b]/30 mt-10 text-white/70">
        <p><i class="fa-solid fa-rotate animate-spin"></i> Loading Data..</p>
    </div>
    {:else}
    {#each repos as repo}
    <div class="transition-all duration-300 hover:scale-105 relative inline-block ml-10 md:ml-20 lg:ml-60 md:-mx-44 lg:-mx-44 border-2 border-[#1c1c1c] w-72 md:w-[35rem] lg:w-80 p-5 rounded bg-[#18181b]/30 mt-10 text-white/70">
        <div class="float-right">
            <p class="text-yellow-500"><i class="fa-solid fa-star"></i> <span class="text-lg">{repo.stargazers_count}</span></p>
        </div>
        <h2 class="text-lg md:text-xl lg:text-xl">{repo.name}</h2>
        <a class="text-xs md:text-xs lg:text-xs relative" href={repo.html_url}>View on Github <i class="fa-solid fa-arrow-up-right-from-square"></i></a>
    </div>
    {/each}
    {/if}
</div>