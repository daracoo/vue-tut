<template>
    <div class="container mb-3">
        <form action="">
            <div class="mb-3">
                <label for="" class="form-label">
                    Page Title
                </label>
                <input
                    type="text" 
                    class="form-control"
                    :value="pageTitle"
                    @input="(e) => pageTitle = e.target.value"
                /><!--v-model="pageTitle"-->
            </div>
            <div class="mb-3">
                <label for="" class="form-label">
                    Content
                </label>
                <textarea 
                    type="text" 
                    class="form-control" 
                    rows="5"
                    v-model="content">
                </textarea>
            </div>
            <div class="container mb-3">
                    <div class="mb-3">
                        <label for="" class="form-label">
                            Page Title
                        </label>
                        <input 
                            type="text" 
                            class="form-control"
                        />
                    </div>
                    <div class="mb-3">
                        <label for="" class="form-label">
                            Content
                        </label>
                        <textarea 
                            type="text" 
                            class="form-control" 
                            rows="5">
                        </textarea>
                    </div>
                    <div class="mb-3">
                        <label for="" class="form-label">
                            Link Text
                        </label>
                        <input 
                            type="text" 
                            class="form-control"
                            v-model="linkText"
                        />
                    </div>
                    <div class="mb-3">
                        <label for="" class="form-label">
                            Link URL
                        </label>
                        <input 
                            type="text" 
                            class="form-control"
                            v-model="linkUrl"
                        />
                    </div>
                    <div class="row mb-3">
                        <div class="form-check">
                            <input 
                                class="form-check-input"
                                type="checkbox" 
                                id="gridCheck1"
                                v-model="published"
                            />
                            <label 
                                class="form-check-label" 
                                for="gridCheck1">
                                Published
                            </label>
                        </div>
                    </div>
            </div>

            <div class="mb-3">
                <button class="btn btn-primary"
                :disabled="isFromInvalid"
                @click.prevent="submitForm">
                    
                    Create Page
                </button>
            </div>
        </form>
    </div>
</template>

<script>
export default{
    emits: {
        pageCreated({pageTitle, content, link}){
            if(!pageTitle){
                return false;
            }
            if(!content){
                return false;
            }
            if(!link || !link.text || !link.url){
                return false;
            }

            return true;
        }
    },
    computed:{
        isFromInvalid(){
            return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl;
        }
    },
    data(){
        return {
            pageTitle: '',
            content: '',
            linkText: '',
            linkUrl: '',
            published: true
        }
    },
    methods: {
        submitForm(){
            if(!this.pageTitle || !this.content || !this.linkText || !this.linkUrl){
                alert("Please fill the form.");
                return;
            }

            this.$emit('pageCreated', {
                pageTitle: this.pageTitle,
                content: this.content,
                link: {
                    text: this.linkText,
                    link:this.linkText
                },
                published: this.published
            });

            this.pageTitle = '',
            this.content =  '',
            this.linkText = '',
            this.linkUrl =  '',
            this.published =  true
        }
    },
    watch:{
        pageTitle(newTitle, oldTitle){
            if(this.linkText === oldTitle){
                this.linkText = newTitle;
            }
        }
    }
}</script>
