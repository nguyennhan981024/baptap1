<template>
  <div class="shadow p-3 mb-5 bg-white rounded">
    <ValidationObserver ref="observer" v-slot="{ handleSubmit }" v-for="(step,index) in listStep" :key="index">

      <form @submit.prevent="handleSubmit(step.stepPage === totalPage ? finishProcess : nextProcess)" v-if="step.stepPage === currentPage">
        <ValidationProvider  v-slot="{ errors, classes }" v-for="(content,index) in step.form" :key="index" :name="content.name"  :rules="content.rule">
          <div class="form-group" :class="{'form-check' : isCheckBox(content.type)}">
            <label v-if="!isCheckBox(content.type)" class="text-left d-flex">{{content.name}}</label>
            <input v-if="!isSelect(content.type)" :type="content.type" :class="{'form-check-input' : isCheckBox(content.type),'form-control' : !isCheckBox(content.type)}" v-model="content.model">
            <label v-if="isCheckBox(content.type)" class="form-check-label">
              Default checkbox
            </label>
            <select v-if="isSelect(content.type)" :type="content.type" class="form-control"  v-model="content.model">
              <option value="Friend facebook">Friend facebook</option>
              <option value="Google">Friend facebook</option>
            </select>
            <span :class="classes" class="styleSpan">{{ errors[0] }}</span>

          </div>
        </ValidationProvider>

        <button class="btn btn-info" type="button" v-if="currentPage < totalPage " @click="prevProcess">PREVIOUS</button>
        <button class="btn btn-primary ml-2" type="submit" v-if="currentPage < totalPage">NEXT</button>
        <button class="btn btn-danger ml-2" type="button" @click="reset" v-if="currentPage === totalPage">RESET</button>
        <button class="btn btn-success" type="submit" v-if="currentPage === totalPage ">Finish</button>
      </form>
    </ValidationObserver>
  </div>
</template>

<script>
export default {
  data(){
    return {
      newData : {
        name: '',
        email: '',
        companyname: '',
        numberofemployee: '',
        select: '',
        checkbox: false,
      }
    }
  },
  props : {
    currentPage : Number,
    prevProcess :{
      type : Function,
      default : () => {
        return []
      }
    },
    nextProcess: {
      type : Function,
      default : () => {
        return []
      }
    },
    resetProcess : {
      type : Function,
      default : () => {
        return []
      }
    },
    finishProcess : {
      type : Function,
      default : () => {
        return []
      }
    },
    totalPage : {
      type : Number,
      default : () => {
        return '';
      }
    },
    listStep : {
      type : Array,
      default : () => {
        return []
      }
    }
  },
  methods : {
    reset(){
      this.resetProcess()
    },
    isCheckBox(item){
      if(item === 'checkbox')
        return true;
      return false;
    },
    isSelect(item){
      if(item === 'select')
        return true;
      return false;
    }

  }
}
</script>

<style scoped>
.styleSpan{
  color: red;
  padding: 5px;
  margin-top: 5px;
  text-align: left;
}
</style>
