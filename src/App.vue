<template>
  <div class="container">
    <div class="page-header">
      <h1>People</h1>
    </div>
    <loading-screen ref="loadingScreen">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Id</th>
            <th>Name</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="obj in objects">
            <td>{{obj.id}}</td>
            <td>{{obj.name}}</td>
          </tr>
        </tbody>
      </table>
    </loading-screen>
    <div class="page-footer">
      <button type="button" class="btn btn-default" @click="refresh">Refresh</button>
      <button type="button" class="btn btn-default" @click="addPerson">Add person</button>
    </div>
  </div>
</template>

<script>
import LoadingScreen from 'vue-loading-screen';
import Chance from 'chance';

const chance = new Chance();

export default {
  components: {
    LoadingScreen,
  },
  data() {
    return {
      objects: [],
    };
  },
  methods: {
    refresh() {
      const p = new Promise((success) => {
        setTimeout(success, 500);
      });

      this.$refs.loadingScreen.load(p);

      p.then(() => {
        this.objects = [
          { id: 0, name: 'Foo' },
          { id: 1, name: 'Bar' },
        ];
      });
    },
    addPerson() {
      const p = new Promise((success) => {
        setTimeout(success, 500);
      });

      this.$refs.loadingScreen.load(p);

      p.then(() => {
        this.objects.push({ id: this.objects.length, name: chance.first() });
      });
    },
  },
  created() {
    this.$nextTick(() => {
      this.refresh();
    });
  },
};
</script>
