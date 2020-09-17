<template>
<v-card>
    <v-tabs v-model="timerType" grow>
        <v-tab v-for="tab in tabsTitles" :key="tab">{{ tab }}</v-tab>
        <v-tabs-items v-model="timerType">
            <v-tab-item>
                <v-card flat class="pa-5">
                    <h1 class="text-h1 text-center font-weight-bold">
                        {{ displayMinutes }}:{{ displaySeconds }}
                    </h1>
                    <div class="text-center">
                        <v-btn @click="start" color="primary" class="mx-2">
                            <v-icon left small>mdi-play-circle-outline</v-icon>
                            Start
                        </v-btn>
                        <v-btn @click="stop" class="mx-2">
                            <v-icon left small>mdi-stop-circle-outline</v-icon>
                            Stop
                        </v-btn>
                        <v-btn @click="reset" class="mx-2" :disabled="isRunning">
                            <v-icon left small>mdi-restart</v-icon>
                            Reset
                        </v-btn>
                    </div>
                </v-card>
            </v-tab-item>
        </v-tabs-items>
    </v-tabs>
</v-card>
</template>

<script>
export default {
    data() {
        return {
            isRunning: false,
            timerInstance: null,
            totalSeconds: 25 * 60,
            timerType: 0,
            tabsTitles: ["Pomodoro", "Short Brake", "Long Brake"]
        };
    },
    computed: {
        displayMinutes() {
            let minutes = Math.floor(this.totalSeconds / 60);
            return this.foramtTime(minutes);
        },
        displaySeconds() {
            let seconds = this.totalSeconds % 60;
            return this.foramtTime(seconds);
        }
    },
    methods: {
        foramtTime(time) {
            return time < 10 ? "0" + time : time.toString();
        },
        start() {
            this.stop();
            this.isRunning = true;
            this.timerInstance = setInterval(() => {
                this.totalSeconds -= 1;
            }, 1000);
        },
        stop() {
            this.isRunning = false;
            clearInterval(this.timerInstance);
        },
        reset() {
            this.stop();
            this.totalSeconds = 25 * 60;
        }
    }
};
</script>
