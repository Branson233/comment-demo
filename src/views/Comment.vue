<template>
    <div class="comet">
      <div v-for="(item,index) in ms" :key="index" class="container">
          <Singlecomment :item="item" :index="index" class="itemlist"></Singlecomment>
      </div>
    </div>
</template>
<script>
import Singlecomment from '../views/Singlecomment'
export default {
  name: 'Comment',
  props: {
    message: Array
  },
  components: {
    Singlecomment
  },
  data () {
    return {
      ms: []
    }
  },
  watch: {
    message (n, o) {
      this.ms = n
    }
  },
  mounted () {
    this.ms = this.message
  },
  methods: {
    controlshow () {
      this.showflag = !this.showflag
      if (this.showflag) {
        this.ifshow = 'hide'
      } else {
        this.ifshow = 'show'
      }
    }
  }
}

</script>

<style scoped>
  .comet{
    position: relative;
    margin-left: 40px;
    margin-right: 40px;
  }
  .container{
    overflow: hidden;
  }
  .itemlist{
    margin-top:30px;
  }
</style>
