<template>
<div id="background" class="page-holder bg-cover">
    <div id="rectangle">
        <b-container id="login" class='mt-n4'>
            <router-link id="change" to="/">Back</router-link>
        <div id="box" class="shadow-lg p-3 mb-5 bg-grey rounded">
            <div>
                <img id="namecard" src="/assets/namecard.png" fluid />
            </div>
            <br>
        <!-- Default form login -->
            <form>
                <p id="member" class="h4 text-center mb-4"> MEMBER LOGIN </p>
                <b-form-input type="email" v-model.lazy='input.username' id="defaultFormLoginEmailEx" class="form-control" placeholder="Email"/>
                <br>
                <b-form-input type="password" v-model.lazy='input.password' id="defaultFormLoginPasswordEx" class="form-control" placeholder="Password"/>
                <br>
                <!-- <router-link to="/after"> -->
                    <div class="text-center mt-4">
                        <b-button id="login_btn" type="submit" v-on:click.prevent="login">Login</b-button>
                     </div>
                <!-- </router-link> -->
            </form>
        </div>
        </b-container>
    </div>
</div>
</template>

<script>
import firebase from "firebase"
export default {
    name: 'Login',
    data() {
        return {
            input: {
                username: "",
                password: ""
            },
            accounts: []
        }
    },
    methods: {
        login() {
            // return this.input.username + this.input.password;
            firebase.auth().signInWithEmailAndPassword(this.input.username, this.input.password)
            .then((user) => {
                alert('Well done! You are now connected.')
                console.log(user.user)
                this.$store.commit('setCurrentUser', user.user)
                this.$store.dispatch('fetchUserProfile')
                this.$router.replace('account')
            })
            .catch((error) => {
                alert('Oops. ' + error.message)
                console.log(error)
            })
        },
        
    },
    
}
</script>

<style scoped>
#background {
    position: absolute;
    background-image:url('/assets/login.jpeg');
    top: 0%;
}

.page-holder {
    min-height: 100vh;
    min-width: 100vw;
}

.bg-cover {
  background-size: cover !important;
  opacity: 0.8;
  z-index: -1;
}

#rectangle {
    position: absolute;
    background: rgba(23, 23, 23, 0.49);
    height: 100%;
    width: 100%;
}


#namecard {
    width: 20%;
    height: 20%;
    margin-left: 40%;
}

#member {
    font-size: 200%;
    color: #000000;
}

#login_btn {
    background-color:#84CEEB; 
    width:30%; 
    height:5%;
    font-family:'Futura Hv BT'; 
    color:#FFFFFF;
    position: center;
    font-size: 120%;
    position: relative;
    border: none;
    cursor: pointer;
}

#box {
    height: 30%;
    width: 60%;
    margin-top: 15%;
    margin-left: 20%;
    background-color: rgba(196, 196, 196, 0.7);
    box-shadow: 50px;
    color: #000000;
}

#back {
    color:#000000;
    text-decoration: underline;
    font-family: 'Futura Hv BT';
}

#change {
    font-family: Futura Hv BT;
    font-size: 130%;
    top: 5%;
    left: 5%;        
    color: #ffffff;
    position: absolute;
    text-decoration: underline;
}


</style>