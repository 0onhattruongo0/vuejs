<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 offset-sm-2 col-md-6 offset-md-3 text-center">
        <h1>Animation</h1>
        <hr>
        <select v-model="typeAnimate" class="form-control mb-md-3">
          <option value="fade">Fade</option>
          <option value="slide">Slide</option>
        </select>
        <button class="btn btn-block btn-success" @click="show=!show">Show notification</button>
        <br>
        <br>
        <transition :name="typeAnimate">
          <div class="alert alert-success" v-if="show">This is something about notification.</div>
        </transition>
        <transition :name="typeAnimate" mode="out-in">
          <div class="alert alert-success" v-if="show" key="success">This is something about notification.</div>
          <div class="alert alert-danger" v-else key="danger">This is something about notification.</div>
        </transition>
        <!-- <transition name="slide">
          <div class="alert alert-warning" v-if="show">This is something about notification.</div>
        </transition>
        <transition name="slide" appear>
          <div class="alert alert-danger" v-if="show">This is something about notification.</div>
        </transition> -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      show: true,
      typeAnimate: 'fade'
    }
  }
}
</script>

<style>
  .fade-enter{
    opacity: 0;
  }
  .fade-enter-active{
    transition: opacity 1s;
  }
  .fade-leave{

  }
  .fade-leave-active{
    transition: opacity 1s;
    opacity: 0;
  }
  .slide-enter{
    opacity: 0;
  }
  .slide-enter-active{
    transition: opacity 1s;
    animation: slide-in 1s ease-out forwards;
  }
  .slide-leave{

  }
  .slide-leave-active{
    opacity: 0;
    transition: opacity 1s;
    animation: slide-out 1s ease-out forwards;
  }

  @keyframes slide-in{
    from{
      transform: translateY(20px);
    }
    to{
      transform: translateY(0);
    }
  }
  @keyframes slide-out{
    from{
      transform: translateY(0);
    }
    to{
      transform: translateY(20px);
    }
  }
</style>
