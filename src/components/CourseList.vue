<template>
    <section class="grid">
        <CourseCard 
            v-for="c in courses" 
            :key="c.id" 
            :course="c"
            @save="$emit('save', c.id)"
            />
        </section>
    </template>

<!--SCRIPT-->
<script setup>
import CourseCard from './CourseCard.vue';

defineProps({
    courses: {
        type: Array,
        default: () => []
    }
});

defineEmits(["save"]);
</script>

<!--STYLE-->
<style scoped>
.grid{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
}
@media(min-width: 1024px){
  .grid > * { grid-column : span 3;} /*4 columns*/
}
@media (min-width: 640px) and (max-width: 1023px) {
  .grid > * { grid-column: span 6; } /* 2 columns */
}
@media (max-width: 639px) {
  .grid > * { grid-column: span 12; } /* 1 column */
}
</style>