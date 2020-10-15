<template>
    <div>
        <div class="search-wrapper" v-bind:class="{ active: searchOpen }">
            <div class="input-holder">
                <input type="text" class="search-input" placeholder="Type to search"/>
                <button class="search-icon" v-on:click="searchOpen = !searchOpen"><span/></button>
            </div>
            <button class="close" v-on:click="searchOpen = !searchOpen"/>
        </div>
        <div>
            <a v-if="isUserLoggedIn" href="#" v-on:click="logout">Logout</a>
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
                if(process.env.NODE_ENV==="development")
                    return this.$root.user !=='' && this.$root.user !==null;
                return this.$root.access_token!=='' &&  this.$root.access_token!==null  
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

