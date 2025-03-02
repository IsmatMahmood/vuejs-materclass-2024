<script setup lang="ts">
import { supabase } from '@/lib/supabaseClient';
import { h, ref } from 'vue';
import type { Tables } from 'database/types';
import type { ColumnDef } from '@tanstack/vue-table';
import DataTable from '@/components/ui/data-table/DataTable.vue';

const tasks =  ref<Tables<'tasks'>[] | null>(null)

;(async () => {
  const {data, error} = await supabase.from('tasks').select()

  if (error) console.log(error)
  tasks.value = data
})()


const columns: ColumnDef<Tables<'tasks'>>[] = [
  {
    accessorKey: 'name',
    header: () => h('div', { class: 'text-left' }, 'Name'),
    cell: ({ row }) => {
      return h('div', { class: 'text-left font-medium' }, row.getValue('name'))
    },
  }
]
</script>

<template>
    <DataTable v-if="tasks" :columns="columns" :data="tasks" />
</template>