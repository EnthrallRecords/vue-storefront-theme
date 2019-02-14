<template>
  <div class="row center-xs">
    <div
      class="col-sm-4 pb15"
      v-for="(tile, index) in social_tiles"
      :key="index"
    >
      <router-link :to="localizedRoute(tile.link)">
        <div
          class="tile center-xs middle-xs"
        >
          <img
            class="tile-image"
            v-lazy="tile.image"
            :alt="tile.alt"
          >
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TileLinks',
  data () {
    return {
      social_tiles: [
        {
          image: '/assets/tl/Music.png',
          alt: 'Music',
          link: '/c/music'
        },
        {
          image: '/assets/tl/Merch.png',
          alt: 'Merch',
          link: '/c/merch'
        },
        {
          image: '/assets/tl/Apparel.png',
          alt: 'Apparel',
          link: '/c/apparel'
        }
      ]
    }
  }
}
</script>

<style lang='scss' scoped>
@import '~theme/css/animations/transitions';

.tile {
  display: flex;
  overflow: hidden;
}

.tile-image {
  width: 100%;
  height: 100%;
  transition: transform 0.3s $motion-main;

  &:hover,
  &:focus {
    transform: scale(1.2);
  }
}
</style>
