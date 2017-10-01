<template>
    <div id="widget-user-github" v-bind:style="{ width: width }">
        <header>
            <a :href="dataUser.url">
                <img id="user-image" :src="dataUser.avatar_url" alt="">
            </a>
            <div id="about-user">
                <strong id="user-name">{{ dataUser.name }}</strong>
                <span id="user-desc">{{ dataUser.bio }}</span>
            </div>
        </header>
        <ul >
            <li v-for="repo in repos">
                <a :href="repo.html_url" target="__blank">
                    {{ repo.name }}
                </a>
                <span id="box-star">
                    <span class="star-number">
                        {{ repo.stargazers_count }}
                    </span>
                    <svg aria-hidden="true" class="star" height="16" version="1.1" viewBox="0 0 14 16" width="14">
                        <path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"></path>
                    </svg>
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
    const api = axios.create({
        baseURL: 'https://api.github.com/users'
    });

    import axios from 'axios'
    export default {
        props: ["width", 'user'],
        data(){
            return{
                dataUser: {},
                repos: {},
            }
        },
        mounted(){
            this.getUser(this.user)
            this.getRepos(this.user)
        },
        methods: {
            getUser(user){
                api.get(`/${user}`)
                .then((response) => {
                    this.dataUser = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
            },
            getRepos(user){
                api.get(`/${user}/repos`)
                .then((response) => {
                    this.repos = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
            }
        }
    }
</script>
<style>
    #widget-user-github{
        min-width: 15em;
        min-height: 20em;
        background-color: #353535;
        overflow: auto;
        margin: 0;
        max-height: 33em;
        box-shadow: 0 18px 35px rgba(50,50,93,.1), 0 8px 15px rgba(0,0,0,.07);
    }
    #widget-user-github header{
        clear: both;
        align-items: center;
        padding: 10px 0px 10px 0px;
        justify-content: center;
    }    
    #about-user{
        display: flex;
        padding: 10px 0px 0px;
        flex-wrap: wrap;
        color: white;
    }
    #user-image{
        width: 5em;
        height: 5em;
        border-radius: 100px;
    }
    #user-image:hover{
        transition: 0.3s;
        transform: translateY(-3px);
        box-shadow: 0 7px 14px rgba(50,50,93,.1), 0 3px 6px rgba(0,0,0,.08);
        transition-timing-function: ease-in;
    }
    #user-name{
        flex-basis: 100%;
        color: #42b983;
    }
    #user-desc{
        font-size: 10px;
        flex-basis: 100%;
        color: #b9c1be;
        font-size: 12px;
    }
    ul{
        background-color: #232323;
        margin: 0;
        padding: 15px;
    }
    #widget-user-github li{
        display: block;
        font-size: 14px;
        text-align: left;
        padding: 7px 10px;
        border-bottom: 1px solid #42b983;
    }
    #widget-user-github li:last-child{
        border-bottom: none;
    }
    #widget-user-github li a{
        text-decoration: none;
        color: #e0e0e0;
    }
    #box-star{
        float: right;
        color: white;
    }
    .star{
        fill: white;
        vertical-align: top;
        margin-top: -1px;
    }
    .star-number{
        margin-top:-2px;
    }
    body ::-webkit-scrollbar-track {
        background-color: #F5F5F5;
    }

    body ::-webkit-scrollbar{
        width: 7px;
        background-color: #F5F5F5;
    }

    body ::-webkit-scrollbar-thumb{
        background-color: #555;
    }
</style>