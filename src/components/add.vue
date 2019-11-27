<template>
  <div style="padding-left: 10px; padding-right: 10px">
    <h1>青年教师基本功比赛</h1>
    <textarea v-if="maxlength" style="width:100%; border:solid 1px #d8d8d8; border-radius:3px; font-size:14px; padding:10px;" rows="3" @input="descInput" v-model="desc" ></textarea>
    <textarea readonly v-if="!maxlength" style="width:100%; border:solid 1px #d8d8d8; border-radius:3px; font-size:14px; padding:10px;" rows="3" @input="descInput" v-model="desc" ></textarea>
    <h3 class="pay-service-textarea-text">当前您已经输入 <span style="color: rgba(255,0,0,0.64)">{{remnant}}</span> 字符</h3>
    <Button type="primary" @click="handleSubmit()"> 提 交 </Button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'add',
  data () {
    return {
      remnant: 0,
      desc: '',
      maxlength: true
    }
  },
  methods: {
    descInput () {
      let cnReg = /([\u4e00-\u9fa5]|[\u3000-\u303F]|[\uFF00-\uFF60]|[A-Za-z])/g
      let mat = this.desc.match(cnReg)
      var txtVal
      if (mat) {
        txtVal = mat.length
      } else {
        txtVal = 0
      }
      this.remnant = txtVal
      if (this.remnant === 500) {
        this.maxlength = false
      }
    },
    handleSubmit () {
      var name = 'user'
      var desc = this.desc
      axios.post('http://localhost:5000/add', {'name': name, 'text': desc}).then(({data}) => {
        this.desc = ''
        this.maxlength = true
      })
    }
  }
}
</script>
