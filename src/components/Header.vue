<template>
<div>
  <div class="progress regis_progress">
    <div class="progress-bar" role="progressbar" :style="{width : currentPage*100/totalPage + '%'}" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100"></div>
  </div>
  <div class="shadow mt-3 mb-5 bg-body rounded regis_stage">
    <div class="p-3 d-flex justify-content-between" >
      <div class="bg-light p-3 col-3 rounded" v-for="(st,index) in listStep" :key="index" :class="{'border border-primary' : st.status}"> <span class="span1 rounded-circle"> {{st.stepPage}} </span> <span class="span2">{{st.text}}</span></div>
     </div>

  </div>
</div>
</template>

<script>
export default {
  props: {
    currentPage : {
      type : Number,
      default : () => {
        return 0
      },
  },
    totalPage : {
      type : Number,
      default : () => {
        return 0
      }
    },
    listStep : {
      type : Array,
      default : () => {
        return []
      }
    }
}}
</script>

<style scoped>
.regis_progress{

}
.span1{
  background-color: #6a7176;
  color: #ffffff;
  padding: 10px;
  /*border-radius: 100%;*/
}
.span2{
  padding: 10px;
}
</style>
