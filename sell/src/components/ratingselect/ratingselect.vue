<template>
  <div class="ratingselect">
    <div class="rating-type border-1px">
      <span @click='select(2,$event)' class="block positive" :class="{'active':selectType===2}">{{desc.all}}<span class="count">{{ratings.length}}</span></span>
      <span @click='select(0,$event)' class="block positive" :class="{'active':selectType===0}">{{desc.positive}}<span class="count">{{positives.length}}</span></span>
      <span @click='select(1,$event)' class='block negative' :class="{'active':selectType===1}">{{desc.negative}}<span class="count">{{negatives.length}}</span></span>
    </div>
    <div @click='toggleContent' class="switch" :class="{'on':onlyContent}">
      <span class="icon-check_circle"></span>
      <span class='text'>只看内容评价</span> 
    </div>
  </div>
</template>

<script>
const POSITIVE = 0;
const NEGATIVE = 1;
const ALL = 2;
export default {
  props:{
    ratings:{
      type:Array,
      //数组和对象都要返回函数
      default(){
        return[];
      }
    },
    selectType:{
      type:Number,
      default:ALL
    },
    onlyContent:{
      type:Boolean,
      default:false
    },
    desc:{
      type:Object,
      default(){
        return{
          all:'全部',
          positive:'满意',
          negative:'不满意'
        }
      }
    }
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods:{
    select(type,event){
      if(!event._constructed){
        return
      }
       this.$emit('select', type);
    },
    toggleContent(event){
       if(!event._constructed){
        return
      }
     this.$emit('toggle');
    }
  },
  computed:{
    positives() {
        return this.ratings.filter((rating) => {
          return rating.rateType === POSITIVE;
        });
      },
      negatives() {
        return this.ratings.filter((rating) => {
          return rating.rateType === NEGATIVE;
        });
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus">
  // @import '../../common/stylus/mixin.style'
  @import '../../common/stylus/mixin';
  .ratingselect
    .rating-type
      padding:18px 0
      margin: 0 18px
      border-1px(rgba(7,17,27,0.1))
      // border-1px(red)
      font-size:0
      .block
        display:inline-block
        padding:8px 12px
        margin-right:8px
        border-radius:1px
        line-height:16px
        font-size:12px
        color: rgb(77, 85, 93)
        &.active
          color:#fff
        .count
          margin-left:2px
          font-size:8px
        &.positive
          background:lightblue
          &.active
            background:rgb(0,160,220)
          // background: rgb(0, 160, 220)
        &.negative
          background:rgba(77,85,93,0.2)
          &.active
            background:rgb(77,85,93)
    .switch
      padding:12px 18px
      line-height:24px
      border-bottom:1px solid rgba(7,17,27,0.1)
      color:rgb(147,153,159)
      font-size:0
      &.on
        .icon-check_circle
          color:#00c850
      .icon-check_circle
        vertical-align:top
        display:inline-block
        font-size:24px
        margin-right:4px
      .text
        font-size:12px
        vertical-align:top
        display:inline-block
        

      
</style>
