<template>
    <v-app>
        <v-toolbar app>
            <v-toolbar-title class="headline text-uppercase">
                <span>Task</span>
                <span class="font-weight-light"></span>
            </v-toolbar-title>
            <v-spacer />
            <v-btn
                flat
                href=""
                target="_blank">
                <span class="mr-2"></span>
                <v-icon>mdi-plus</v-icon>
            </v-btn>
        </v-toolbar>

        <v-content>
            <router-view />
        </v-content>
    </v-app>
</template>

<script>

export default {
    name: 'App',
    data () {
        return {
            //
        };
    },
};

</script>
