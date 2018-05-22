<template>
	<div class="recommend">
		<Scroll ref="scroll" class="recommend-content" :data="discList">
      <div>
        <div class="recommend-list">
          <h1 class="list-title">热门歌曲推荐</h1>
          <ul>
            <li v-for="(item,index) in discList" :key="index" class="item">
              <div class="icon">
                <img width="60" height="60" class="needsclick" :src="item.imgurl">
              </div>
              <div class="text">
                <h2 class="name" v-html="item.creator.name"></h2>
                <p class="desc" v-html="item.dissname"></p>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </Scroll>
	</div>
</template>

<script>
import Scroll from '../scroll/scroll'

export default {
  data() {
    return {
      discList: []
    }
  },
  created() {
    this._getDiscList()
  },
  methods: {
    _getDiscList() {
      this.$http.get('api/list').then((res) => {
        this.discList = res.data.data
      })
    }
  },
  components: {
    Scroll
  }
}
</script>
<style scoped lang="stylus" rel="stylesheet/stylus">
  // 颜色定义规范
  $color-background = #222
  $color-background-d = rgba(0, 0, 0, 0.3)
  $color-highlight-background = #333
  $color-dialog-background = #666
  $color-theme = #ffcd32
  $color-theme-d = rgba(255, 205, 49, 0.5)
  $color-sub-theme = #d93f30
  $color-text = #fff
  $color-text-d = rgba(255, 255, 255, 0.3)
  $color-text-l = rgba(255, 255, 255, 0.5)
  $color-text-ll = rgba(255, 255, 255, 0.8)

  //字体定义规范
  $font-size-small-s = 10px
  $font-size-small = 12px
  $font-size-medium = 14px
  $font-size-medium-x = 16px
  $font-size-large = 18px
  $font-size-large-x = 22px
  .recommend
    position: fixed
    width: 100%
    top: 0px
    bottom: 0
    background: $color-background
    .recommend-content
      height: 100%
      overflow: hidden
      .slider-wrapper
        position: relative
        width: 100%
        overflow: hidden
      .recommend-list
        .list-title
          height: 65px
          line-height: 65px
          text-align: center
          font-size: $font-size-medium
          color: $color-theme
        .item
          display: flex
          box-sizing: border-box
          align-items: center
          padding: 0 20px 20px 20px
          .icon
            flex: 0 0 60px
            width: 60px
            padding-right: 20px
          .text
            display: flex
            flex-direction: column
            justify-content: center
            flex: 1
            line-height: 20px
            overflow: hidden
            font-size: $font-size-medium
            text-align: left;
            .name
              margin-bottom: 10px
              color: $color-text
            .desc
              color: $color-text-d
      .loading-container
        position: absolute
        width: 100%
        top: 50%
        transform: translateY(-50%)
</style>
