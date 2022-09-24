<script>
  export let name;
</script>

<div
  class="flex flex-col gap-2 sm:max-w-sm p-4 rounded bg-gray-100 justify-center"
>
  <label>
    <p>character name</p>
    <input
      class="rounded px-2 bg-gray-200 w-full"
      type="text"
      bind:value={name}
    />
  </label>
</div>
