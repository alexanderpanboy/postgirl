<template>
  <v-container fluid class="overflow-y-auto py-0">
    <v-layout align-space-around justify-space-around fill-height wrap class="px-8 pt-0 pb-0 mr-1">
      <v-flex md2 xs5 class="pl-1 d-flex justify-center">
        <v-card max-width="260" height="870" class="ml-0 pr-0 justify-space-between" color="grey lighten-3" tile flat>
          <ul class="pl-0">
            <div align="center">
              <v-btn color="grey lighten-1" class="my-2 mb-5 justify-center" width="180" depressed tile dark flat>
                Create
              </v-btn>
            </div>
            <div>
              <v-list-group no-action sub-group class="px-0" :value="true" disabled>
                <template v-slot:activator>
                  <v-list-item-content class="margin-right:5px;">
                    <v-list-item-title class="pr-0">
                      GFaceManager
                      <v-menu :offset-x="true" :closeOnContentClick="false">
                        <template v-slot:activator="{ on }">
                          <v-btn @click="onPlusButtonClick" v-on="on" style="float:right" class="mb-1"
                            color="grey lighten-3" depressed tile x-small>
                            <v-icon>mdi-plus</v-icon>
                          </v-btn>
                        </template>
                        <v-card>
                          <v-text-field placeholder="Add item" v-model="addItem1">
                            <v-icon type="button" slot="append" color="black" @click="onPlusAddItem1()">mdi-plus
                            </v-icon>
                          </v-text-field>
                        </v-card>
                      </v-menu>
                      <v-btn @click="onPlusButtonClick" style="float:right" class="mb-1" color="grey lighten-3"
                        depressed tile x-small>
                        <v-icon>mdi-chevron-down</v-icon>
                      </v-btn>
                    </v-list-item-title>
                  </v-list-item-content>
                </template>
                <v-divider></v-divider>
                <v-list-item v-for="admin in admins" :key="admin.title" class="pl-12 ml-0" link>
                  <v-list-item-title @mouseover="hover = true" @mouseleave="hover = false" v-text="admin.title">
                  </v-list-item-title>
                  <v-btn v-show="hover" @click="onRemoveItem1" style="float:right" class="mb-1"
                    color="grey lighten-3" depressed tile x-small>
                    <v-icon>mdi-close-circle-outline</v-icon>
                  </v-btn>
                </v-list-item>
              </v-list-group>
            </div>
            <div>
              <v-list-group no-action sub-group value="true" disabled>
                <template v-slot:activator>
                  <v-list-item-content>
                    <v-list-item-title class="pr-0">
                      GFaceUser
                      <v-menu :offset-x="true" :closeOnContentClick="false">
                        <template v-slot:activator="{ on }">
                          <v-btn @click="onPlusButtonClick" v-on="on" style="float:right" class="mb-1"
                            color="grey lighten-3" depressed tile x-small>
                            <v-icon>mdi-plus</v-icon>
                          </v-btn>
                        </template>
                        <v-card>
                          <v-text-field placeholder="Add item" v-model="addItem2">
                            <v-icon type="button" slot="append" color="black" @click="onPlusAddItem2()">mdi-plus
                            </v-icon>
                          </v-text-field>
                        </v-card>
                      </v-menu>
                      <v-btn @click="onPlusButtonClick" style="float:right" class="mb-1" color="grey lighten-3"
                        depressed tile x-small>
                        <v-icon>mdi-chevron-down</v-icon>
                      </v-btn>
                    </v-list-item-title>
                  </v-list-item-content>
                </template>
                <v-divider></v-divider>
                <v-list-item v-for="crud in cruds" :key="crud.title" class="pl-12 ml-0" @click="">
                  <v-list-item-title @mouseover="hover = true" @mouseleave="hover = false" v-text="crud.title">
                  </v-list-item-title>
                  <v-btn v-show="hover" @click="onRemoveItem2"" style="float:right" class="mb-1"
                    color="grey lighten-3" depressed tile x-small>
                    <v-icon>mdi-close-circle-outline</v-icon>
                  </v-btn>
                </v-list-item>
              </v-list-group>
            </div>
          </ul>
        </v-card>
      </v-flex>
      <v-flex md10 xs7 class="px-0">
        <v-card max-width="1400" height="870" class="d-flex justify-center ml-12" color="grey lighten-3" tile flat>
          <v-container>
            <v-row>
              <v-expansion-panels>
                <v-expansion-panel v-for="(item,i) in apis" :key="i">
                  <v-expansion-panel-header>{{item.title}}
                    <template v-slot:actions>
                      <v-btn tile large icon>
                        <v-icon>mdi-format-vertical-align-bottom</v-icon>
                      </v-btn>
                      <v-btn tile large icon>
                        <v-icon>mdi-play-circle-outline</v-icon>
                      </v-btn>
                      <v-icon>$expand</v-icon>
                    </template>
                  </v-expansion-panel-header>
                  <v-expansion-panel-content>
                    <GFaceManagerPage />
                    <v-col v-for="param in params" cols="12">
                      <v-card :color="item.color" dark>
                        <div class="d-flex flex-no-wrap justify-space-between">
                          <div>
                            <v-card-title class="headline">{{param}}</v-card-title>
                            <v-card-subtitle v-text="item.artist"></v-card-subtitle>
                            <v-card-actions>
                              <div>
                                <v-btn text>EDIT</v-btn>
                              </div>
                            </v-card-actions>
                          </div>
                        </div>
                      </v-card>
                    </v-col>
                    <div>
                      <v-btn text>SAVE</v-btn>
                    </div>
                  </v-expansion-panel-content>
                </v-expansion-panel>
              </v-expansion-panels>
            </v-row>
          </v-container>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: 'MainPage',
    data() {
      return {
        hover: false,
        addItem1: '/',
        addItem2: '/',
        selectedSubItem: {},
        admins: [
          { title: '/user' },
          { title: '/record' },
          { title: '/authorization' },
          { title: '/account' },
          { title: '/antipassback' },
        ],
        cruds: [
          { title: '/user' },
        ],
        apis: [
          { title: 'GET' },
          { title: 'POST' },
          { title: 'PUT' },
          { title: 'PATCH' },
          { title: 'DELETE' },
          { title: 'COPY' },
          { title: 'HEAD' },
          { title: 'OPTIONS' },
          { title: 'LINK' },
          { title: 'UNLINK' },
          { title: 'PURGE' },
          { title: 'LOCK' },
          { title: 'UNLOCK' },
          { title: 'PROPFIND' },
          { title: 'VIEW' },
        ],
        params: [
          'Parameters',
          'Body',
          'Header',
        ],
      }
    },
    methods: {
      /* update state to maintain selected option and toggle view */
      updateSelected(selecteditem) {
        this.selectedSubItem = selecteditem;
      },
      /*Prevent the click event of the button from bubbling out*/
      onPlusButtonClick(event) {
        event.cancelBubble = true;
      },
      onExpandButtonClick(event) {
        event.cancelBubble = true;
      },
      onPlusAddItem1() {
        var newAddItem1 = this.addItem1;
        if (!newAddItem1) { return; }
        this.admins.push(
          { title: newAddItem1 }
        );
        this.addItem1 = '/' + '';
      },
      onRemoveItem1() {
           console.log('thisadmins');
    },
      onPlusAddItem2() {
        var newAddItem2 = this.addItem2;
        if (!newAddItem2) { return; }
        this.cruds.push(
          { title: newAddItem2 }
        );
        this.addItem2 = '/' + '';
      },
      onRemoveItem2() {
        var removed = this.admin.splice(index, 1);
           console.log('thnoeirgo');
    },
    }
  };
</script>
<style type="text/css">
  /* Cancel the formatted capital letter on v-btn */
  .v-btn {
    text-transform: none !important;
    font-size: 17px !important;
    font-weight: 350 !important;
  }

  /* Style the buttons */
  .v-list-group {
    border: none;
    outline: none;
    padding: 5px 5px;
    background-color: "grey lighten-1";
    cursor: pointer;
  }

  /* Style the active class, and buttons on mouse-over */
  .v-list-item:hover {
    background-color: #339FFF;
    color: white !important;
  }

  .v-list-item {
    min-height: 20px !important;
  }

  .v-list-item__content {
    padding: 3px !important;
  }

  .v-list-item__title {
    font-size: 18px !important;
    font-weight: 400 !important;
    color: #000000 !important;
    padding: 3px;
    margin: 0px;
  }

  .v-list-item__icon:first-child {
    margin-right: 0px !important;
  }

  .v-list-group__header {
    padding: 0px !important;
    text-align: left !important;
    color: #000000 !important;
  }

  .v-icon {
    transform: none !important;
  }

  .mdi-menu-down::before {
    display: none;
  }
</style>