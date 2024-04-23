<template>
  <div
    ref='pxScaleRef'
    class='size-scale px-scale'
    :class='`${placement}-scale`'
    :style='style'>
    <template v-for='(item, index) in scales' :key='index'>
      <div
        class='scale-item'
        :class='`${item.type}-scale-item`'
        :style='{
          top: (placement=== "left" || placement==="right")? `${item.size}px`:undefined,
          left: (placement=== "top" || placement==="bottom")? `${item.size}px`:undefined,
        }' />
    </template>
    <template v-for='(item,index) in scaleTexts' :key='index'>
      <div
        class='scale-text'
        :style='{
          top: (placement=== "left" || placement==="right")? `${item.offset+2}px`:undefined,
          left: (placement=== "top" || placement==="bottom")? `${item.offset+2}px`:undefined,
        }'>
        {{ item.offset }}
      </div>
    </template>
  </div>
</template>

<script setup lang="ts">
import { PropType, computed, ref } from 'vue';
import { useElementSize } from '@vueuse/core';

const props = defineProps({
  placement: {
    type: String as PropType<'top' | 'right' | 'bottom' | 'left'>,
    default: 'top'
  },
  particleSize: {
    type: Number,
    default: 5
  }
});

const pxScaleRef = ref();
const { width, height } = useElementSize(pxScaleRef);

const style = ref({});

const scaleCount = computed(() => {
  const size = (props.placement === 'top' || props.placement === 'bottom') ? width.value : height.value;
  const count = Math.floor(size / props.particleSize) + 1;
  return count;
});

const scales = computed(() => {
  const count = scaleCount.value;
  const _scales:{size: number, type: 'small' | 'normal' | 'large'}[] = [];

  for (let i = 0; i < count; i++) {
    _scales.push({
      size: i * props.particleSize,
      type: i % 10 === 0 ? 'large' : (i % 5 === 0 ? 'normal' : 'small')
    });
  }

  return _scales;
});

const scaleTexts = computed(() => {
  const step = 20;
  const count = Math.floor(scaleCount.value / step);
  
  const texts:{offset: number}[] = [];

  for (let i = 1; i < count; i++) {
    texts.push({ offset: i * step * props.particleSize });
  }
  return texts;
});
</script>

<style scoped lang="scss">
.px-scale{
  position: absolute;
  --scale-border-color: #333;
  --scale-border: 1px solid var(--scale-border-color);
  --small-scale-size: 4px;
  --normal-scale-size: calc(2 * var(--small-scale-size));
  --large-scale-size: calc(4 * var(--small-scale-size));
  --scale-size: calc(5 * var(--small-scale-size));

  &.top-scale{
    top:0;
    .scale-item{
      bottom:0;
    }

    .scale-text{
      top: var(--small-scale-size);
    }
  }

  &.bottom-scale{
    bottom:0;
    .scale-item{
      top:0;
    }

    .scale-text{
      bottom: var(--small-scale-size);
    }
  }

  &.left-scale{
    left:0;
    height: 100%;
    .scale-item{
      right:0;
    }

    .scale-text{
      left: var(--small-scale-size);
    }
  }

  &.right-scale{
    right:0;
    .scale-item{
      left:0;
    }

    .scale-text{
      right: var(--small-scale-size);
    }
  }

  &.top-scale,&.bottom-scale{
    width: 100%;
    height: var(--scale-size);
    .scale-item{
      border-left: var(--scale-border);

      &.small-scale-item{
        height: var(--small-scale-size);
      }
      &.normal-scale-item{
        height: var(--normal-scale-size);
      }
      &.large-scale-item{
        height: var(--large-scale-size);
      }
    }
  }

  &.left-scale,&.right-scale{
    height: 100%;
    width: var(--scale-size);
    .scale-item{
      border-top: var(--scale-border);

      &.small-scale-item{
        width: var(--small-scale-size);
      }
      &.normal-scale-item{
        width: var(--normal-scale-size);
      }
      &.large-scale-item{
        width: var(--large-scale-size);
      }
    }

    .scale-text{
      writing-mode: vertical-rl;
    }
  }

  .scale-item{
    position: absolute;
  }

  .scale-text{
    position: absolute;
    font-size: 12px;
    line-height: 1;
  }
}
</style>