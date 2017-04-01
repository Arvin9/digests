<template>
    <div class="hello">
        <group>
            <cell title="title" value="value"></cell>
        </group>
    </div>
</template>

<script>
import { Group, Cell } from 'vux'

export default {
components: {
    Group,
    Cell
  },
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>


<style scoped>

</style>
