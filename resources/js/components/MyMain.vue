<template>
    <div class=container>
        <h1 class="my-4">Bacheca</h1>
        <div class="row">
            <div v-for="(post, index) in posts" :key="index" class="card col-12 mb-4" style="width: 18rem;">
                <div class="card-body">
                    <h5 class="card-title">{{post.title}}</h5>
                    <p class="card-text">{{post.content}}</p>
                    <p class="card-text">{{post.category?post.category.name:'-'}}</p>
                    <a href="#" class="btn btn-primary">Read more...</a>
                </div>
            </div> 
        </div>

    </div>
    
</template>

<script>
export default {
    name: 'MyMain',
    data() {
        return{
            posts:[ ]
        }

    },
    methods:{
        getPosts() {
            axios.get('/api/post')
            .then((response) =>{
                this.posts = response.data.results;
            });
        }
    },
    mounted(){
        this.getPosts();
    }
}
</script>

<style>

</style>