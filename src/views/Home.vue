<template>
  <div>
    <v-flex v-if="isLoaded">
   <v-data-table
    :headers="headersval"
    :items="itemsData"
    :items-per-page="10"
    class="elevation-1"
  >
   <template v-slot:item.thumbnailUrl="{ item }">
            <div class="p-2">
              <v-img :src="item .thumbnailUrl" :alt="item .title" height="100px"></v-img>
            </div>
          </template>
    <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >New Item</v-btn>
          </template>
          <v-card>
           

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="itemsData.thumbnailUrl" label="thumbnailUrl"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="itemsData.albumId" label="albumId"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="itemsData.title" label="title"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="itemsData.url" label="url"></v-text-field>
                  </v-col>
                  
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="save">Save</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
  </v-data-table>
  </v-flex>
  </div>
</template>

<script lang="ts">
// @ is an alias to /src
import { Component, Prop, Vue ,Watch} from "vue-property-decorator";
import ToDoApp from '@/components/ToDoApp.vue'
import {default as axios, AxiosStatic, AxiosInstance} from 'axios';

 @Component({

  }) 

export default class Home extends Vue {
  public getData: any;
  public headersval: any;
  public itemsData: any;
  public isLoaded: any = true;
  public dialog = false;
  public editedIndex=-1;
  public editedItem= {
        thumbnailUrl: '',
        albumId: '',
        title: '',
        url: '',
      
      };
     public defaultItem={
        thumbnailUrl: '',
        albumId: '',
        title: '',
        url: '',
      }
  created() {
    this.headersval = [  { text: 'Photo Thumbnail', value: 'thumbnailUrl' },
          { text: 'Album ID', value: 'albumId' },
          { text: 'Title', value: 'title' },
          { text: 'Image', value: 'url' },
          {text: 'Actions', value: 'actions'}
          ];
    //  axios
    //   .get('https://jsonplaceholder.typicode.com/photos')
    //   .then(response => {
    //     this.isLoaded = true;
      
    //     (this.itemsData = response.data)
    //      console.log(this.itemsData );
    //   }
    //   )
  
          this.itemsData = [{thumbnailUrl:"https://via.placeholder.com/150/92c952",
          albumId:1,
          title:"accusamus beatae ad facilis cum similique qui sunt",
              url:"https://via.placeholder.com/600/92c952"
          }]
  }
    // @Watch(this.dialog) public getDialog() {
    //   !this.dialog
    // }
  mounted() {
    
      this.itemsData = [{thumbnailUrl:"https://via.placeholder.com/150/92c952",
          albumId:1,
          title:"accusamus beatae ad facilis cum similique qui sunt",
              url:"https://via.placeholder.com/600/92c952"
          }]
  }
  /*eslint no-debugger: "error"*/
  editItem (item) {
    /* eslint-disable no-debugger */
    debugger;
        this.editedIndex = this.itemsData.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      }

      deleteItem (item) {
        const index = this.itemsData.indexOf(item)
        confirm('Are you sure you want to delete this item?') && this.itemsData.splice(index, 1)
      }
   public close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      }

     public save () {
        if (this.editedIndex > -1) {
          Object.assign(this.itemsData[this.editedIndex], this.editedItem)
        } else {
          this.itemsData.push(this.editedItem)
        }
        this.close()
      }
 public navigateProfile() {
   this.$router.push('Profile');
  }
 
   public navigateTodo() {
    this.$router.push('ToDOApp');
  }
  }

</script>
<style scoped>
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 50%;
  width:50%;
}
.heading {
      margin: 10px 165px;
}
.todobtn {
  margin: 52px 208px;
}
.prfbtn {
  margin: 52px 208px;
}
</style>