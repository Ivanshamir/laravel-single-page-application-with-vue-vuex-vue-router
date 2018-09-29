<template>
    <div class="customer-view" v-if="customer">
        <div class="user-img">
            <img src="https://picsum.photos/200/300" alt="lorem picsum">
        </div>
        <div class="user-info">
            <table class="table">
                <tr>
                    <td>ID</td>
                    <td>{{ customer.id }}</td>
                </tr>
                <tr>
                    <td>Name</td>
                    <td>{{ customer.name }}</td>
                </tr>
                <tr>
                    <td>Email</td>
                    <td>{{ customer.email }}</td>
                </tr>
                <tr>
                    <td>Phone</td>
                    <td>{{ customer.phone }}</td>
                </tr>
                <tr>
                    <td>Website</td>
                    <td>{{ customer.website }}</td>
                </tr>

            </table>
            <router-link to="/customers">Go Back To All Customers</router-link>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'View',
        created(){
            if(this.customers.length){
                this.customer = this.customers.find((customer) => customer.id == this.$route.params.id);
            }else{
                axios.get(`/api/customers/${this.$route.params.id}`)
                    .then((response) => {
                        this.customer = response.data.customer
                    })
            }

        },
        data(){
            return{
                customer: null
            };
        },
        computed:{
            currentUser(){
                return this.$store.getters.currentUser;
            },
            customers(){
                return this.$store.getters.customers;
            }
        }
    }
</script>

<style scoped>
    .customer-view {
        display: flex;
        align-items: center;
    }
    .user-img {
        flex: 1;
    }
    .user-img img{
        max-width: 160px;
    }
    .user-info{
        flex: 3;
        overflow-x: scroll;
    }
</style>