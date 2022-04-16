<script>
  import { t } from "./i18n";
</script>

<sl-alert open variant="success">
  <sl-icon slot="icon" name="info-circle" />
  <div class="flex items-center justify-between">
    <h3 class="title-md">{$t("found")}</h3>
    <sl-button class="mt-2" href={"/in-editor?"} size="small" variant="success">
      <sl-icon name="box-arrow-up-right" />
      {$t("open")}
    </sl-button>
  </div>
</sl-alert>
<sl-alert open>
  <sl-icon slot="icon" name="info-circle" />
  <h3 class="title-md">
    {$t("directory")}
  </h3>
</sl-alert>
<!-- filter = only show directories -->
<ol class="rounded border divide-y">
  <h3 class="title-md px-4 py-3 bg-surface-100">{$t("file")}</h3>
  {#await new Promise() then paths}
    {#each paths as { path, isDirectory }}
      <li class="px-4 py-2">
        {#if isDirectory}
          <a
            class="link"
            sveltekit:prefetch
            href={`/git/?dir=${paths + path}/`}
          >
            <sl-icon name="folder-fill" class="mr-2" />
            {path}
          </a>
        {:else}
          <sl-icon name="file-text-fill" class="mr-2" />
          {path}
          {#if path.includes("inlang.config.json")}
            <sl-tag variant="success" size="small" class="ml-2">
              Configuration found
            </sl-tag>
          {/if}
        {/if}
      </li>
    {/each}
  {/await}
</ol>
