<template>
    <view-wrapper>
    <mdb-mask class="d-flex gradient justify-content-center align-items-center"></mdb-mask>
    </view-wrapper>
  
</template>

<script>
import {
  mdbMask,
  ViewWrapper
} from 'mdbvue';

export default {
    name: 'Profile',
    components: {
      mdbMask,
      ViewWrapper
    },
    computed: {
        currentUser() {
            return this.$store.state.auth.user;
        }
    },
    mounted() {
        if (!this.currentUser) {
            this.$router.push('/login');
        }
    }
}
</script>

<style scoped>
.gradient {
  background-color: plum;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  height: calc(109vh - 70px);
}
</style>