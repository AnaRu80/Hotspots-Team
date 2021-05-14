<template>
  <div class="boxed">
    <b-row>
      <b-col cols="12">
        <!-- <img src="./assets/images/Teams-Avatar.png" width="100%" alt=""> -->
        <div class="cloud">
          <div class="image-hotspot" :class="{ 'is-selected': open }">
            <CloudDetails
              :item="selectedHotspot"
              :selected-index="selectedIndex"
              :all-items="hotspots"
              @close="closeDetails"
              v-if="open"
            ></CloudDetails>
            <transition-group name="hotspots">
              <a
                href="#"
                class="hotspot-point"
                v-for="(hotspot, index) in hotspotItems"
                :style="[
                  windowWidth >= 990
                    ? { top: hotspot.position.top, left: hotspot.position.left }
                    : {
                        top: hotspot.positionMob.top,
                        left: hotspot.positionMob.left
                      }
                ]"
                @click.prevent="hotspotClicked(hotspot, index)"
                :key="index"
              >
                <span :data-price="hotspot.title">
                  <svg class="icon icon-close" viewBox="0 0 24 24">
                    <path d="M18.984 12.984h-6v6h-1.969v-6h-6v-1.969h6v-6h1.969v6h6v1.969z"></path>
                  </svg>
                </span>
              </a>
            </transition-group>
            <img id="imgTeam" src="./assets/images/Teams-Avatar.png" alt="" @click="closeDetails" />
            <div style="height:20px"></div>
          </div>
        </div>
        <!-- <div id="cloud"></div> -->
      </b-col>
    </b-row>
  </div>
</template>

<script>
import CloudDetails from '@/components/CloudDetails.vue';

const hotspots = [
  {
    id: 1,
    title: 'Roberto',
    name: 'Roberto Flores',
    // price: '$1,299.00',
    imageAvatar: require('./assets/images/I-CEO-Roberto.png'),
    imageInfo: require('./assets/images/I-CEO-Roberto.png'),
    linkedIn: 'https://www.linkedin.com/in/energycloud/',
    position: { top: '22%', left: '30%' },
    positionMob: { top: '32%', left: '24%' }
  },
  {
    id: 2,
    title: 'Pedro',
    name: 'Pedro Bejarano',
    imageAvatar: require('./assets/images/I-CFO-Pedro.png'),
    imageInfo: require('./assets/images/I-CFO-Pedro.png'),
    linkedIn: 'https://www.linkedin.com/in/pedro-bejarano-31aa8769/',
    position: { top: '20%', left: '48%' },
    positionMob: { top: '29%', left: '49%' }
  },
  {
    id: 3,
    title: 'Alessandro',
    name: 'Alessandro Citelli',
    imageAvatar: require('./assets/images/I-COO-Alessandro.png'),
    imageInfo: require('./assets/images/I-COO-Alessandro.png'),
    linkedIn: 'https://www.linkedin.com/in/alessandro-citelli-apruzzese-2a797b1b/',
    position: { top: '35%', left: '19.7%' },
    positionMob: { top: '53%', left: '9%' }
  },
  {
    id: 3,
    title: 'Aldo',
    name: 'Aldo Solari',
    imageAvatar: require('./assets/images/I-SalesExec-Aldo.png'),
    imageInfo: require('./assets/images/I-SalesExec-Aldo.png'),
    linkedIn: 'https://www.linkedin.com/in/aldo-solari-v/',
    position: { top: '35%', left: '36.7%' },
    positionMob: { top: '52%', left: '33%' }
  },

  {
    id: 4,
    title: 'Michael',
    name: 'Michael Chavez',
    imageAvatar: require('./assets/images/I-ProductDeveloper-Michael.png'),
    imageInfo: require('./assets/images/I-ProductDeveloper-Michael.png'),
    linkedIn: 'https://www.linkedin.com/in/michaelchavezleed/',
    position: { top: '35%', left: '53.7%' },
    positionMob: { top: '52%', left: '58%' }
  },
  {
    id: 5,
    title: 'Alvick',
    name: 'Alvick Maliqui',
    imageAvatar: require('./assets/images/I-DataWizard-Alvick.png'),
    imageInfo: require('./assets/images/I-DataWizard-Alvick.png'),
    linkedIn: 'https://www.linkedin.com/in/alvick-mallqui-alor-068775144/',
    position: { top: '33%', left: '71%' },
    positionMob: { top: '51%', left: '82%' }
  },
  {
    id: 6,
    title: 'Karina',
    name: 'Karina Yela',
    imageAvatar: require('./assets/images/I-PM-Karina.png'),
    imageInfo: require('./assets/images/I-PM-Karina.png'),
    linkedIn: 'https://www.linkedin.com/in/karina-yela-lascano/',
    position: { top: '52%', left: '43.3%' },
    positionMob: { top: '75%', left: '44%' }
  },
  {
    id: 7,
    title: 'Georgina',
    name: 'Georgina Reinoso',
    imageAvatar: require('./assets/images/I-BDM-Georgina.png'),
    imageInfo: require('./assets/images/I-BDM-Georgina.png'),
    linkedIn: 'https://www.linkedin.com/in/georgina-reinoso-0286813b/',
    position: { top: '50%', left: '61.5%' },
    positionMob: { top: '74%', left: '69%' }
  }
];

export default {
  name: 'Cloud',
  components: {
    CloudDetails
  },

  data() {
    return {
      windowWidth: window.innerWidth,
      hotspots,
      open: false,
      hotspotPosition: null,
      selectedHotspot: null
    };
  },

  computed: {
    hotspotItems() {
      return this.open ? [] : this.hotspots;
    }
  },

  methods: {
    closeDetails() {
      this.open = false;
    },

    hotspotClicked(hotspot, index) {
      this.selectedHotspot = hotspot;
      this.selectedIndex = index;

      this.open = true;
    },

    handleResize() {
      this.windowWidth = window.innerWidth;
    },

    beforeDestroy() {
      window.removeEventListener('resize', this.handleResize);
    }
  }
};
</script>

<style scoped></style>
