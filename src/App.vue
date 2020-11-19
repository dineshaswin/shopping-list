<template>
    <v-app id="inspire">
        <v-navigation-drawer v-model="drawer"
                             app
                             dark>
            <v-list-item>
                <v-list-item-content>
                    <v-list-item-title class="title">
                        {{detail[0].name}}
                    </v-list-item-title>
                    <v-list-item-subtitle>
                        Buy your stuffs!
                    </v-list-item-subtitle>
                </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list dense
                    nav>
                <v-list-item v-for="item in items"
                             :key="item.title"
                             :to="item.to"
                             link>
                    <v-list-item-icon to>
                        <v-icon>{{ item.icon }}</v-icon>
                    </v-list-item-icon>

                    <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>

        <v-app-bar app dark>
            <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

            <v-toolbar-title>ShopApp</v-toolbar-title>
        </v-app-bar>

        <v-main>
            <router-view></router-view>
        </v-main>
    </v-app>
</template>

<script>
    export default {
        data: () => ({
            drawer: null,
            detail: [
                {name: "aswin dinesh"},
            ],
            items: [
                { title: 'Items', icon: 'mdi-format-list-checks', to:'/' },
                { title: 'About', icon: 'mdi-help-box', to:'/about' },
            ],
            right: null,
        }),
    }
</script>