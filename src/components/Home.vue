<template>
  <div class="flexible-content">
    <!--ViewWrapper-->
    <view-wrapper>
      <mdb-mask overlay="black-light" color="#78909c" class="d-flex gradient justify-content-center align-items-center">
        <mdb-container>
        <mdb-row class="mt-5 pt-5">
          <mdb-col md="12" class="text-center">
            <h1 class="h1-reponsive white-text">
              <strong>Minimalist Design</strong>
            </h1>
            <h5 class="mb-5 white-text"><strong>Azka Hanifah</strong></h5>
          </mdb-col>
        </mdb-row>
        </mdb-container>
      </mdb-mask>
    </view-wrapper>
    <!--/.ViewWrapper-->
  </div>
</template>

<script>
    import {
        mdbContainer,
        mdbRow,
        mdbCol,
        mdbMask,
        ViewWrapper
    } from "mdbvue";

    export default {
        name: 'Home',
        components: {
            mdbContainer,
            mdbRow,
            mdbCol,
            mdbMask,
            ViewWrapper
        }
    }
</script>

<style lang="scss">
$image-path: '~@/../mdb/mdbvue/img';
@import '~@/../mdb/mdbvue/scss/mdb-free.scss';

@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap');
</style>

<style scoped>
.flexible-content {
  transition: padding-left 0.3s;
  padding-right: 0px;
}

.gradient {
  background-image: url('https://images.pexels.com/photos/1166209/pexels-photo-1166209.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  height: calc(109vh - 70px);
}
</style>