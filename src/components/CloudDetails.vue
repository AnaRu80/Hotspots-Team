<template>
  <div>
    <transition
      name="detail"
      @before-enter="beforeEnter"
      @after-enter="afterEnter"
      @before-leave="beforeLeave"
    >
      <div class="hotspot-details">
        <a href="#" @click.prevent="close" class="hotspot-details__close">
          <svg class="icon icon-close" viewBox="0 0 24 24">
            <path
              d="M18.984 6.422l-5.578 5.578 5.578 5.578-1.406 1.406-5.578-5.578-5.578 5.578-1.406-1.406 5.578-5.578-5.578-5.578 1.406-1.406 5.578 5.578 5.578-5.578z"
            ></path>
          </svg>
        </a>
        <flickity class="carousel" ref="flickity" :options="flickityOptions">
          <div class="carousel-cell" v-for="item in allItems" :key="item.key">
            <div class="hotspot-details__left">
              <div class="hotspot-details__content row justify-content-center ">
                <!-- <h3 class="text-success">{{item.description}}</h3> -->

                <div class="row justify-content-center mx-0 ">
                  <img :src="item.imageInfo" width="80%" class="my-auto" />
                </div>
                <div class="row justify-content-right w-100">
                  <div class="col-7 col-md-6 w-100 ml-auto text-left linkedIn-text__position">
                    <a :href="item.linkedIn">
                      <img src="../assets/images/logoIn.png" class="linkedIn-icon" alt="" />
                      <span class="linkedIn-text">Click to find me in LinkedIn</span>
                    </a>
                  </div>
                </div>
              </div>
            </div>

            <div class="hotspot-details__nav">
              <a
                href="#"
                @click.prevent="selectProduct(index)"
                class="hotspot-details__nav-item"
                v-for="(item, index) in allItems"
                :key="item.key"
              >
                <img :src="item.image" width="80%" />
              </a>
            </div>
          </div>
        </flickity>
      </div>
    </transition>
  </div>
</template>

<script>
import Flickity from 'vue-flickity';

export default {
  name: 'CloudDetails',

  props: {
    item: { type: Object },
    selectedIndex: { type: Number },
    allItems: { type: Array }
  },
  data() {
    return {
      selectedItem: this.item,
      flickityOptions: {
        cellAlign: 'left',
        contain: true,
        draggable: true,
        initialIndex: this.selectedIndex,
        imagesLoaded: true,
        prevNextButtons: true,
        pageDots: true
      }
    };
  },
  components: {
    Flickity
  },

  methods: {
    close() {
      this.$emit('close');
    },
    selectProduct(index) {
      this.flickityOptions.select(index);
    },
    onProductSelected() {
      this.selectedItem = this.allItems[this.flickityOptions.selectedIndex];
    },
    beforeEnter(el) {
      el.style.setProperty(`--top`, this.item.position.top);
      el.style.setProperty(`--left`, this.item.position.left);
    },
    afterEnter(el) {
      el.classList.add('is-loaded');
    },
    beforeLeave(el) {
      el.classList.remove('is-loaded');
    }
  }
};
</script>

<style scoped></style>
