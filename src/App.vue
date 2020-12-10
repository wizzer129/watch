<template>
    <v-app style="-webkit-app-region: drag">
        <v-navigation-drawer v-model="drawer" :mini-variant.sync="mini" permanent color="#2C3A47" dark app>
            <v-list-item class="px02 pt-1">
                <v-list-item-avatar>
                    <v-img src="./assets/watch.jpg" alt="admin" class="mx-auto" />
                </v-list-item-avatar>
                <v-list-item-title class="ml-4 text-capitalize">Lazo Ltd</v-list-item-title>
            </v-list-item>
            <v-list shaped class="clickable">
                <template v-for="item in items">
                    <v-list-group
                        v-if="item.children"
                        :key="item.text"
                        v-model="item.model"
                        :prepend-icon="item['icon-ctr']"
                        :append-icon="item.mode ? item.icon : item['icon-alt']"
                        active-class="orange--text"
                    >
                        <template v-slot:activator>
                            <v-list-item-content>
                                <v-list-item-title>
                                    {{ item.text }}
                                </v-list-item-title>
                            </v-list-item-content>
                        </template>
                        <v-list-item
                            v-for="(child, i) in item.children"
                            :key="i"
                            route
                            :to="child.route"
                            active-class="orange"
                        >
                            <v-list-item-action v-if="child.icon">
                                <v-icon>{{ child.icon }}</v-icon>
                            </v-list-item-action>

                            <v-list-item-content>
                                <v-list-item-tile>
                                    {{ child.text }}
                                </v-list-item-tile>
                            </v-list-item-content>
                        </v-list-item>
                    </v-list-group>
                    <v-list-item v-else :key="item.text" active-class="orange--text" route :to="item.route">
                        <v-list-item-action>
                            <v-icon>{{ item.icon }}</v-icon>
                        </v-list-item-action>
                        <v-list-item-title>
                            {{ item.text }}
                        </v-list-item-title>
                    </v-list-item>
                </template>
            </v-list>
        </v-navigation-drawer>
    </v-app>
</template>

<script>
export default {
    name: 'App',
    props: {
        source: String,
    },

    data: () => ({
        drawer: null,
        mini: false,
        fab: false,
        items: [
            { icon: 'mdi-home', text: 'Dashboard', route: '/' },
            {
                icon: 'mdi-chevron-up',
                'icon-alt': 'mdi-chevron-down',
                'icon-ctr': 'mdi-cart-arrow-right',
                text: 'Orders',
                model: false,
                children: [
                    { icon: 'style', text: 'Type', route: '/Type' },
                    { icon: 'atm', text: 'Mark', route: '/Mark' },
                ],
                route: '/',
            },
            {
                icon: 'mid-chevron-up',
                'icon-alt': 'mdi-chevron-down',
                'icon-ctr': 'mdi-google-maps',
                text: 'Tracking',
                model: false,
                children: [
                    { icon: 'mdi-tooltip-account', text: 'Locate', route: '/locate' },
                    { icon: 'mdi-printer', text: 'Print', route: '/print' },
                ],
                route: '/',
            },
            { icon: 'mdi-finance', text: 'Revenue', route: '/revenue' },
            { icon: 'mdi-chart-pie', text: 'Analytics', route: '/chart' },
            { icon: 'mdi-magnify', text: 'Search', route: '/Recherche' },
        ],
    }),
};
</script>

<style>
.clickable {
    -webkit-app-region: no-drag;
}
</style>
