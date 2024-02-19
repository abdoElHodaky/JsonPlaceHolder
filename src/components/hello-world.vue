<template>
    <v-container>
        <v-layout
            text-xs-center
            wrap>
            <v-flex xs12>
                <v-data-table
                    class="elevation-1"
                    :headers="headers"
                    :items="comments"
                    
                    >
                    <template
                        v-if="status.success"
                        v-slot:items="props">
                        <td class="text-xs-left">
                            {{ props.item.id }}
                        </td>
                        <td class="text-xs-left">
                            <!-- Stupid users -->
                            {{ props.item.email | lower }}
                        </td>
                        <td class="text-xs-left">
                            {{ props.item.body }}
                        </td>
                    </template>
                    <template
                        v-if="showErrorMessage"
                        v-slot:no-data>
                        <v-alert
                            :value="true"
                            color="error"
                            icon="mdi-alert">
                            Sorry, nothing to display here :(
                        </v-alert>
                    </template>
                </v-data-table>
              <v-dialog
      v-model="dialog"
      persistent
      max-width="600px"
    >
      <template v-slot:activator="{ on, attrs }">
       <v-fab-transition>
              <v-btn
                color="primary"
                dark
                absolute
                bottom
                right
                fab
                v-bind="attrs"
                v-on="on" 
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </v-fab-transition>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">comment</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <!--v-col
                cols="12"
                sm="6"
                md="4"
              >
                <v-text-field
                  label="number"
                  required
                ></v-text-field>
              </v-col-->
              
              
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
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
              <p>{{comments}}</p>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
import { getComments } from '../lib/fake-data-client.js';

export default {
    name: 'HelloWorld',
    filters: {
        lower (original) {
            return original.toLowerCase();
        },
    },
    methods: {
     
    async load(){
      if(localStorage.comments)
      { this.comments=JSON.parse(localStorage.comments)}
      else{
       const response = await getComments(10);
        this.status.requestOccured = true;
        if (response.success) {
            this.status.success = true;
            this.comments = response.comments;
            //window.localStorage.setItem("comments",JSON.stringify(comments))
            this.commentnum=response.comments.reverse()[0].id
        } else {
            this.status.success = false;
            this.status.errorMessage = response.error;
            this.comments = [];
        }
      }
     },
      
    async addcomment(){
      
        await this.comments.push({
          id:this.commentnum++,
          email:this.comment.email,
          body:this.comment.message
        })
        localStorage.comments=JSON.stringify(this.comments)
        this.dialog=false
       // window.localStorage.setItem("comments",JSON.stringify(comments))
       // this.
       this.load()
      }
     
    },
    data () {
        return {
            headers: [
                {
                    text: 'Comment Number',
                    align: 'left',
                    sortable: true,
                    value: 'id',
                },
                {
                    text: 'E-Mail',
                    align: 'left',
                    sortable: true,
                    value: 'email',
                },
                {
                    text: 'Message',
                    align: 'left',
                    sortable: true,
                    value: 'body',
                },
            ],
            comments: [],
           commentnum:1,
            comment:{
              email:"",
              message:""
            },
            dialog:false,
            status: {
                requestOccured: false,
                success: false,
                errorMessage: '',
            },
        };
    },
    computed: {
        showErrorMessage () {
            if (this.status.requestOccured && !this.status.success) {
                return true;
            }

            return false;
        },
    },
    async mounted () {
      
      //let comments=JSON.parse(window.localStorage.getItem("comments"))
      if(localStorage.comments){
        localStorage.comments=JSON.stringify(this.comments)
      }
      else{
      await this.load()}
      console.log(this.comment)
    }
};
</script>
