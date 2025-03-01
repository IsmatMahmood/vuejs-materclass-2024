<script setup lang="ts">
import { useRoute } from 'vue-router'

const route = useRoute()

</script>

<template>
    <div>
      <h1>Single Project {{ route.params?.id }} Page</h1>
    </div>
</template>