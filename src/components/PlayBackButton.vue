<script setup>
  import '../style/playbackbutton.css';
  const emit = defineEmits();
  const props = defineProps({
    is_playing: Boolean,
  })

  const playBackOnClick = () => {
    const is_playing = !props.is_playing;
    emit('setPlayBackStatus', is_playing);
  };

</script>

<template>
  <button  
    class="playback-btn mb-3"
    @click="playBackOnClick"
    :class="[props.is_playing ? 'btn-pause' : 'btn-play']"
  />
</template>