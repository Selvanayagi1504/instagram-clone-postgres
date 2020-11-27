<template>
    <div class="request">
        <div class="nav-upload">
            <div class="row" style="margin-top: 7px;margin-bottom: 5px;">
                <div class="col-sm-4">
                    <img :src="require('./images/instagram-name.png')" class="img-insta" />
                </div>
                <div class="col-sm-4">
                    <!-- <input type="text" placeholder="&#xF002;Search" class="search-bar"/> -->
                    <center>
                        <div class="form-group has-search">
                            <span class="fa fa-search form-control-feedback"></span>
                            <input type="text" class="form-control search-bar" placeholder="Search">
                        </div>
                    </center>
                </div>
                <div class="col-sm-4 icon-arrange" v-bind:key="pro">
                    <img :src="require('./images/home-icon.png')" class="icon-side" />
                    <img :src="require('./images/save.png')" class="icon-side" />
                    <img :src="require('./images/discover.png')" class="icon-side" />
                    <router-link to="/request">
                        <img :src="require('./images/activity.png')" class="icon-side" />
                    </router-link>
                    <router-link to="/profile">
                        <img :src="`${pro}`" class="user-profile-img" />
                    </router-link>
                    &nbsp;&nbsp;
                    <router-link to="/movieapp">
                        <img :src="require('./images/movie.png')" style="width: 7%;border-radius: 16px;"
                            class="icon-side" />
                    </router-link>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    name:'request',
    props:{
        msg:String
    },
    data(){
        return{
            pro:""
        }
    },
    mounted(){
        let email=sessionStorage.getItem("email")
            fetch("https://secret-ridge-70355.herokuapp.com/api/user/getuser/" + email)
            .then(response => response.json())
            .then(user => {
                this.pro = user.profile
            });
    },
    methods:{

    }
}
</script>

<style scoped>

.request{
        background-color: rgba(var(--b3f, 250, 250, 250), 1) !important;
        overflow-x: hidden;
    }
    .nav-upload {
        background-color: white;
        border: 1px solid rgba(var(--ca6, 219, 219, 219), 1);
    }

    .img-insta {
        width: 27%;
    }

    .icon-arrange {
        margin-left: -3%;
        margin-top: 0.5%;
    }

    .icon-side {
        width: 6%;
        margin-right: 3%;
    }

    .user-profile-img {
        width: 25px;
        height: 25px;
        object-fit: cover;
        border-radius: 50%;
        margin-right: 3%;
    }

    .has-search .form-control {
        padding-left: 2.375rem;
    }

    .has-search .form-control-feedback {
        position: absolute;
        z-index: 2;
        display: block;
        width: 2.375rem;
        height: 2.375rem;
        line-height: 1.7em;
        text-align: center;
        pointer-events: none;
        color: #aaa;
        margin-left: 38%;
    }

    .form-control:focus {
        background-color: rgba(var(--b3f, 250, 250, 250), 1);
        border: 1px solid rgba(var(--ca6, 219, 219, 219), 1);
        outline: none;
        box-shadow: none;
    }

    .search-bar {
        text-align: center;
        background-color: rgba(var(--b3f, 250, 250, 250), 1);
        border: 1px solid rgba(var(--ca6, 219, 219, 219), 1);
        border-radius: 2px;
        font-family: 'Helvetica', FontAwesome, sans-serif;
        width: 53%;
        font-size: 12px;
        height: 74%;
        margin-top: 1%;
    }

</style>