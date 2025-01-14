<template>
    <navbar 
        :pages="pages" 
        :active-page="activePage" 
        :use-dark-nav-bar="useDarkNavBar" 
        :nav-link-click="(index) => activePage = index" 
        @toggle-navbar-theme="toggleNavbarTheme">
    </navbar>        

    <page-viewer 
        v-if="pages.length > 0"
        :page="pages[activePage]">
    </page-viewer>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import Navbar from './components/Navbar.vue';

export default {
    components: {
        Navbar,
        PageViewer,
    },
    created() {
        this.getPages();
        this.loadTheme();
    },
    data() {
        return {
            activePage: 0,
            useDarkNavBar: false,
            pages: []
        };
    },
    methods: {
        async getPages() {
            let res = await fetch('pages.json');
            let data = await res.json();
            this.pages = data;
        },
        toggleNavbarTheme() {
            this.useDarkNavBar = !this.useDarkNavBar;
            const theme = this.useDarkNavBar ? 'dark' : 'light';
            localStorage.setItem('theme', theme);
        },
        loadTheme() {
            const savedTheme = localStorage.getItem('theme');
            this.useDarkNavBar = savedTheme === 'dark';
        }
    }
};
</script>