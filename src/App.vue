<template>
    <div class="container content">
      <Header
        class="mt-3"
        :currentPage="currentPage"
        :totalPage="totalPage"
        :listStep="listStep"/>
      <Body
        :currentPage="currentPage"
        :next-process="nextProcess"
        :totalPage="totalPage"
        :prev-process="prevProcess"
        :reset-process="resetProcess"
        :finish-process="finishProcess"
        :listStep="listStep"
      />
    </div>
</template>
<script>


import Header from "./components/Header";
import Body from "./components/Body";
export default {
  components: {Header,Body},
  data(){
    return {
      currentPage : 1,
      progress: 0,
      listStep : [
        {
        stepPage : 1,
        status : true,
        text : 'about you',
        form :[
          {
            model: '',
            name: 'name',
            type: 'text',
            rule:
                'required'
          },
          {
            model: '',
            name: 'email',
            type: 'text',
            rule:
              'required|email',
          }
        ]
      },
        {
          stepPage : 2,
          status : false,
          text : 'about your company',
          form :[
            {
              model: '',
              name: 'companyname',
              type: 'text',
              rule:
                'required',
            },
            {
              model: '',
              name: 'numberofemployee',
              type : 'text',
              rule:
                'required|numeric',
            }
          ]
        },
        {

          stepPage : 3,
          status : false,
          text : 'finishing up',
          form :[
            {

              model: '',
              name: 'select option',
              type: 'select',
              rule:
                'required',
            },
            {
              model: '',
              name: 'checkbox option',
              type : 'checkbox',
              rule:
                'required',
            }
          ]
        }

      ],
    }
  },
  computed: {
    totalPage(){
      return this.listStep.length;
    }
  },
  methods:{
    nextProcess(){
      if(this.currentPage === this.totalPage){
        this.currentPage = this.totalPage;
      }
      if(this.currentPage <3){
        this.currentPage ++;
      }
      this.listStep[this.currentPage-1].status= true;
    },
    prevProcess(){
      if(this.currentPage === 1){
        this.currentPage = 1;
      }
      if(this.currentPage >1){
        this.currentPage--;
        this.listStep[this.currentPage].status = false;
      }
    },
    resetProcess(){
      this.currentPage = 1
      this.listStep = [...this.listStep].map(item => {
        if(item.stepPage !== this.currentPage){
          item.status = false;
        }
        return item
      })
      this.listStep.forEach(item=>{
        item.form.forEach(i => {
          i.model = ''
        })
      })
    },
    finishProcess(){
      alert('The form submit successfully')
    }
  },

}
</script>

<style>
.content {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #a3aaaf;
  margin-top: 60px;
  text-transform: capitalize;
}
</style>
