<template>
    <div class="main">
        <StopWatch
            v-for="stopwatch in stopwatchs"
            :key="stopwatch.id"
            :stopwatch="stopwatch"
            :play="play"
            :reset="reset"
        />
        <StopWatchAdder :add="add" />
    </div>
</template>

<script>
import StopWatch from '@/components/StopWatch.vue';
import StopWatchAdder from '@/components/StopWatchAdder.vue';

export default {
    name: 'Main',
    data() {
        return {
            stopwatchs: [
                {
                    id: 0,
                    isActive: false,
                    time: {
                        second: 0,
                        minute: 0,
                        hour: 0,
                    },
                    interval: null,
                },
            ],
        };
    },
    components: {
        StopWatch,
        StopWatchAdder,
    },
    methods: {
        play(id) {
            const stopwatch = this.stopwatchs[id];
            const time = stopwatch.time;
            stopwatch.isActive = !stopwatch.isActive;
            if (stopwatch.isActive) {
                stopwatch.interval = setInterval(() => {
                    time.second++;
                    if (time.second >= 60) {
                        time.second = 0;
                        time.minute++;
                    } else if (time.minute >= 60) {
                        time.minute = 0;
                        time.hour;
                    }
                }, 1000);
            } else {
                clearInterval(stopwatch.interval);
            }
        },
        reset(id) {
            const stopwatch = this.stopwatchs[id];
            const time = stopwatch.time;
            time.second = 0;
            time.minute = 0;
            time.hour = 0;
            stopwatch.isActive = false;
            clearInterval(stopwatch.interval);
            stopwatch.interval = null;
        },
        add() {
            this.stopwatchs = [
                ...this.stopwatchs,
                {
                    id: this.stopwatchs.length,
                    isActive: false,
                    time: {
                        second: 0,
                        minute: 0,
                        hour: 0,
                    },
                    interval: null,
                },
            ];
        },
    },
};
</script>
