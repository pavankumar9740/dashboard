<template>
    <div>
        <div>
            <span v-if="this.$root.user != ''">Welcome <b>{{this.$root.user.profile.GivenName}} </b>({{this.$root.user.profile.Role}}) </span><a v-if="isUserLoggedIn" href="#" v-on:click="logout">Logout</a>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                searchOpen: false,
            }
        },
        computed:{
            isUserLoggedIn: function(){
                return process.env.NODE_ENV ==="development"? this.$root.user: this.$root.access_token!=null  
            }
        },
        methods:{
            logout: function(){
                if(process.env.NODE_ENV==="development")
                    this.$root.mgr.signoutRedirect();
                //this.$router.push('~/Account/Logout');
                else{
                this.$router.push('/')
                window.location.href= process.env.VUE_APP_Authority + '/Account/Logout'
                }
                
            }
            
        }
    }
</script>

