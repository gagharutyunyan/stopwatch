<template>
    <div class="stopwatch adder">
        <button @click="add" class="btn add"></button>
    </div>
</template>

<script>
export default {
    name: 'StopWatchAdder',
    props: ['add'],
};
</script>
