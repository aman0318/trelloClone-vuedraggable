<template>
    <div>
         <div class="board-layout">
             <div class="left">
          <div class="board-text">Board</div>
                <tasklist />
        </div>
                
                
         </div>
    </div>
</template>
<script>
import tasklist from './trelloCards.tasklist.vue'
export default {
components:{
    tasklist
}
}
</script>

<style>

</style>