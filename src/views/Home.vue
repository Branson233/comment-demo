<template>
  <div class="home">
    <h5>Show HN: 10 KB Club: With links to popular HN, Reddit threads for each website</h5>
    <textarea rows="10" cols="30" placeholder="comment something" v-model="mes">
    </textarea>
    <div class="commnent-button">
      <button @click="add">add comment</button>
    </div>
    <div class="comment-list">
      <comment :message="message"></comment>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Comment from '../views/Comment'
export default {
  name: 'Home',
  components: {
    Comment
  },
  data () {
    return {
      mes: '',
      meslist: [],
      addflag: false,
      message: [],
      items: {
        msg: '',
        reply: ''
      }
    }
  },
  methods: {
    add () {
      if (this.mes) {
        if (localStorage.getItem('mes-list')) {
          this.meslist = JSON.parse(localStorage.getItem('mes-list'))
        }
        this.items.msg = this.mes
        this.meslist.push(this.items)
        localStorage.setItem('mes-list', JSON.stringify(this.meslist))
        this.addflag = true
        this.message = JSON.parse(localStorage.getItem('mes-list'))
      }
    }
  },
  mounted () {
      this.message = JSON.parse(localStorage.getItem('mes-list'))
  }
}
</script>

<style scoped>
  .commnent-button {
    width: 100px;
    height: 25px;
    margin:auto auto;
  }

</style>
