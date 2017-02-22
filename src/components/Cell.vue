<template>
<div
  class="cell"
  :class="{'deselected': !item.selected, 'selected': item.selected, 'locked': item.locked}"
  @click="toggle()" @click.left="toggleLock()">
  {{ item.value }}
</div>

</template>

<script>
export default {
  props: ['item', 'check'],
  methods: {
    toggle: function() {
      this.item.selected = !this.item.selected;
      this.check();
    },
    toggleLock: function(item) {
      this.item.locked = this.item.locked ? false : true;
    }
  }

}
</script>

<style scoped>
.cell {
  width: 45px;
  text-align: center;
  margin: 5px;
  border-radius: 50%;
  border: 1px solid grey;
  line-height: 40px;
}
.selected {
  background-color: lightgreen;
  animation: flip-in .5s;
  cursor: pointer;
}
.deselected {
  background-color: white;
  cursor: pointer;
  animation: flip-out .5s;
}
.locked {
  border: 2px solid black;
}

@keyframes flip-out {
  from {
    transform: rotateY(0deg);
  }
  to {
    transform: rotateY(360deg);
  }
}
@keyframes flip-in {
  from {
    transform: rotateY(360deg);
  }
  to {
    transform: rotateY(0deg);
  }
}

button:focus {
  outline: none;
}

</style>
