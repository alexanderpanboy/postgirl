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
              <v-list-group no-action sub-group class="px-0" :value="expandList1" disabled>
                <template v-slot:activator>
                  <v-list-item-content class="margin-right:5px;">
                    <v-list-item-title class="pr-0">
                      GFaceManager
                      <v-menu :offset-x="true" :closeOnContentClick="false">
                        <template v-slot:activator="{ on }">
                          <v-btn icon @click="onPlusButtonClick" v-on="on" style="float:right" class="mb-1"
                            color="black" depressed tile small>
                            <v-icon>mdi-plus-circle-outline</v-icon>
                          </v-btn>
                        </template>
                        <v-card>
                          <v-text-field placeholder="Add item" v-model="addItem1">
                            <v-btn icon slot="append" color="black" @click="onPlusAddItem1()">
                            <v-icon>mdi-plus-circle-outline
                            </v-icon>
                            </v-btn>
                          </v-text-field>
                        </v-card>
                      </v-menu>
                      <v-btn icon @click="onExpandButtonClick1" style="float:right" class="mb-1" color="black"
                        depressed tile small>
                        <v-icon>mdi-chevron-down-circle-outline</v-icon>
                      </v-btn>
                    </v-list-item-title>
                  </v-list-item-content>
                </template>
                <v-divider></v-divider>
                <v-list-item v-for="(admin, index) in admins" :key="admin.title" @mouseover="hover = true"
                  @mouseleave="hover = false" class="pl-12 ml-0" link>
                  <v-list-item-title v-text="admin.title">
                  </v-list-item-title>
                  <v-btn v-show="hover" icon @click="onEditItem1(index)" style="float:right" class="mb-1"
                    color="black" depressed tile x-small>
                    <v-icon>mdi-circle-edit-outline</v-icon>
                  </v-btn>
                  <v-btn v-show="hover" icon @click="onRemoveItem1(index)" style="float:right" class="mb-1"
                    color="black" depressed tile x-small>
                    <v-icon>mdi-close-circle-outline</v-icon>
                  </v-btn>
                </v-list-item>
              </v-list-group>
            </div>
            <div>
              <v-list-group no-action sub-group :value="expandList2" disabled>
                <template v-slot:activator>
                  <v-list-item-content>
                    <v-list-item-title class="pr-0">
                      GFaceUser
                      <v-menu :offset-x="true" :closeOnContentClick="false">
                        <template v-slot:activator="{ on }">
                          <v-btn icon @click="onPlusButtonClick" v-on="on" style="float:right" class="mb-1"
                            color="black" depressed tile small>
                            <v-icon>mdi-plus-circle-outline</v-icon>
                          </v-btn>
                        </template>
                        <v-card>
                          <v-text-field placeholder="Add item" v-model="addItem2">
                            <v-btn icon slot="append" color="black" @click="onPlusAddItem2()">
                            <v-icon>mdi-plus-circle-outline
                            </v-icon>
                            </v-btn>
                          </v-text-field>
                        </v-card>
                      </v-menu>
                      <v-btn icon @click="onExpandButtonClick2" style="float:right" class="mb-1" color="black"
                        depressed tile small>
                        <v-icon>mdi-chevron-down-circle-outline</v-icon>
                      </v-btn>
                    </v-list-item-title>
                  </v-list-item-content>
                </template>
                <v-divider></v-divider>
                <v-list-item v-for="(crud, index) in cruds" :key="crud.title" @mouseover="hover = true"
                  @mouseleave="hover = false" class="pl-12 ml-0" link>
                  <v-list-item-title v-text="crud.title">
                  </v-list-item-title>
                  <v-btn v-show="hover" icon @click="onEditItem2(index)" style="float:right" class="mb-1"
                    color="black" depressed tile x-small>
                    <v-icon>mdi-circle-edit-outline</v-icon>
                  </v-btn>
                  <v-btn v-show="hover" icon @click="onRemoveItem2(index)" style=" float:right" class="mb-1"
                    color="black" depressed tile x-small>
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
        expandList1: true,
        expandList2: true,
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
      onExpandButtonClick1(event) {
        this.expandList1 = !this.expandList1
      },
      onExpandButtonClick2(event) {
        this.expandList2 = !this.expandList2
      },
      onPlusButtonClick(event) {
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
      onPlusAddItem2() {
        var newAddItem2 = this.addItem2;
        if (!newAddItem2) { return; }
        this.cruds.push(
          { title: newAddItem2 }
        );
        this.addItem2 = '/' + '';
      },
      onRemoveItem1(index) {
        this.admins.splice(index, 1);
        console.log(index);
      },
      onRemoveItem2(index) {
        this.cruds.splice(index, 1);
        console.log(index);
      },
      onEditItem1(index) {
        var newAddItem1 = this.addItem1;
        if (!newAddItem1) { return; }
        this.admins.push(
          { title: newAddItem1 }
        );
        this.addItem1 = '/' + '';
        console.log(index);
      },
      onEditItem2(index) {
        var newAddItem2 = this.addItem2;
        if (!newAddItem2) { return; }
        this.cruds.push(
          { title: newAddItem2 }
        );
        this.addItem2 = '/' + '';
        console.log(index);
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
  }

  .v-list-item__title:active {
    color: white !important;
  }

  .v-list-item {
    min-height: 20px !important;
  }

  .v-list-item__content {
    padding: 0px !important;
  }

  .v-list-item__title {
    font-size: 18px !important;
    font-weight: 400 !important;
    color: #000000 !important;
    padding: 2px;
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
    padding: 5px;
    transform: none !important;
  }

  .mdi-menu-down::before {
    display: none;
  }
</style>