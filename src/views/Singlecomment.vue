<template>
    <div class="single">
        <div class="des">
            <span class="comment-title">comment:</span>
            <a href="javascript:;" @click = "showreply" class="reply"> reply</a>
            <a href="javascript:;" @click="controlshow" class="show">{{ifshow}}</a>
        </div>
        <div v-show="showflag" class="msg">
            {{item.msg}}
            <div v-if="item.reply" class="rep">reply:
                {{storereply}}
            </div>
        </div>
        <div class="reply-view" v-show = "replyflag">
            <textarea rows="10" cols="30" placeholder="comment something" v-model="rep">
            </textarea>
            <div class="reply-button">
                <button @click="handle" >add reply</button>
            </div>    
        </div>
    </div>
</template>
  
<script>
  export default {
    name: 'Singlecomment',
    props: {
        item: Object,
        index: Number
    },
    data () {
        return {
            ifshow: 'hide',
            showflag: true,
            rep: '',
            replyflag: false,
            meslist2: '',
            storereply: '' 
        }
    },
    methods: {
        controlshow () {
            this.showflag = !this.showflag
            if (this.showflag) {
                this.ifshow = 'hide'
            } else {
                this.ifshow = 'show'
            }
        },
        showreply () {
            this.replyflag = true
        },
        handle () {
            if (this.rep) {
                this.meslist2 = JSON.parse(localStorage.getItem('mes-list'))
                this.meslist2[this.index].reply = this.rep
                localStorage.setItem('mes-list', JSON.stringify(this.meslist2))
                this.storereply = JSON.parse(localStorage.getItem('mes-list'))[this.index].reply
                this.replyflag = false
            }
        }
    },
    watch: {
        replyflag (n, o) {
            this.storereply = JSON.parse(localStorage.getItem('mes-list'))[this.index].reply
        }
    },
    mounted () {
        this.storereply = JSON.parse(localStorage.getItem('mes-list'))[this.index].reply
    }
}
</script>

<style scoped>
    .single{
        margin-bottom: 15px;
        position: relative;
    }
    .comment-title{
        float:left;
    }
    .reply {
        margin-left: 50px;
    }
    .show{
        float:right;
        
    }
    .msg{
        padding-top: 5px;
        float: left;
    }
    .rep{
        padding-top: 5px;
    }
    .reply-view {
        z-index: 99;
        position: fixed;
        top:0;
        left: 0;
        bottom:0;
        right:0;
        background-color: white;
    }
    .reply-button {
        width: 100px;
        height: 25px;
        margin:auto auto;
    }
</style>
