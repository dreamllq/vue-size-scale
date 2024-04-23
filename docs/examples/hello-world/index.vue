<template>
  <div style='position: relative; height: 500px; display: flex; flex-direction: column;'>
    <div style='height: 20px; display: flex;'>
      <div style='width: 20px;' />
      <div style='flex: 1; position: relative;'>
        <px-scale />
      </div>
      <div style='width: 20px;' />
    </div>
    <div style='flex: 1;display: flex;'>
      <div style='width: 20px; position: relative;'>
        <px-scale placement='left' />
      </div>
      <div style='flex: 1; position: relative;' />
      <div style='width: 20px; position: relative;'>
        <px-scale placement='right' />
      </div>
    </div>
    <div style='height: 20px; display: flex;'>
      <div style='width: 20px;' />
      <div style='flex: 1; position: relative;'>
        <px-scale placement='bottom' />
      </div>
      <div style='width: 20px;' />
    </div>
  </div>
</template>

<script setup lang="ts">
import { PxScale } from '@/index.ts';

</script>

<style scoped>

</style>