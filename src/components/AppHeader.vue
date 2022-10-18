 <script setup>
   defineProps(['color1'])
 </script>
 
 
 <template>
  <header>
    <h1 :style="{'color': color1}"><slot>No Title</slot></h1>
  </header>
 </template>