<template>
 <div class="container">
   <div class="row">
     <div class="col-6 divcard">
       <h2>{{cardWords}}</h2>
      <p>This is my card.</p>
      <slot></slot>
     </div>
   </div>
 </div>
</template>

<script>
export default {
  props: ['cardWords']
}
</script>

<style scoped>
    .divcard{
      border: 1px solid #ccc;
      box-shadow: 1px 1px 2px rgba(0, 0, 0, .6);
      padding: 30px;
      margin: 20px auto;
      text-align: center;
    }

</style>
