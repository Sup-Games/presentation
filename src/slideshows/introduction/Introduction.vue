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

    slide(:steps=4, leave='fadeOut')
      eg-transition(enter='flipInX')
        h3 Show me the codey !!!

      eg-transition(enter='flipInX')
        p Here is how you slideshow with Eagle.js:

      eg-transition(enter='flipInX')
        eg-code-block(lang='html').
          .eg-slideshow

            slide <eg-code-comment :active='step === 2' enter='flipInY'> EAGLE SLIDE TAG</eg-code-comment>
              h1 EagleJS <eg-code-comment :active='step === 3' enter='flipInY'> SIMPLIFIED HTML (PUG)</eg-code-comment>
              img(src='logo.png')

            slide(enter='slideInLeft', :steps=4)
              h3 EagleJS is the greatest slideshow framework
              p(v-if="step >= 2") The best !  <eg-code-comment :active='step === 4' enter='flipInY'> BULLET POINT WITH V-IF</eg-code-comment>
              p(v-if="step >= 3") All others are failed frameworks.
              p(v-if="step >= 4") Not even real frameworks. Fake !

    slide.boredYet(enter='fadeIn', :mouseNavigation='false', :keyboardNavigation='false')
      h3 Bored yet ?
      .center
        p What shall I call you ?
        input.center(v-model='username')
        p.
          {{ username }}<span v-if='username.length'>,</span> I got you.
          Tell me what you like, I'll skip the rest:

        .inline(v-for='category, name in slideCategories')
            eg-toggle(:key='name', v-model='category.show', :width='30',
                      on-text='', off-text='', on-color='#ffeeaa',
                      @change='changeMessage(category.changeMessage)')
              p.label {{ category.name }}
              eg-triggered-message(:trigger='!category.show',
                                  :duration='3', position='top right',
                                  enter='bounceInRight', leave='bounceOutRight')
                p(v-html="message(category.name)")

      .center
        p What's your favourite ?
        eg-radio-button.inline(v-for='(pref, i) in preferences', v-model="preference",
                        :label="pref.label" :key="i")
          p {{ pref.text}}
          eg-triggered-message(:trigger='preference=== pref.label',
                              :duration='3', position='top right',
                              enter='bounceInRight', leave='bounceOutRight')
                          p {{ message(pref.label) }}

      .button.prev(@click.stop='previousSlide')
        span &lt; Prev. slide
        br
        span.small  Ctrl + left
      .button.next(@click.stop='nextSlide')
        span Next slide &gt;
        br
        span.small Ctrl + right

    awesome-inserted-slide(:username='username', :preference='preference',
                           enter='fadeIn', leave='hinge',
                           :skip="!slideCategories['slideReuse'].show")

    figures-slide(enter='flipInY', leave='rollOut', :skip="['slideReuse', 'themes', 'interactivity'].some(function (e) {return slideCategories[e].show})")

    slide(:steps='5' enter='fadeIn' leave='fadeOut')
      h3 Presenter Mode
      p.center What if I'm too lazy and cannot remember my notes when doing a presentation?
      .center
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 2")
            | By default pressing P toggles Presenter Mode
        eg-transition(enter='bounceInRight' leave='bounceOutRight')
          p(v-if="step >= 3")
            | You have a cloned child view which shares parent's control
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 4")
            | Then on parent window you can have all the fun!
        eg-transition(enter='fadeIn' leave='fadeOut')
          eg-modal(v-if="step >= 5")
            h3 PUSH THE P BUTTON NOW!!:
            .center
              img(:src="preloadedImages['pushButton']",
                  :style="{height: '10em'}")

    slide(:steps='5' enter='fadeIn' leave='fadeOut')
      h3(v-if="childWindow")
        | Speaker Notes
      h3(v-if="parentWindow")
        | Presentation
      h3(v-if="!childWindow && !parentWindow")
        | Press P if you haven't
      p.center(v-if="childWindow") We can have some fun in our parent window!
      p.center(v-if="parentWindow") I'm doing a very serious talk right now
      .center
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 2")
            | Eagle.js is easy to use
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          h6(v-if="step >= 2 && childWindow")
            | we can have a timer here: {{ slideTimer }}
        eg-transition(enter='bounceInRight' leave='bounceOutRight')
          p(v-if="step >= 3")
            | Eagle.js has max hackability
        eg-transition(enter='bounceInRight' leave='bounceOutRight')
          h6(v-if="step >= 3 && childWindow")
            | we can display the current slide index here: {{ currentSlideIndex }}
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 4")
            | Eagle.js is modular
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          h6(v-if="step >= 4 && childWindow")
            | we also could insert our notes here (duh)
        eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 5")
            | You can press P again to close child window

    slide(:steps=6, leave='fadeOut')
      eg-transition(enter='flipInX')
        h3 To use Presenter Mode
      eg-transition(enter='flipInX')
        eg-code-block(lang='html').
          .eg-slideshow

            slide
              p Eagle.is is awesome!<eg-code-comment :active='step === 2' enter='flipInY'>This would always show up</eg-code-comment>
              p(v-if="parentWindow") I can be a note!<eg-code-comment :active='step === 3' enter='flipInY'>This would only show on child window</eg-code-comment>
              p(v-if="childWindow") I can be a note too!<eg-code-comment :active='step === 4' enter='flipInY'>This would only show on parent window</eg-code-comment>
      eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 5")
            | It might be counter-intuitive that '(v-if="parentWindow")' is actually child window. It's because it means this window has a parent window, thus making itself a child window.
      eg-transition(enter='bounceInLeft' leave='bounceOutLeft')
          p(v-if="step >= 6")
            | But the good thing is that you can put notes in either parent window or child window, so it really doesn't matter!

    slide(enter='zoomIn', leave='fadeOut')
      h3 That's all folks !
      p.center Think you can help ?
      .center
        img.computerkid.shadowbox(src='https://i.imgur.com/AAlntwU.gif')
      p.center.
        I'm not a frontend person, so everyone<br />
        is welcome to contribute to <a href="https://github.com/Zulko/eagle.js" target='_blank'> the repo</a>.

    slide(enter='fadeIn')
      h3 Thank you !
      p This slideshow's so fresh, it has end credits.
      end-credits(:username='username')
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
    border: solide 1px red;
  }
}
</style>
