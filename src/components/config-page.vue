<template>
    <v-card>
        <v-card-title class="headline grey lighten-1">
            Choose your preferred resources
        </v-card-title>
        <v-container>
            <v-slider
                    class="font-weight-bold"
                    min="0"
                    max="3"
                    step="1"
                    label="CPU"
                    :thumb-label="true"
                    thumb-color="blue"
                    ticks
            ></v-slider>
            <v-slider
                    class="font-weight-bold"
                    min="0"
                    max="2048"
                    step="128"
                    label="RAM"
                    :thumb-label="true"
                    thumb-color="blue"
                    ticks
            ></v-slider>
            <v-slider
                    class="font-weight-bold"
                    min="0"
                    max="15000"
                    step="100"
                    label="Disk Storage (GB)"
                    :thumb-label="true"
                    thumb-color="blue"
                    ticks
            ></v-slider>
        </v-container>
        <v-btn
                width="100%"
                dark
                @click="toggleConfigOverlay"
        >
            Change
        </v-btn>
    </v-card>
</template>
<script>
    export default {
        name: 'config_page',
        props: {
            configOverlay: Boolean,
            toggleConfigOverlay: null
        }
    }
</script>
