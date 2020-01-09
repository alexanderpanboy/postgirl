<template>
  <v-container fluid class="overflow-y-auto py-0">
    <v-layout
      align-space-around
      justify-space-around
      fill-height
      wrap
      class="px-8 pt-0 pb-0 mr-1"
    >
      <v-flex md2 xs5 class="pl-1 d-flex justify-center">
        <v-card
          max-width="260"
          height="870"
          class="ml-0 pr-0 justify-space-between"
          color="grey lighten-3"
          tile
          flat
        >
          <ul class="pl-0" style="width:235px">
            <div align="center">
              <v-btn
                @click.stop="dialog = true"
                color="grey lighten-1"
                class="my-2 mb-5 justify-center"
                width="180"
                depressed
                tile
                dark
                flat
                >Create
              </v-btn>

              <v-dialog v-model="dialog" persistent max-width="600px">
                <v-card>
                  <v-card-title>
                    <span class="headline">CREATE A NEW PROJECT</span>
                  </v-card-title>
                  <v-card-text>
                    <v-container>
                      <v-row>
                        <v-col cols="12">
                          <v-text-field
                            v-model="createdProject"
                            label="PROJECT NAME*"
                            required
                          ></v-text-field>
                        </v-col>
                      </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                  </v-card-text>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" text @click="dialog = false"
                      >Cancel</v-btn
                    >
                    <v-btn
                      color="blue darken-1"
                      text
                      @click="
                        dialog = false;
                        onCreateProject();
                      "
                      >Create</v-btn
                    >
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </div>
      <!-- sideBararray: [
        { title: "Gface", content: [{ name: "/1" }, { name: "/2" }] },
        { title: "Gface2", content: [{ name: "/1" }, { name: "/2" }] },
        { title: "new", content: [] },
      ], -->
