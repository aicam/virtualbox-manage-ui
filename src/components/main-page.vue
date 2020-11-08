<template>
    <v-container>
        <v-snackbar
                v-model="snackbar"
        >
            Starting server...

            <template v-slot:action="{ attrs }">
                <v-btn
                        color="pink"
                        text
                        v-bind="attrs"
                        @click="snackbar = false"
                >
                    Close
                </v-btn>
            </template>
        </v-snackbar>
      <v-dialog
              v-model="configOverlay"




              hide-overlay
              transition="dialog-bottom-transition">
      <config_page :configOverlay="configOverlay" :toggleConfigOverlay="toggleConfigOverlay"></config_page>
      </v-dialog>
        <v-banner v-for="vm in vms" :key="vm.name" elevation="2" single-line
                  class="d-flex justify-lg-space-around">
            <v-icon
                    large
                    color="green darken-2"
            >
                {{vm.on ? "cloud_on" : "cloud_off"}}
            </v-icon>
            {{vm.name}}
            <v-card-text class="font-weight-bold justify-space-around row">
                <p>RAM: {{vm.ram}}MB</p>
                <p>CPU: {{vm.cpu}} Core</p>
                <p>Hard Disk: 10GB</p>
            </v-card-text>
            <template v-slot:actions>
                <v-btn
                        v-bind:color="vm.on ? 'red': 'primary'"
                        class="ma-2"
                        dark
                        @click="snackbar = true"
                >
                    {{vm.on ? "Stop" : "Start"}}
                    <v-icon
                            dark
                            right
                    >
                        cloud
                    </v-icon>
                </v-btn>
                <v-btn
                        class="ma-2"
                        color="primary"
                        dark
                        @click="configOverlay = !configOverlay"
                >
                    resource
                    <v-icon
                            dark
                            right
                    >
                        settings
                    </v-icon>
                </v-btn>
                <v-btn
                        class="ma-2"
                        color="primary"
                        dark
                >
                    SSH
                    <v-icon
                            dark
                            right
                    >
                        settings_ethernet
                    </v-icon>
                </v-btn>
                <v-btn
                        class="ma-2"
                        color="primary"
                        dark
                >
                    clone
                    <v-icon
                            dark
                            right
                    >
                        content_copy
                    </v-icon>
                </v-btn>
            </template>
        </v-banner>
    </v-container>
</template>

<script>
    import config_page from './config-page'
    const P_URL = 'http://localhost:2020/';
    const axios = require('axios');
    export default {
        name: 'HelloWorld',
        components: {
            config_page
        },
        data: function () {
            return {
                configOverlay: false,
                vms : null,
                snackbar: false,
            };
        },
      methods: {
          toggleConfigOverlay: function () {
            this.configOverlay = !this.configOverlay
          }
      },
        mounted() {
            axios.get(P_URL + 'get_vms_info')
                .then(response => {
                    this.vms = JSON.parse(response.data.message)
                })
        }
    }
</script>
