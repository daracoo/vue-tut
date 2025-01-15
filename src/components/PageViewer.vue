<template>
    <div v-if="page" class="container mt-4">
        <h1>{{page.pageTitle}}</h1>
        <p>{{page.content}}</p>
    </div>
</template>

<script>
export default{
    created(){
        this.page = this.$pages.getSinglePage(this.$route.params.index);
    },
    data(){
        return{
            page:null
        }
    }
}

</script>