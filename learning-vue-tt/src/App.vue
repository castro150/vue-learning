<template>
<div id="app">
  <nav class="navbar navbar-default">
    <div class="container">
      <a class="navbar-brand" href="#">
        <i class="glyphicon glyphicon-time"></i>
        Vue Time Tracker
      </a>
      <ul class="nav navbar-nav">
        <li>
          <router-link :to="'/home'">Home</router-link>
        </li>
        <li>
          <router-link :to="'/time-entries'">Time Entries</router-link>
        </li>
      </ul>
    </div>
  </nav>
  <div class="container">
    <div class="col-sm-3">
      <sidebar :time="totalTime"></sidebar>
    </div>
    <div class="col-sm-9">
      <router-view></router-view>
    </div>
  </div>
</div>
</template>

<script>
import Sidebar from './components/Sidebar.vue'

export default {
  components: {
    'sidebar': Sidebar
  },
  data() {
    return {
      // Start with the same value as our
      // first time entry. Hard-coded for now
      // because we'll use a different approach
      // in the next article anyway
      totalTime: 1.5
    }
  },
  created() {
    Event.$on('time-update', timeEntry => {
      this.totalTime += parseFloat(timeEntry.totalTime)
      return true
    });

    Event.$on('delete-time', timeEntry => {
      this.totalTime -= parseFloat(timeEntry.totalTime)
      return true
    });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
