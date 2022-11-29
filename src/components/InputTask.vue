<script lang="ts">
import { defineComponent, ref, reactive, computed } from "vue";

export default defineComponent({
  setup() {
    let taskinput = ref("");
    let tasklists: Array<string> = reactive([]);
    const addtask = () => {
      tasklists.push(taskinput.value);
      taskinput.value = "";
    };
    const deltask = (i: number) => {
      tasklists.splice(i, 1);
    };

    return {
      taskinput,
      tasklists,
      addtask,
      deltask,
    };
  },
});
</script>

<template>
  <div class="w-screen px-4">
    <input
      type="text"
      name="taskinput"
      id="taksinput"
      placeholder="Input new task"
      class="p-2 px-4 rounded-xl bg-amber-100 text-amber-800 focus:outline-none focus:bg-amber-200 w-full placeholder-slate-600"
      v-model="taskinput"
      @keyup.enter="addtask"
    />
  </div>
  <div class="w-full pt-4 px-8 mx-auto">
    <ul>
      <li v-for="(tasklist, i) in tasklists" :key="i" class="py-1">
        <label>
          <input type="checkbox" class="apperance-none accent-neutral-50" />
          {{ tasklist }}
          <button
            class="rounded-xl bg-red-200 text-red-900 hover:bg-red-500 hover:text-red-200 px-5 float-right"
            @click.prevent="deltask(i)"
          >
            delete
          </button>
        </label>
      </li>
    </ul>
  </div>
</template>
