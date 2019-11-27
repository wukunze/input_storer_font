<template>
    <Table :columns="columns1" :data="person"></Table>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      columns1: [{title: '用户', key: 'name', width: 60}, {title: '内容', key: 'text'}],
      person: this.personlist()
    }
  },
  methods: {
    personlist () {
      axios.post('http://172.25.46.97:5001/all').then(({data}) => {
        this.person = data
      })
    }
  }
}
</script>
