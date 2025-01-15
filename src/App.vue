<template>
    <navbar 
        :pages="pages" 
        :active-page="activePage" 
        :use-dark-nav-bar="useDarkNavBar" 
        @toggle-navbar-theme="toggleNavbarTheme">
    </navbar>        

    
        <page-viewer 
            v-if="pages.length > 0"
            :page="pages[activePage]">
        </page-viewer>

    <create-page
        @page-created="pageCreated"
    >
    </create-page>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import Navbar from './components/Navbar.vue';
import CreatePage from './components/CreatePage.vue';

export default {
    components: {
        Navbar,
        PageViewer,
        CreatePage
    },
    created() {
        this.getPages();
        this.loadTheme();

        this.$bus.$on('navbarLinkActivated', (index) => {
            this.activePage = index;
        });
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
        },
        pageCreated(pageObj){
            this.pages.push(pageObj);
            console.log(pageObj);
        }
    }
};
</script>