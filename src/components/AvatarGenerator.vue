<template>
  <section class="avatar-generator content">
    <h1 class="avatar-title">Генерация Аватара</h1>
    <div class="avatar-generator avatar" id="avatar"
    v-bind:style="{backgroundImage: `url(${require(`@/assets/img/bg/${selectedBg}.jpg`)})`}"
    >
      <img src="@/assets/img/head.svg" alt="head" class="avatar-detail avatar-head">
      <img :src="selectedTop" id="avatar-top" alt="hear" class="avatar-detail avatar-top">
      <img :src="selectedMouth" id="avatar-mouth" alt="mouthes" class="avatar-detail avatar-mouth">
      <img :src="selectedEyes" id="avatar-eyes" alt="eyes" class="avatar-detail avatar-eyes">
      <img :src="selectedGlasses" id="avatar-glasses" alt="" class="avatar-detail avatar-glasses">
      <img :src="selectedEyebrows" id="avatar-eyebrows" alt="eyebrows" class="avatar-detail avatar-eyebrows">
      <img :src="selectedBody" id="avatar-body" alt="body" class="avatar-detail avatar-body">
      <img :src="selectedPets" id="avatar-pet" alt="pet" class="avatar-detail avatar-pet">
    </div>
    <div class="avatar-generator buttons">
      <button class="button" @click="changeAvatar()" id="generate-button">
        Generate
      </button>
      <button class="button" id="download-button" @click="printThis()">
        Download
      </button>
    </div>
  </section>
</template>

<script>
import html2canvas from 'html2canvas'

export default {
  data () {
    return {
      countBg: 3,
      countTop: [
        require('@/assets/img/top/1.svg'),
        require('@/assets/img/top/2.svg'),
        require('@/assets/img/top/3.svg'),
        require('@/assets/img/top/4.svg'),
        require('@/assets/img/top/5.svg'),
        require('@/assets/img/top/6.svg'),
        require('@/assets/img/top/7.svg'),
        require('@/assets/img/top/8.svg')
      ],
      countBody: [
        require('@/assets/img/body/1.svg'),
        require('@/assets/img/body/2.svg'),
        require('@/assets/img/body/3.svg'),
        require('@/assets/img/body/4.svg'),
        require('@/assets/img/body/5.svg'),
        require('@/assets/img/body/6.svg')
      ],
      countEyebrows: [
        require('@/assets/img/eyebrows/1.svg'),
        require('@/assets/img/eyebrows/2.svg'),
        require('@/assets/img/eyebrows/3.svg'),
        require('@/assets/img/eyebrows/4.svg'),
        require('@/assets/img/eyebrows/5.svg'),
        require('@/assets/img/eyebrows/6.svg')
      ],
      countMouth: [
        require('@/assets/img/mouthes/1.svg'),
        require('@/assets/img/mouthes/2.svg'),
        require('@/assets/img/mouthes/3.svg'),
        require('@/assets/img/mouthes/4.svg'),
        require('@/assets/img/mouthes/5.svg'),
        require('@/assets/img/mouthes/6.svg')
      ],
      countEyes: [
        require('@/assets/img/eyes/1.svg'),
        require('@/assets/img/eyes/2.svg'),
        require('@/assets/img/eyes/3.svg'),
        require('@/assets/img/eyes/4.svg'),
        require('@/assets/img/eyes/5.svg')
      ],
      countGlasses: [
        '',
        require('@/assets/img/glasses/1.svg'),
        require('@/assets/img/glasses/2.svg'),
        require('@/assets/img/glasses/3.svg')
      ],
      countPets: [
        '',
        require('@/assets/img/pets/1.svg'),
        require('@/assets/img/pets/2.svg'),
        require('@/assets/img/pets/3.svg'),
        require('@/assets/img/pets/4.svg')
      ],
      selectedBg: 1,
      selectedTop: null,
      selectedEyebrows: null,
      selectedMouth: null,
      selectedEyes: null,
      selectedGlasses: null,
      selectedPets: null,
      selectedBody: null
    }
  },
  methods: {
    randomItem (items) {
      return items[Math.floor(Math.random() * items.length)]
    },

    async printThis () {
      const el = document.getElementById('avatar')
      const options = {
        type: 'dataURL'
      }
      const printCanvas = await html2canvas(el, options)
      const link = document.createElement('a')
      link.setAttribute('download', 'download.png')
      link.setAttribute(
        'href',
        printCanvas
          .toDataURL('image/png')
          .replace('image/png', 'image/octet-stream')
      )
      link.click()
    },

    changeAvatar () {
      this.selectedTop = this.randomItem(this.countTop)
      this.selectedBody = this.randomItem(this.countBody)
      this.selectedEyebrows = this.randomItem(this.countEyebrows)
      this.selectedMouth = this.randomItem(this.countMouth)
      this.selectedEyes = this.randomItem(this.countEyes)
      this.selectedGlasses = this.randomItem(this.countGlasses)
      this.selectedPets = this.randomItem(this.countPets)
      this.selectedBg = Math.floor(Math.random() * 3) + 1
    }
  },

  mounted () {
    this.changeAvatar()
  }
}
</script>

<style lang="scss" scoped>
.content {
  text-align: center;
}

.avatar {
  width: 440px;
  height: 440px;
  position: relative;
  margin: auto;
  overflow: hidden;
  margin-bottom: 20px;

  &-title {
    font-size: 30px;
  }

  &-wrapper {
    border: #000 solid;
    padding-top: 10px;
    width: 100%;
    margin: 0 auto;
    max-width: 500px;
  }

  &-detail {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
  }

  &-head {
   top: 132px;
  }

  &-top {
    top: 58px;
    z-index: 2;
  }

  &-mouth {
   top: 225px;
  }

  &-eyes {
    top: 200px;
  }

  &-glasses {
    top: 194px;
    z-index: 1;
  }

  &-eyebrows {
    top: 176px;
  }

  &-body {
   top: 297px;
  }

  &-pet {
    position: absolute;
    bottom: -67px;
    left: -50px;
    transform: rotate(-25deg);
    z-index: 200;
  }
}

.button {
  width: 100px;
  height: 40px;
  border: none;
  background: #4149F2;
  color: #fff;
  font-size: 17px;
  cursor: pointer;

    &:first-child {
      margin-right: 0.2rem;
    }

    &:hover {
      opacity: 0.9;
    }

  }
</style>
