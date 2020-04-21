<template lang="pug">
#IntroducingEagle.eg-theme-agrume
  .eg-slideshow
    slide(enter='fadeIn' leave='bounceOutLeft')
      .center.frontpage
        h1 Sup`GAMES
        img(src='./assets/logo.svg')
        h4 A specialization and lab project from Supinfo
        eg-triggered-message(:trigger='slideTimer >= 2',
                            :duration='6', position='top right',
                            enter='bounceInRight', leave='bounceOutRight')
          p Next:
          img.control-schema(src='./assets/controlsNext.svg')
          p Previous:
          img.control-schema(src='./assets/controlsPrev.svg')

    slide(:steps=7, enter='bounceInRight' leave='bounceOutDown')
      h3
        | Project
        .inline(class='animated infinite pulse heart')
        | Introduction
      .center
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 2")
            <b>Sup`GAMES</b> will first introduce step by step courses on subjects to make games
        eg-transition(enter='bounceInRight' leave='bounceOutRight')
          p(v-if="step >= 3")
            <b>These courses</b> will be done by the students, followed by some full-teachers
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 4")
            <b>At the same time</b> we will develop a space MMORTS game for the long-term
        eg-transition(enter='bounceInRight' leave='bounceOutRight')
          p(v-if="step >= 5")
            <b>We will</b> also constitute a Game Lab, to share techniques & build smaller games
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 6")
            <b>Teams</b> will be defined, regarding all aspects of a game development
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 7")
            <b>This game project</b> will be open source and available as well to external peoples

    slide(:steps=6, enter='bounceInDown')
      h3 What's the human needs?

      eg-transition(enter='fadeIn' leave='fadeOut')
        .quarter(v-if='step >=2')
          img(src='./assets/icons/basic_paperplane.svg')
          h4 ALL CURSUS
          p SiiT, SiiB, SiaD, SicM

      eg-transition(enter='fadeIn' leave='fadeOut')
        .quarter(v-if='step >=3')
          img(src='./assets/icons/basic_share.svg')
          h4 ALL CAMPUS
          p Physical, International, Virtual

      eg-transition(enter='fadeIn' leave='fadeOut')
        .quarter(v-if="step >= 4")
         img(src='./assets/icons/basic_mixer2.svg')
         h4 MANY TOPICS
         p Art, Dev, Design, Marketing, Story, ...

      eg-transition(enter='fadeIn' leave='fadeOut')
        .quarter(v-if="step >= 5")
          img(src='./assets/icons/basic_display.svg')
          h4 BRAINS IN ACTION
          p Thoughts and Regular meetings

      eg-transition(enter='fadeIn' leave='fadeOut')
        eg-modal(v-if='step >= 6')
          h3 You right now:
          .center
            img(:src="preloadedImages['youRightNow']",
                :style="{height: '10em'}")
</template>

<script>
import eagle from 'eagle.js'

export default {
  mixins: [eagle.slideshow],
  infos: {
    title: 'Introducing Sup`GAMES',
    description: 'Specialization & Lab',
    path: 'introducing-eagle'
  },
  components: {
    'awesome-inserted-slide': require('./AwesomeInsertedSlide').default,
    'figures-slide': require('./FiguresSlide').default,
    'end-credits': require('./components/EndCredits').default
  },
  data: function () {
    return {
      username: 'Tracy',
      preference: 'baby bunnies',
      preferences: [
        {
          label: 'baby bunnies',
          text: 'Baby bunnies'
        },
        {
          label: 'fluffy puppies',
          text: 'Fluffy puppies'
        },
        {
          label: 'funny kitties',
          text: 'Funny kitties'
        }
      ],
      slideCategories: {
        themes: {
          show: true,
          name: 'Theming'
        },
        slideReuse: {
          show: true,
          name: 'Slide reuse'
        },
        interactivity: {
          show: true,
          name: 'Interactivity'
        }
      },
      preloadedImages: {
        computerKid: 'https://i.imgur.com/AAlntwU.gif',
        youRightNow: 'https://i.imgur.com/DFBTj0a.gif',
        bretagne: 'https://i.imgur.com/rYkJ6I8.jpg',
        forrestRoad: 'https://i.imgur.com/hxTMFZW.jpg',
        starrySky: 'https://i.imgur.com/yO2ivoD.jpg',
        cityBokeh: 'https://i.imgur.com/kmmHith.jpg',
        darkWoods: 'https://i.imgur.com/FL9mwpd.jpg',
        pushButton: 'https://i.imgur.com/KaAyvZ5.gif'
      }
    }
  },
  methods: {
    message: function (name) {
      return {
        'baby bunnies': 'Yeeeeah my favorite too !',
        'fluffy puppies': 'Wow so original.',
        'funny kitties': 'Good for you ' + this.username + '.',
        'Theming': 'Ok ' + this.username + ', whatever.',
        'Slide reuse': 'Seriously ' + this.username + ' you <em>want</em> to see this.',
        'Interactivity': 'Well that\'s this slide, ' + this.username +
                         '. <br /> A bit too late to unsee it, heh ?'
      }[name]
    }
  }
}
</script>

<style lang='scss'>
@import 'node_modules/eagle.js/dist/themes/agrume/agrume';
#IntroducingEagle {
  .frontpage {
    img {
      height: 7em;
    }
    img.control-schema {
      width: 8em;
      height: 3em;
    }
  }
  .heart {
    width: 1em;
    height: 0.8em;
    margin-left: 0.1em;
    margin-right: 0.1em;
    background-image: url('./assets/heart.svg');
    background-position: center center;
    background-repeat:  no-repeat;
    background-size: contain;
  }

  .quarter {
    text-align: center;
    p {
      margin-top: 0;
      text-align: center;
    }
    h4 {
      margin-top: 0;
      margin-bottom: 0
    }
  }
  .boredYet {
    p {
      margin-bottom: 0.3em;
      margin-top: 1.3em;
    }
    .button {
      border: none;
    }
    .button.prev {
      float: left;
    }
    .button.next {
      float: right;
    }
  }
  img.computerkid {
    height: 6.5em;
  }

  a {
    color: black;
  }

  .parentWindow {
    border: solid 1px red;
  }
}
</style>
