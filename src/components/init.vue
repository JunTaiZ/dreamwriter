<template>
  <div class=""
    @panstart="touchStart"
    @swipe="swipeLeft"
  >
    <wxc-minibar
      @wxcMinibarLeftButtonClicked="minibarLeftButtonClick"
      @wxcMinibarRightButtonClicked="minibarRightButtonClick"
      :use-default-return="false"
      :bar-style="minibarTodo"
      title=""
    >
      <text
        class="iconfont minibar-left" 
        slot="left"
      >&#xe7ec;</text>
      <text
        class="iconfont minibar-right"
        slot="right"
      >&#xe749;</text>
    </wxc-minibar>
    <list :style="listStyle">

    </list>
  </div>
</template>
<style scoped>
.iconfont {
  font-family: iconfont;
}
</style>
<script>
  import { WxcMinibar } from 'weex-ui';
  import { mapState, mapMutations, mapGetters } from 'vuex'
  export default {
    components: { 
      WxcMinibar
    },
    data: () => ({
      listStyle: {
        height: 0,
        width: 0,
      },
      touchStartX: 200,
    }),
    computed: {
      ...mapState('list', {
        statusIcon: 'statusIcon',
        statusList: 'statusList',
      }),
      ...mapState('pageConfig', [
        'contentHeight',
        'minibarTodo',
        'pageTodo'
      ])
    },
    created () {
      this.listStyle.height = this.contentHeight - 90 + 'px';
      this.listStyle.width = 750 + 'px';
    },
    methods: {
      pageHide () {
        this.pageTodo.ref.hidePage();
      },
      minibarLeftButtonClick () {
        this.pageHide();
      },
      minibarRightButtonClick () {
        
      },
      swipeLeft (e) {
        // console.log(e.changedTouches[0]);
        if (e.direction === 'right' && this.touchStartX < 100) {
          this.pageHide();
        }
      },
      touchStart (e) {
          let {pageX} = e.changedTouches[0]
          this.touchStartX = pageX
          // console.log(pageX)
      },
    }
  }
</script>