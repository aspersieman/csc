<template>
  <div id="app">
    <ul id="nav">
        <li class="left"><a href="#">Chris Standard Calendar</a></li>
    </ul>
    <div class="navigation">
        &nbsp;
    </div>
    <div class="center">
        <datepicker
            class="datepicker"
            v-model="date"
        />
        <input type="button" @click="today()" value="Today" />
    </div>
    <small>Click to set the date</small>
    <div class="formatted-date">
        {{ formattedDate }}
        <br/>
        <small class="target-format">{{ targetFormat }}</small>
    </div>

    <div class="chris-container center">
        <div class="container center">
            <img class="animation center" alt="Chris!" src="./assets/chris.png">
        </div>
    </div>
  </div>
</template>

<script>

/* eslint-disable-next-line */
import Datepicker from 'vuejs-datepicker';

export default {
  name: 'App',
  components: {
      Datepicker,
  },
  data() {
      return {
        targetFormat: "DM-YY-MYDY",
        date: new Date(),
      };
  },

  computed: {
      formattedDate: function () {
          const year = String(this.date.getFullYear()).split('');
          const month = String(this.pad(this.date.getMonth() + 1)).split('');
          const day = String(this.pad(this.date.getDate() + 1)).split('');
          return `${day[0]}${month[0]}-${year[0]}${year[1]}-${month[1]}${year[2]}${day[1]}${year[3]}`;
      },
  },

  methods: {
      pad (value) {
          if (String(value).length < 2) {
              return '0' + String(value);
          }
          return value;
      },

      today () {
          this.date = new Date();
      },
  }
}
</script>

<style>
@font-face {
 font-family: '3DumbRegular';
 src: url('./assets/3Dumb-webfont.eot');
 src: local('‚ò∫'), url('./assets/3Dumb-webfont.woff') format('woff'), url('./assets/3Dumb-webfont.ttf') format('truetype');
 font-weight: normal;
 font-style: normal;
}

ul li {
 list-style: none;
 margin-right: 1em;
 font-family: '3DumbRegular', helvetica, sans-serif;
 font-size: 35px;
 padding: 12px; 
}
 
li a {
 color: #544738;
 text-decoration: none;
}
 
li a:hover {
 color: #7eb9be;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

.center {
    display: flex;
    justify-content: center;
}

.chris-container {
    width: 100%;
}
.container {
  margin: 50px;
  position: absolute;
  animation: zoomInZoomOut 5s infinite;
}

.animation {
  width: 216px;
  height: 288px;
  animation: spin 5s;
  animation-duration: 5s;
  animation-timing-function: ease;
  animation-iteration-count: infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes zoomInZoomOut {
  0% {
    transform: scale(1, 1);
  }
  50% {
    transform: scale(1.2, 1.2);
  }
  100% {
    transform: scale(1, 1);
  }
}

small {
    font-size: 10px;
}
.datepicker input {
    width: 100px;
}
.target-format {
    padding-top: -20px;
}
.formatted-date {
    margin-top: 20px;
    font-size: 2em;
}
</style>
