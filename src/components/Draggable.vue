<template>
  <vue-draggable-resizable
    :w="145"
    :h="206"
    :x="400"
    :y="200"
    @dragging="onDragging"
    @dragstop="onDragstop"
    :parent="true"
  >
    <slot :dragStart="dragStart"></slot>
  </vue-draggable-resizable>
</template>

<script>
import VueDraggableResizable from 'vue-draggable-resizable'
   export default {
       components:{
           VueDraggableResizable
       },
       data() {
           return {
           x: 0,
           y: 0,
           dragStart: false,
           }
       },
       methods: {
           onDragging(x, y) {
           this.dragStart = true;
           },
           onDragstop(ev){
            this.dragStart = false;
            }
        }
   }
</script>

<style scoped></style>
