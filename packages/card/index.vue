<template>
  <div :class="b()">
    <div :class="b('header')">
      <a
        v-if="thumb || $slots.thumb"
        :href="thumbLink"
        :class="b('thumb')"
      >
        <slot name="thumb">
          <img
            v-if="lazyLoad"
            v-lazy="thumb"
            :class="b('img')"
          >
          <img
            v-else
            :src="thumb"
            :class="b('img')"
          >
        </slot>
        <van-tag
          v-if="tag"
          mark
          type="danger"
          :class="b('tag')"
        >
          {{ tag }}
        </van-tag>
      </a>

      <div :class="b('content')">
        <slot name="title">
          <div
            v-if="title"
            v-text="title"
            :class="b('title')"
          />
        </slot>
        <slot name="desc">
          <div
            v-if="desc"
            v-text="desc"
            :class="[b('desc'), 'van-ellipsis']"
          />
        </slot>
        <slot name="tags" />

        <div class="van-card__bottom">
          <div
            v-if="isDef(price)"
            :class="b('price')"
          >
            <slot name="price">{{ currency }} {{ price }}</slot>
          </div>
          <div
            v-if="isDef(originPrice)"
            :class="b('origin-price')"
          >
            {{ currency }} {{ originPrice }}
          </div>
          <div
            v-if="isDef(num) || $slots.num"
            :class="b('num')"
          >
            <slot name="num">x {{ num }}</slot>
          </div>
        </div>
      </div>
    </div>

    <div
      :class="b('footer')"
      v-if="$slots.footer"
    >
      <slot name="footer" />
    </div>
  </div>
</template>

<script>
import VanTag from '../tag';
import create from '../utils/create';

export default create({
  name: 'card',

  components: {
    VanTag
  },

  props: {
    tag: String,
    desc: String,
    thumb: String,
    title: String,
    centered: Boolean,
    lazyLoad: Boolean,
    thumbLink: String,
    num: [Number, String],
    price: [Number, String],
    originPrice: [Number, String],
    currency: {
      type: String,
      default: '¥'
    }
  }
});
</script>
