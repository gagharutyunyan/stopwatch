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
            let second = this.stopwatchs[id].time.second;
            this.stopwatchs[id].isActive = !this.stopwatchs[id].isActive;
            if (this.stopwatchs[id].isActive) {
                this.stopwatchs[id].interval = setInterval(() => {
                    this.stopwatchs[id].time.second++;
                    if (this.stopwatchs[id].time.second >= 60) {
                        this.stopwatchs[id].time.second = 0;
                        this.stopwatchs[id].time.minute++;
                    } else if (this.stopwatchs[id].time.minute >= 60) {
                        this.stopwatchs[id].time.minute = 0;
                        this.stopwatchs[id].time.hour;
                    }
                }, 1000);
            } else {
                clearInterval(this.stopwatchs[id].interval);
            }
        },
        reset(id) {
            this.stopwatchs[id].time.second = 0;
            this.stopwatchs[id].time.minute = 0;
            this.stopwatchs[id].time.hour = 0;
            this.stopwatchs[id].isActive = false;
            clearInterval(this.stopwatchs[id].interval);
            this.stopwatchs[id].interval = null;
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
