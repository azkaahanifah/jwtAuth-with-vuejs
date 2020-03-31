<template>
  <view-wrapper>
    <mdb-mask class="d-flex gradient justify-content-center align-items-center">
        <mdb-container>
            <mdb-row >
                <mdb-col md="6" xl="5" class="mb-4 form">
                <!-- Card -->
                <mdb-card>
                    <mdb-card-body>
                        <mdb-modal-header class="text-center">
                            <mdb-modal-title tag="h4" class="w-100 font-weight-bold">Login</mdb-modal-title>
                        </mdb-modal-header>
                    <mdb-modal-body class="mx-3 grey-text">
                        <mdb-input
                            label="Username"
                            type="text"
                            name="username"
                            class="mb-5"
                            icon="user"
                            v-model="user.username"
                            v-validate="'required'"
                        />    
                        <mdb-input
                            label="Password"
                            type="password"
                            name="password"
                            class="mb-5"
                            icon="lock"
                            v-model="user.password"
                            v-validate="'required'"
                        />
                    </mdb-modal-body>
                    <mdb-modal-footer center>
                        <mdb-btn @click.native="handleLogin" color="indigo">Send <mdb-icon icon="sign-in-alt" class="ml-1"/></mdb-btn>
                    </mdb-modal-footer>
                    </mdb-card-body>
                </mdb-card>
                <!--/.Card -->
                </mdb-col>
            </mdb-row>
        </mdb-container>
    </mdb-mask>
  </view-wrapper>
</template>

<script>
import User from '../model/user'

import {
    mdbContainer,
    mdbModalHeader,
    mdbModalTitle,
    mdbModalBody,
    mdbModalFooter,
    mdbInput,
    mdbCol,
    mdbRow,
    mdbMask,
    ViewWrapper,
    mdbCard, 
    mdbCardBody,
    mdbBtn 
} from "mdbvue";

export default {
    name: 'Login',
    components: {
        mdbContainer,
        mdbModalHeader,
        mdbModalTitle,
        mdbModalBody,
        mdbModalFooter,
        mdbInput,
        mdbCol,
        mdbRow,
        mdbMask,
        ViewWrapper,
        mdbCard, 
        mdbCardBody,
        mdbBtn 
    },
    data() {
        return {
            user: new User('', ''),
            loading: false
        };
    },
    computed: {
        loggedIn() {
            return this.$store.state.auth.status.loggedIn;
    }},
    created() {
        if (this.loggedIn) {
            this.$router.push('/profile');
    }},
    methods: {
        handleLogin() {
            this.$validator.validateAll().then(isValid => {
                if (!isValid) {
                    this.loading = false;
                    return;
                }

                if (this.user.username && this.user.password) {
                    this.$store.dispatch('auth/login', this.user).then(
                        () => {
                            this.$router.push('/profile');
                        },
                        error => {
                            this.loading = false;
                            this.message = 
                                (error.response && error.response.data) ||
                                error.message ||
                                error.toString();
                        }
                    );
                }
            });
        }
    }
}   
</script>

<style lang="scss">
$image-path: '~@/../mdb/mdbvue/img';
@import '~@/../mdb/mdbvue/scss/mdb-free.scss';

@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap');
</style>

<style scoped>
.gradient {
  background-image: url('https://images.pexels.com/photos/917494/pexels-photo-917494.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  height: calc(109vh - 70px);
}

.form {
  max-width: 500px;
  margin: 0 auto;
}
</style>