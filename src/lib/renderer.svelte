<script lang="ts">
  import type { Result } from '@malloydata/malloy';
  import '@malloydata/render/webcomponent';
  import { getMalloyModel } from './malloy';

  export let query: string;

  let result: Result;

  const model = getMalloyModel('malloy-model');

  $: {
    result = model.runQuery(query);
  }

  function props(node, props = {}){
    Object.assign(node, props)
  }
</script>

{#await result then data}
  <malloy-render use:props={{result: data}}></malloy-render>
{/await}
