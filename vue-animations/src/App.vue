<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Animations</h1>
        <hr>

        <select v-model="alertAnimation" class="form-control">
          <option value="fade">Fade</option>
          <option value="slide">Slide</option>
        </select>
        <br><br>

        <button class="btn btn-primary" @click="show = !show">Show Alert</button>
        <br><br>

        <transition :name="alertAnimation">
          <div class="alert alert-info" v-show="show">This is some information</div>
        </transition>

        <transition name="slide" type="animation" appear>
          <div class="alert alert-info" v-if="show">This is some information</div>
        </transition>

        <transition
          enter-active-class="animated bounce"
          leave-active-class="animated shake">
          <div class="alert alert-info" v-if="show">This is some information</div>
        </transition>

        <transition :name="alertAnimation" mode="out-in">
          <div class="alert alert-info" v-if="show" key="info">This is some information</div>
          <div class="alert alert-warning" v-else key="warning">This is a warning</div>
        </transition>

        <hr>
        <button class="btn btn-primary" @click="load = !load">Load / Remove Element</button>
        <br><br>
        <transition
          @before-enter="beforeEnter"
          @enter="enter"
          @after-enter="afterEnter"
          @enter-cancelled="enterCancelled"
          @before-leave="beforeLeave"
          @leave="leave"
          @after-leave="afterLeave"
          @leave-cancelled="leaveCancelled"
          :css="false">
          <div style="background-color: lightgreen; height: 100px; width: 300px" v-if="load"></div>
        </transition>

        <hr>

        <button class="btn btn-primary"
                @click="selectedComponent == 'app-success-alert' ? selectedComponent = 'app-danger-alert' : selectedComponent = 'app-success-alert'">
          Toggle Components
        </button>

        <br>
        <br>

        <transition name="fade" mode="out-in">
          <component :is="selectedComponent"></component>
        </transition>

        <hr>

        <button class="btn btn-primary" @click="addItem">Add Item</button>

        <br>
        <br>

        <ul class="list-group">
          <transition-group name="slide">
            <li class="list-group-item"
                v-for="(number, index) in numbers"
                @click="removeItem(index)"
                style="cursor: pointer"
                :key="number">{{ number }}
            </li>
          </transition-group>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  import DangerAlert from './DanagerAlert'
  import SuccessAlert from './SuccessAlert'

  export default {
    data () {
      return {
        load: true,
        show: false,
        alertAnimation: 'fade',
        elementWidth: 100,
        selectedComponent: 'app-success-alert',
        numbers: [1, 2, 3, 4, 5]
      }
    },
    methods: {
      beforeEnter (el) {
        console.log('beforeEnter')
        this.elementWidth = 100
        el.style.width = this.elementWidth + 'px'
      },
      enter (el, done) {
        console.log('enter')
        let round = 1
        const interval = setInterval(() => {
          el.style.width = (this.elementWidth + round * 10) + 'px'
          round++
          if (round > 20) {
            clearInterval(interval)
            done() // Tell Vue.js when the animation has finished
          }
        }, 20)
      },
      afterEnter (el) {
        console.log('afterEnter')
      },
      enterCancelled (el) {
        console.log('enterCancelled')
      },
      beforeLeave (el) {
        console.log('beforeLeave')
        this.elementWidth = 300
        el.style.width = this.elementWidth + 'px'
      },
      leave (el, done) {
        console.log('leave')
        let round = 1
        const interval = setInterval(() => {
          el.style.width = (this.elementWidth - round * 10) + 'px'
          round++
          if (round > 20) {
            clearInterval(interval)
            done() // Tell Vue.js when the animation has finished
          }
        }, 20)
      },
      afterLeave (el) {
        console.log('afterLeave')
      },
      leaveCancelled (el) {
        console.log('leaveCancelled')
      },
      addItem () {
        const pos = Math.floor(Math.random() * this.numbers.length)
        this.numbers.splice(pos, 0, this.numbers.length + 1) // Add another item
      },
      removeItem (index) {
        this.numbers.splice(index, 1)
      }
    },
    components: {
      appDangerAlert: DangerAlert,
      appSuccessAlert: SuccessAlert
    }
  }
</script>

<style>
  .fade-enter {
    opacity: 0;
  }

  .fade-enter-active {
    transition: opacity 1s;
  }

  .fade-leave {

  }

  .fade-leave-active {
    transition: opacity 1s;
    opacity: 0;
  }

  .slide-enter {
    opacity: 0;
  }

  .slide-enter-active {
    animation: slide-in 1s ease-out forwards;
    transition: opacity .5s;
  }

  .slide-leave {

  }

  .slide-leave-active {
    animation: slide-out 1s ease-out forwards;
    opacity: 0;
    position: absolute;
    transition: opacity 1s;
  }

  /* Attached to any element that needs to change it's place (after adding or deleting an element). */
  .slide-move {
    transition: transform 1s;
  }

  @keyframes slide-in {
    from {
      transform: translateY(1em);
    }

    to {
      transform: translateY(0);
    }
  }

  @keyframes slide-out {
    from {
      transform: translateY(0);
    }

    to {
      transform: translateY(1em);
    }
  }
</style>
