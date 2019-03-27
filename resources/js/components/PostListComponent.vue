<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">posts</div>

                    <div class="card-body">
                        <li v-for="post in posts">{{post.title}}</li>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                posts:[]
            }
        },
        mounted() {
           axios.get('api/posts')
            .then(response=>this.posts=response.data);
        }
    }
</script>
