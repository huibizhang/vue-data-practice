<template>
  要做的事
  <ul>
    <li v-for="a in filterData().incompelete" :key="a.id">
      <Divv v-bind="a" @updated="dataUpdate($event)" />
      {{ a.data }}
    </li>
  </ul>
  <br />
  做完的事
  <ul>
    <li v-for="a in filterData().compeleted" :key="a.id">
      <Divv v-bind="a" @updated="dataUpdate($event)" />
      {{ a.data }}
    </li>
  </ul>
  <Msg v-for="msg in msgs" v-bind="msg" :key="msg.id" />
  <!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Divv from "./components/Divv.vue";
import Msg from "./components/Msg.vue";

export default {
  data() {
    return {
      a1: [],
      unsave: false,
      msgs:[]
    };
  },
  mounted() {
    for (var i = 0; i < 3; i++) {
      this.a1.push({
        name: `data${i + 1}`,
        id: this.hashGenerator(5),
        data: false,
      });
    }
    for (var i = 0; i < 35; i++) {
      this.msgs.push({
        id: this.hashGenerator(16),
        text: this.hashGenerator(16),
        self: i%3===0,
      });
    }
  },
  methods: {
    hashGenerator(digit) {
      const pattern =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
      let output = "";
      for (let i = 0; i < digit; i++) {
        output += pattern.charAt(Math.random() * pattern.length);
      }
      return output;
    },
    dataUpdate(newData) {
      const origin = this.a1;

      if (newData.event === "update") {

        origin.forEach((a, index) => {
          if (a.id === newData.id) {
            a.data = newData.data;
          }
        });

        // 本地 localStorage

        // 遠端 axios ... ajax ...
      } else if (newData.event === "del") {

        const d = origin.filter((a)=>{
          return a.id == newData.id
        })
        const index = origin.indexOf(d[0])
        origin.splice(index, 1);
      }
    },

    filterData(){
      return {
        incompelete:this.a1.filter((a)=>{
          return a.data === false
        }),
        compeleted:this.a1.filter((a)=>{
          return a.data === true
        })
      }
    }
  },
  components: {
    Divv,Msg,
  },
};
</script>
