<script setup>
import { computed } from 'vue';
import { 
  AlertTriangle, 
  TrendingDown, 
  Activity, 
  ArrowRight, 
  CheckCircle, 
  Search 
} from 'lucide-vue-next';

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  size: {
    type: [Number, String],
    default: 16
  },
  color: {
    type: String,
    default: 'currentColor'
  }
});

const iconComponent = computed(() => {
  switch (props.name) {
    case 'AlertTriangle': return AlertTriangle;
    case 'TrendingDown': return TrendingDown;
    case 'Activity': return Activity;
    case 'ArrowRight': return ArrowRight;
    case 'CheckCircle': return CheckCircle;
    case 'Search': return Search;
    default: return null;
  }
});
</script>

<template>
  <component 
    :is="iconComponent" 
    :size="size" 
    :color="color" 
    v-if="iconComponent"
  />
</template>

