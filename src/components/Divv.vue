<template>
  <input type="checkbox" v-model="data" />{{ name }}<a @click="del()">刪除</a>
</template>

<script>
export default {
    name:"Divv",
    props:['name','data','id'],
    watch:{
      data:'onchange'
    },
    methods:{
      onchange(){
        this.$emit('updated',{
          id:this.id,
          data:this.data,
          event:"update"
        })
      },
      del(){
        this.$emit('updated',{
          id:this.id,
          event:"del"
        })
      }
    }
}
</script>