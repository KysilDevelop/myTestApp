<template>
    <aside class="aside aside--w25">
      <h2 class="aside__title">A place called Inspiration.</h2>
      <p class="aside__text">
        Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non
        numquam eius modi tempora incidunt ut labore et dolore magnam voluptatem.
      </p>
      <div class="aside__controls">
        <select class="aside__select" name="typeChart" id="typeChart" v-model="selected">
          <option v-for="item in list" :value="item.type">{{item.name}}</option>
        </select>
        <button @click="addChart" class="aside__btn">Insert</button>
      </div>
    </aside>
</template>

<script>
  export default {
    name: 'AsideApp',
    data(){
      return{
        selected: ''
      }
    },
    props: ['list'],
    methods: {
      addChart: function() {
        this.$root.$emit('add', this.selected);
      }
    }
  }
</script>

