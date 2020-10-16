<template>
    <div>
        <div>
            <span v-if="isUserLoggedIn">Welcome <b>{{userName}} </b>({{role}}) </span><a v-if="isUserLoggedIn" href="#" v-on:click="logout">Logout</a>
        </div>
    </div>
</template>

<script>
    import jwt_decode from "jwt-decode";
    export default {
        data() {
            return {
                searchOpen: false,
                userName:'',
                role:'',
                token:null
            }
        },
        computed:{
            isUserLoggedIn: function(){
                return this.token!=null;
            }
        },
        created(){
            this.token= process.env.NODE_ENV === "development"
                    ? this.$root.user.access_token
                    : this.$root.access_token;
            var decodedToken = jwt_decode(this.token);
            console.log(decodedToken);
            this.userName = decodedToken.GivenName;
            this.role= decodedToken.Role;
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

