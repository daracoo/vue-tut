<template>
    <nav 
        :class="[useDarkNavBar ? 'navbar-dark bg-dark' : 'navbar-light bg-light', 'navbar', 'navbar-expand-lg']"
    >
        <div class="container-fluid">
            <a class="navbar-brand" href="#">My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <navbar-link
                    v-for="(page, index) in publishedPages" class="nav-item" :key="index"
                        :page="page"
                        :index="index"
                        :isActive="activePage === index"
                        @activated="$emit('activated')">
                    </navbar-link>

                    <li>
                        <router-link
                            to="/create" 
                            class="nav-link" 
                            aria-current="page">
                            Create Page
                        </router-link>  
                    </li>
            </ul>
            <form class="d-flex">
                <button 
                    class="btn btn-primary" 
                    @click.prevent="$emit('toggle-navbar-theme')"
                >
                    Toggle Navbar
                </button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';

export default {
    components: { NavbarLink },
    computed: {
        publishedPages(){
            return this.pages.filter(p=>p.published)
        }
    },
    props: ['pages', 'activePage', 'useDarkNavBar', 'navLinkClick']
};
</script>