<template>
  <view-wrapper>
    <mdb-mask class="d-flex gradient justify-content-center align-items-center">
        <mdb-container>
            <mdb-row>
                <mdb-col md="6" xl="5" class="mb-4 form"> 
                <!-- Card -->
                <mdb-card>
                    <mdb-card-body>
                    <mdb-modal-header class="text-center">
                        <mdb-modal-title tag="h4" class="w-100 font-weight-bold">Sign Up</mdb-modal-title>
                    </mdb-modal-header>
                    <mdb-modal-body class="mx-3 grey-text">
                        <div v-if="!successful">
                        <mdb-input
                            label="Username"
                            type="text"
                            name="username"
                            class="mb-5"
                            icon="user"
                            v-model="user.username"
                            v-validate="'required|min:3|max:20'"
                        />
                        <mdb-input
                            label="Email"
                            type="email"
                            name="email"
                            class="mb-5"
                            icon="envelope"
                            v-model="user.email"
                            v-validate="'required|email|max:50'"
                        />
                        <mdb-input
                            label="Password"
                            type="password"
                            name="password"
                            class="mb-5"
                            icon="lock"
                            v-model="user.password"
                            v-validate="'required|min:6|max:40'"
                        />
                        </div>
                    </mdb-modal-body>
                    <mdb-modal-footer center>
                        <mdb-btn @click.native="handleRegister" color="indigo">Send <mdb-icon icon="sign-in-alt" class="ml-1"/></mdb-btn>
                    </mdb-modal-footer>
                    </mdb-card-body>
                </mdb-card>
                <!--/.Card -->
                </mdb-col>
            </mdb-row>
            <mdb-row>
                 <mdb-col md="6" xl="5" class="mb-4 form">
                    <div
                    v-if="message"
                    class="alert"
                    :class="successful ? 'alert-success' : 'alert-danger'"
                    >{{message}}</div>
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
} from 'mdbvue';

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
            user: new User('', '', ''),
            register: false,
            successful: false,
            message: ''
        };
    },
    computed: {
        loggedIn() {
            return this.$store.state.auth.status.loggedIn;
        }
    },
    mounted() {
        if (this.loggedIn) {
            this.$router.push('/profile');
        }
    },
    methods: {
        handleRegister() {
             this.message = '';
             this.$validator.validate().then(isValid => {
                if (isValid) {
                    this.$store.dispatch('auth/register', this.user).then(
                        data => {
                            this.message = data.message;
                            this.successful = true;
                        },
                        error => {
                            this.message =
                                (error.response && error.response.data) ||
                                error.message ||
                                error.toString();
                                this.successful = false;
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