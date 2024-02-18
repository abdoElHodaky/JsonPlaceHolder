<template>
    <v-app>
        <v-toolbar app>
            <v-toolbar-title class="headline text-uppercase">
                <span>Task</span>
                <span class="font-weight-light"></span>
            </v-toolbar-title>
            <v-spacer />
             <!--v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
       <v-btn

           color="primary"
          flat
          v-bind="attrs"
          v-on="on" >
                <span class="mr-2"></span>
                <v-icon>mdi-plus</v-icon>
            </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">comment</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="number"
                  required
                ></v-text-field>
              </v-col>
              <v-col
              
              <v-col cols="12">
                <v-text-field
                  v-model="comment.email"
                  label="Email*"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  v-model="comment.message"
                  label="Message*"
                  type="textarea"
                  required
                ></v-text-field>
              </v-col>
              <v-col
                cols="12"
                sm="6"
              >
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue darken-1"
            text
            @click="addcomment"
          >
            Close
          </v-btn>
          <v-btn
            color="blue darken-1"
            text
            @click="dialog = false"
          >
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog-->

          
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
            dialog:false,
            comment:{}
        };
    },
};

</script>
