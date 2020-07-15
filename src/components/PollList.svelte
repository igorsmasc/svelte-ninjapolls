<script>
  // import { onMount, onDestroy } from "svelte";
  import PollStore from "../stores/PollStore.js";
  import PollDetails from "./PollDetails.svelte";

  // export let polls = [];

  // const unsub = PollStore.subscribe(data => {
  //   polls = data;
  // });

  // onDestroy(() => {
  //   unsub();
  // });
</script>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>

<div class="poll-list">
  {#each $PollStore as poll (poll.id)}
    <div>
      <PollDetails {poll} />
    </div>
  {/each}
</div>
