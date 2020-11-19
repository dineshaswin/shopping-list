<template>
    <div class="todo pa-3">
        <h3>Your Shopping List</h3>
        <v-col cols="12"
               sm="6">
            <v-text-field v-model="newItem"
                          class="pt-2"
                          @click:append="addItem"
                          @keyup.enter="addItem"
                          outlined
                          label="Add Items"
                          append-icon="mdi-plus"
                          hide-details
                          clearable></v-text-field>
        </v-col>
        <v-list flat>
            <v-list-item v-for="item in stuffs"
                         :key="item.id">
                <v-list-item @click="itemBought(item.id)"
                             :class="{ 'teal lighten-3' : item.bought}">
                    <template v-slot:default>
                        <v-list-item-action>
                            <v-checkbox :input-value="item.bought"
                                        color="primary"></v-checkbox>
                        </v-list-item-action>

                        <v-list-item-content>
                            <v-list-item-title :class="{'text-decoration-line-through' : item.bought}">
                                {{item.name}}
                            </v-list-item-title>

                        </v-list-item-content>

                        <v-list-item-action>
                            <v-btn icon
                                   @click="snackbar = true"
                                   @click.stop="deleteItem(item.id)">
                                <v-icon color="grey lighten-1">mdi-delete</v-icon>
                            </v-btn>
                        </v-list-item-action>
                    </template>
                </v-list-item>
            </v-list-item>

        </v-list>
        
        <v-snackbar v-model="snackbar"
                    :timeout="timeout">
            {{ text }}

            <template v-slot:action="{ attrs }">
                <v-btn color="blue"
                       text
                       v-bind="attrs"
                       @click="snackbar = false">
                    Close
                </v-btn>
            </template>
        </v-snackbar>

    </div>
</template>

<script>

    export default {
        name: 'Home',
        data() {
            return {
                newItem:'',
                stuffs: [
                    {
                        name: "tomato",
                        qt: 1,
                        id: 1,
                        bought: false,
                    },
                    {
                        name: "potato",
                        qt: 1,
                        id: 2,
                        bought: false,
                    },
                ],
                snackbar: false,
                text: 'Task was deleted.',
                timeout: 2000,
            }  
        },
        methods: {
            addItem() {
                let newItemList = {
                    id: Date.now(),
                    name: this.newItem,
                    bought: false,
                    qt: 1,
                }
                this.stuffs.push(newItemList)
            },
            deleteItem(id) {
                this.stuffs = this.stuffs.filter(task => task.id !== id)
            },
            itemBought(id) {
                let item = this.stuffs.filter(item => item.id === id)[0]
                item.bought = !item.bought
            }
        }
}
</script>
