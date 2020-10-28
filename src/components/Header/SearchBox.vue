<template>
    <div>
        <div>
            <span v-if="isUserLoggedIn">Welcome <b>{{userName}} </b>({{role}}) </span><a v-if="isUserLoggedIn" href="#" v-on:click="logout">Logout</a>
        </div>
    </div>
</template>

<script>
    import jwt_decode from "jwt-decode";
    import roles from "../../router/roles";
    export default {
        data() {
            return {
                searchOpen: false,
                userName:'',
                role:'',
                token:null,
                roleDisplayName : [{role: roles.TsspAdmin, displayName:"Admin"},{role: roles.TsspIntermediate, displayName:"Intermediate Role"},{role: roles.TsspWarehouseIncharge, displayName:"Warehouse Incharge"}, 
                {role:roles.TpsafAdmin, displayName:"Admin"},{role:roles.TpsafFacilityAdmin, displayName:"Facility Admin"},{role:roles.TpsafFacilityIncharge, displayName:"Facility Incharge"},
                {role:roles.TaxAuthAdmin, displayName:"Admin"},{role:roles.TaxAuthRevenueOfficer, displayName:"Revenue Officer"},
                {role:roles.MfAdmin, displayName:"Admin"},{role:roles.MfAccountManager, displayName:"Account Manager"},{role:roles.MfWarehouseIncharge, displayName:"Warehouse Incharge"},
                {role:roles.PrintPartner, displayName:"Print Partner"}]
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
            this.role = this.getRoleDisplayName(decodedToken.Role);
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
                
            },
            getRoleDisplayName: function(role){
                return this.roleDisplayName.find(x=>x.role == role).displayName;
            }
            
        }
    }
</script>

