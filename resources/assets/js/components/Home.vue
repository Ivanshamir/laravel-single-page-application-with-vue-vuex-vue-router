<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card card-default">
                    <div class="card-header">Vue.JS SPA Example</div>

                    <div class="card-body">
                        <h2>{{welcome}}</h2>
                        <img src="https://picsum.photos/200/300" alt="lorem picsum">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        name:'home',
        computed:{
            welcome(){
                return this.$store.getters.welcome
            }
        },
        created(){
            axios.defaults.headers.common["Authorization"] = 'Bearer ' + this.$store.getters.currentUser.token;
        }
    }
</script>