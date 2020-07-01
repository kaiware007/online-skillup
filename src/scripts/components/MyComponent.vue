<template>
  <transition-group tag="ul" class="list" name="flip">
    <template v-for="item in $props.messageList">
      <li :key="item" class="item">
        <p class="item__name">{{ item.name }}</p>
        <p class="item__text">{{ item.text }}</p>
      </li>
    </template>
  </transition-group>
</template>

<script>
import VueTypes from 'vue-types';

export default {
  props: {
    messageList: VueTypes.arrayOf(VueTypes.shape({
      name: VueTypes.string.isRequired,
      text: VueTypes.string.isRequired
    })).isRequired
  }
};
</script>

<style lang="scss" scoped>

body {
  background-color: #ddd;
}

.list {
  position: relative;
  padding: 0;
}

.item {
  position: relative;
  // display: flex;
  align-items: center;
  width: 100%;
  transition: all 0.5s;
  // padding: 1px;
  // margin-top: 10px;
  cursor: pointer;

  &__name {
    // flex: 1 1 0;
    padding: 0 5px;
    font-size: 12px;
    margin: 10px 0 0 0;
  }

  &__text {
    // flex: 1 1 0;
    margin: 0 10px 10px 10px;
    padding: 10px;
    border: solid 1px #ddd;
    border-radius: 15px;
    // box-shadow: 0 0 10px 0 rgba(#000, 0.1);
    background-color: #ddd;
  }

  &__text::before {
    content: '';
    position: absolute;
    top: 50%;
    left: 2px;
    margin-top: -1px;
    display: block;
    width: 1px;
    height: 1px;
    border-style: solid;
    border-width: 1px 8px 8px 0;
    border-color: transparent #ddd transparent transparent;
  }
}

.flip {
  // 要素が動くときにtransitionを設定する（.itemでtransitionを設定しているため-moveで書く必要はない）
  // &-move {
  //   transition: transform 0.5s;
  // }

  // 要素が入るときのアニメーション
  &-enter {
    &-active {
      opacity: 0;
      transform: translate3d(0, -30px, 0);
    }

    &-to {
      opacity: 1;
      transform: translate3d(0, 0, 0);
    }
  }

  // 要素が消える時のアニメーション
  &-leave {
    &-active {
      position: absolute;
    }

    &-to {
      opacity: 0;
      transform: translate3d(0, -30px, 0);
    }
  }
}
</style>
