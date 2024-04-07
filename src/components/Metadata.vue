<script setup>
  const props = defineProps({
    metadata: Object
  })
</script>

<template>
  <div class="d-flex flex-column mb-4">
    
    <div class="row align-items-center">
      <div class="p-2 col-2 fw-bold">Title</div>
      <div v-if="props.metadata" class="col-5">{{ props.metadata.title }}</div>
    </div>

    <div class="row align-items-center">
      <div class="p-2 col-2 fw-bold">Artist</div>
      <div v-if="props.metadata" class="col-4">{{ props.metadata.artist }}</div>
    </div>

    <div class="row align-items-center">
      <div class="p-2 col-2 fw-bold">Album Artist</div>
      <div v-if="props.metadata" class="col-4">{{ props.metadata.albumartist }}</div>
    </div>

    <div class="row align-items-center">
      <div class="p-2 col-2 fw-bold">Album</div>
      <div v-if="props.metadata" class="col-4">{{ props.metadata.album }}</div>
    </div>

    <div class="row align-items-center">
      <div class="p-2 col-2 fw-bold">Year</div>
      <div v-if="props.metadata" class="col-4">{{ props.metadata.year }}</div>
    </div>

    <div class="row align-items-center">
      <div class="p-2 col-2 fw-bold">Track No.</div>
      <div v-if="props.metadata" class="col-4">{{ props.metadata.track.no }}</div>
    </div>
    
  </div>

</template>

<style>
  .row {
    font-size: 1rem;
  }

  .col-2 {
    border-right: solid 2px #eee;
  }
</style>