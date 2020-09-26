<template>
    <div class="stopwatch">
        <div class="stopwatch__time">
            <span v-if="stopwatch.time.minute === 0">
                {{ stopwatch.time.second }}
            </span>
            <span v-else-if="stopwatch.time.minute > 0">
                {{ stopwatch.time.minute }}:{{ stopwatch.time.second }}
            </span>
            <span v-else-if="stopwatch.time.hour > 0">
                {{ stopwatch.time.hour }}:{{ stopwatch.time.minute }}:{{
                    stopwatch.time.second
                }}
            </span>
        </div>
        <hr />
        <div class="stopwatch-buttons">
            <div class="buttons">
                <button
                    @click="play(stopwatch.id)"
                    :class="[
                        stopwatch.isActive
                            ? 'btn buttons__pause'
                            : 'btn buttons__play',
                    ]"
                ></button>
                <button
                    @click="reset(stopwatch.id)"
                    class="btn buttons__reset"
                ></button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'StopWatch',
    props: ['stopwatch', 'play', 'reset'],
};
</script>