<!--       
            <div v-for="(item, index) in sideBararray" :key="index">
              <div>{{item.title}}</div>
              <div v-for="(child, y) in item.content" :key="y">   
                <div>{{child.name}}</div>
              </div>           
            </div> -->
            <div>
              <v-list-group
                no-action
                sub-group
                class="px-0"
                disabled
                v-for="(item, index) in sideBararray"
                :value="item.isExpanded"
                :key="index"
              >
                <template v-slot:activator>
                  <v-list-item-content class="margin-right:5px;">
                    <v-list-item-title class="pr-0">
                      {{item.title}}
                      <v-menu :offset-x="true" :closeOnContentClick="false">
                        <template v-slot:activator="{ on }">
                          <v-btn
                            icon
                            @click="onPlusButtonClick(item, event)"
                            v-on="on"
                            style="float:right"
                            class="mb-1"
                            color="black"
                            depressed
                            tile
                            small
                          >
                            <v-icon>mdi-plus-circle-outline</v-icon>
                          </v-btn>
                        </template>
                      </v-menu>
                      <v-btn
                        icon
                        @click="onExpandButtonClick(item)"
                        style="float:right"
                        class="mb-1"
                        color="black"
                        depressed
                        tile
                        small
                      >
                        <v-icon>mdi-chevron-down-circle-outline</v-icon>
                      </v-btn>
                    </v-list-item-title>
                  </v-list-item-content>
                </template>
                <v-divider></v-divider>

                <v-list-item
                  v-show="item.showInput"
                  @mouseover="hover = true"
                  @mouseleave="hover = false"
                  class="pl-12 ml-0"
                  link
                >
                  <v-list-item-title>
                    <input
                      @keyup.enter="onPlusAddItem(item)"
                      type="text"
                      v-model="addItem"
                      placeholder="Add item"
                      style="width: 130px; background-color: whitesmoke;"
                    />
                  </v-list-item-title>
                  <v-btn
                    icon
                    style="float:right"
                    class="mb-1"
                    color="black"
                    depressed
                    tile
                    x-small
                    @click="onPlusAddItem(item)"
                  >
                    <v-icon>mdi-plus-circle-outline</v-icon>
                  </v-btn>
                </v-list-item>

                <v-list-item
                  v-for="(child, y) in item.content"
                  :key="y"
                  @mouseover="hover = true"
                  @mouseleave="hover = false"
                  class="pl-12 ml-0 itemHover"
                  link
                >
                  <v-list-item-title>
                    <span v-show="!item.content.edit">{{ child.name }}</span>
                    <input
                      v-on:keyup.enter="test(index)"
                      type="text"
                      v-model="child.name"
                      v-show="item.content.edit"
                      style="width: 130px; background-color: whitesmoke;"
                    />
                  </v-list-item-title>
                  <v-btn
                    v-show="hover"
                    icon
                    @click="onEditItem(item)"
                    style="float:right"
                    class="mb-1"
                    color="black"
                    depressed
                    tile
                    x-small
                  >
                    <v-icon>mdi-circle-edit-outline</v-icon>
                  </v-btn>
                  <v-btn
                    v-show="hover"
                    icon
                    @click="onRemoveItem(item, index)"
                    style="float:right"
                    class="mb-1"
                    color="black"
                    depressed
                    tile
                    x-small
                  >
                    <v-icon>mdi-close-circle-outline</v-icon>
                  </v-btn>
                </v-list-item>
              </v-list-group>
            </div>

            <!-- <div>
              <v-list-group
                no-action
                sub-group
                class="px-0"
                :value="expandList2"
                disabled
              >
                <template v-slot:activator>
                  <v-list-item-content class="margin-right:5px;">
                    <v-list-item-title class="pr-0">
                      GFaceUser
                      <v-menu :offset-x="true" :closeOnContentClick="false">
                        <template v-slot:activator="{ on }">
                          <v-btn
                            icon
                            @click="onPlusButtonClick2"
                            v-on="on"
                            style="float:right"
                            class="mb-1"
                            color="black"
                            depressed
                            tile
                            small
                          >
                            <v-icon>mdi-plus-circle-outline</v-icon>
                          </v-btn>
                        </template>
                      </v-menu>
                      <v-btn
                        icon
                        style="float:right"
                        class="mb-1"
                        color="black"
                        depressed
                        tile
                        small
                      >
                        <v-icon>mdi-chevron-down-circle-outline</v-icon>
                      </v-btn>
                    </v-list-item-title>
                  </v-list-item-content>
                </template>
                <v-divider></v-divider>

                <v-list-item
                  v-show="showGFaceUserInput"
                  @mouseover="hover = true"
                  @mouseleave="hover = false"
                  class="pl-12 ml-0"
                  link
                >
                  <v-list-item-title>
                    <input
                      @keyup.enter="onPlusAddItem2()"
                      type="text"
                      v-model="addItem2"
                      placeholder="Add item"
                      style="width: 130px; background-color: whitesmoke;"
                    />
                  </v-list-item-title>
                  <v-btn
                    icon
                    style="float:right"
                    class="mb-1"
                    color="black"
                    depressed
                    tile
                    x-small
                    @click="onPlusAddItem2()"
                  >
                    <v-icon>mdi-plus-circle-outline</v-icon>
                  </v-btn>
                </v-list-item>

                <v-list-item
                  v-for="(crud, index) in cruds"
                  :key="index"
                  @mouseover="hover = true"
                  @mouseleave="hover = false"
                  class="pl-12 ml-0"
                  link
                >
                  <v-list-item-title>
                    <span v-show="!crud.edit">{{ crud.title }}</span>
                    <input
                      :id="`hi-${index}`"
                      @keyup.enter="
                        document.getElementById(`hi-${index}`).blur()
                      "
                      type="text"
                      v-model="crud.title"
                      v-show="crud.edit"
                      style="width: 130px; background-color: whitesmoke;"
                    />
                  </v-list-item-title>
                  <v-btn
                    v-show="hover"
                    icon
                    @click="onEditCrud(crud)"
                    style="float:right"
                    class="mb-1"
                    color="black"
                    depressed
                    tile
                    x-small
                  >
                    <v-icon>mdi-circle-edit-outline</v-icon>
                  </v-btn>
                  <v-btn
                    v-show="hover"
                    icon
                    @click="onRemoveItem2(index)"
                    style="float:right"
                    class="mb-1"
                    color="black"
                    depressed
                    tile
                    x-small
                  >
                    <v-icon>mdi-close-circle-outline</v-icon>
                  </v-btn>
                </v-list-item>
              </v-list-group>
            </div> -->
          </ul>
        </v-card>
      </v-flex>
      <v-flex md10 xs7 class="px-0">
        <v-card
          max-width="1400"
          height="870"
          class="d-flex justify-center ml-12"
          color="grey lighten-3"
          tile
          flat
        >
          <v-container>
            <v-row>
              <v-expansion-panels>
                <v-expansion-panel v-for="(item, i) in apis" :key="i">
                  <v-expansion-panel-header>
                    {{ item.title }}
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
                    <v-col
                      v-for="param in params"
                      v-bind:key="{ param }"
                      cols="12"
                    >
                      <v-card :color="item.color" dark>
                        <div class="d-flex flex-no-wrap justify-space-between">
                          <div>
                            <v-card-title class="headline">
                              {{ param }}
                            </v-card-title>
                            <v-card-subtitle
                              v-text="item.artist"
                            ></v-card-subtitle>
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
  name: "MainPage",
  data() {
    return {
      sideBararray: [
        { isExpanded: true, title: "GFaceManager", showInput: false, content: [{ name: "/dashboard", edit: false, }, { name: "/record", edit: false, }, { name: "/stranger", edit: false, }, { name: "/anti-passback", edit: false, },{ name: "/user", edit: false, },{ name: "/authorization", edit: false, },{ name: "/device", edit: false, }] },
        { isExpanded: true,title: "GFaceUser", showInput: false, content: [{ name: "/user" ,edit: false }] },
      ],
      hover: false,
      dialog: false,
      addItem: "/",
      addProject:"",
      createdProject: "",
      selectedSubItem: {},
      admins: [
        { title: "/dashboard", edit: false },
        { title: "/record", edit: false },
      ],
      cruds: [{ title: "/user", edit: false }],
      apis: [
        { title: "GET" },
        { title: "POST" },
        { title: "PUT" },
        { title: "DELETE" },
        { title: "COPY" },
        { title: "HEAD" },
        { title: "OPTIONS" },
        { title: "LINK" },
        { title: "UNLINK" },
        { title: "PURGE" },
        { title: "LOCK" },
        { title: "UNLOCK" },
        { title: "PROPFIND" },
        { title: "VIEW" }
      ],
      params: ["Parameters", "Body", "Header"],
    };
  },
  methods: {
    test(index) {
      console.log(index);
      document.getElementById(`qq-${index}`).blur();
    },
    onEditItem(item) {
      item.content = Object.assign({}, item.content);
      item.content.edit = true;
    },
    /*Prevent the click event of the button from bubbling out*/
    onExpandButtonClick(item) {
      item.isExpanded = !item.isExpanded;
    },
    onPlusButtonClick(item,event) {
      item.showInput = true;
      event.cancelBubble = true;
    },
    onPlusAddItem(item) {
      var newAddItem = this.addItem;
      if (!newAddItem) {
        return;
      }
      item.content.unshift({ name: newAddItem });
      this.addItem = "/" + "";
      item.showInput = false;
    },
    onRemoveItem(item, index) {
      item.content.splice(index, 1);
    },
    onCreateProject() {
      var newAddProject = this.addProject;
      if (!newAddProject) {
        return;
      }
      sideBararray.append({ title: newAddProject });
      this.addProject ="";
    }
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
.itemHover:hover {
  background-color: #339fff;
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
