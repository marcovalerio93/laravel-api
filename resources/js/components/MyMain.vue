<template>
    <div class=container>
        <h1 class="my-4">Bacheca</h1>

        <div v-if="loading" class="d-flex justify-content-center">

            <div class="spinner-border text-primary" role="status">
                <span class="sr-only">Loading...</span>
            </div>

        </div>

        <div v-else class="row">
            <div v-for="(post, index) in posts" :key="index" class="card col-12 mb-4" style="width: 18rem;">
                <div class="card-body">
                    <h5 class="card-title">{{post.title}}</h5>
                    <p class="card-text">{{cutText(post.content, 150)}}</p>
                    <p class="card-text">{{post.category?post.category.name:'-'}}</p>
                    <a href="#" class="btn btn-primary">Read more...</a>
                </div>
            </div> 
        </div>

        <nav aria-label="...">
        <ul class="pagination">
            <li class="page-item" :class="(currentPage==1?'disabled':'')" >
                <a class="page-link" href="#" @click="getPosts(currentPage - 1)" >Previous</a>
            </li>
            <li class="page-item disable">
                <span class="page-link" href="#">{{currentPage}}/{{lastPage}}</span>
            </li>
            <li class="page-item" :class="(currentPage==lastPage?'disabled':'')">
                <a class="page-link" href="#" @click="getPosts(currentPage + 1)" >Next</a>
            </li>
        </ul>
        </nav>

    </div>
    
</template>

<script>
export default {
    name: 'MyMain',
    data() {
        return{
            posts:[ ],
            currentPage: 1, 
            lastPage: null,
            loading: true
        }

    },
    methods:{
        getPosts(page) {

            this.loading = true;
            
            axios.get('/api/post',{
                params:{
                    page: page
                }
            })
            .then((response) =>{
                this.posts = response.data.results.data;
                this.loading = false;
                this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
            });
        },

        //accorciare il testo 
        cutText(text, maxLength){
            if (text.length < maxLength){
            return text;
            } else {
            return text.substring(0, maxLength) + '...';
            }
        }
    },
    mounted(){ 
        this.getPosts();
    }
}
</script>

<style>

</style>