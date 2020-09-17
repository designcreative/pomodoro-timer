<template>
<v-app>
    <v-main>
        <v-container>
            <v-row>
                <v-col sm="6" offset="3">
                    <Pomodoro />
                </v-col>
            </v-row>
        </v-container>
    </v-main>
</v-app>
</template>

<script>
import Pomodoro from "./components/Pomodoro";

export default {
    name: "App",

    components: {
        Pomodoro
    },

    data: () => ({
        //
    })
};
</script>
