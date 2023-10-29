<template>
  <div id="main-section">
    <loading v-if="loading"></loading>
    <div id="countdown" class="countdown" v-if="countDownNone">
      <div class="countdown-items">
        <h1 class="heading">New Year Countdown</h1>
        <p class="brithdayYear">2024</p>
        <div class="countdown-lists">
          <div class="time">
            <div class="card">
              <h2 id="days">{{ displayDays }}</h2>
              <div class="card-button">
                <small>Days</small>
              </div>
            </div>
          </div>
          <div class="time">
            <div class="card">
              <h2 id="hours">{{ displayHours }}</h2>
              <div class="card-button">
                <small>Hours</small>
              </div>
            </div>
          </div>
          <div class="time">
            <div class="card">
              <h2 id="minutes">{{ displayMinutes }}</h2>
              <div class="card-button">
                <small>Minutes</small>
              </div>
            </div>
          </div>
          <div class="time">
            <div class="card">
              <h2 id="seconds">{{ displaySeconds }}</h2>
              <div class="card-button">
                <small>Seconds</small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Loading from "./components/Loading.vue";
export default {
  data() {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      countDownNone: false,
      loading: true,
    };
  },
  created() {
    setTimeout(() => {
      this.countDownNone = true;
      this.loading = false;
    }, 2000);
  },
  computed: {
    _secends() {
      return 1000;
    },
    _minutes() {
      return this._secends * 60;
    },
    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
  },
  mounted() {
    this.updateCountdown();
  },

  methods: {
    //  Update countdown time
    updateCountdown() {
      const timer = setInterval(() => {
        const currentYear = new Date();

        // Get the next new year's date
        const nextYear =
          currentYear.getFullYear() +
          (currentYear.getMonth() === 0 && currentYear.getDate() === 1 ? 0 : 1);
        const newYearTime = new Date(nextYear, 0, 1, 0, 0, 0, 0);

        // Set background year
        const diff = newYearTime - currentYear;
        if (diff < 0) {
          return clearInterval(timer);
        }
        const d = Math.floor(diff / this._days);
        const h = Math.floor((diff % this._days) / this._hours);
        const m = Math.floor((diff % this._hours) / this._minutes);
        const s = Math.floor((diff % this._minutes) / this._secends);
        // Add values to
        this.displayMinutes = m < 10 ? "0" + m : m;
        this.displaySeconds = s < 10 ? "0" + s : s;
        this.displayHours = h < 10 ? "0" + h : h;
        this.displayDays = d < 10 ? "0" + d : d;
      }, 1000);
    },
  },
  components: {
    Loading,
  },
};
</script>
<style>
/* Reset */
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  margin: 0;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  padding: 20px;
  border-radius: 6px;
  text-align: center;
}
small {
  font-size: 29px;
  color: #5dabcd;
}
h2 {
  font-size: 40px;
  color: #bc2e1e;
  padding-bottom: 20px;
}
.card-buttom {
  padding: 2px 16px;
}
.heading {
  padding: 2rem;
  font-size: 4rem;
  padding-bottom: 20px;
  color: #202c2d;
  text-shadow: 0 1px #808d93, -1px 0 #cdd2d5, -1px 2px #808d93, -2px 1px #cdd2d5,
    -2px 3px #808d93, -3px 2px #cdd2d5, -3px 4px #808d93, -4px 3px #cdd2d5,
    -4px 5px #808d93, -5px 4px #cdd2d5, -5px 6px #808d93, -6px 5px #cdd2d5,
    -6px 7px #808d93, -7px 6px #cdd2d5, -7px 8px #808d93, -8px 7px #cdd2d5;
  color: #202c2d;
}
.brithdayYear {
  text-align: center;
  font-size: 4rem;
  padding: 10px;
  color: #bc2e1e;
  text-shadow: 0 1px 0px #378ab4, 1px 0 0px #5dabcd, 1px 2px 1px #378ab4,
    2px 1px 1px #5dabcd, 2px 3px 2px #378ab4, 3px 2px 2px #5dabcd,
    3px 4px 2px #378ab4, 4px 3px 3px #5dabcd, 4px 5px 3px #378ab4,
    5px 4px 2px #5dabcd, 5px 6px 2px #378ab4, 6px 5px 2px #5dabcd,
    6px 7px 1px #378ab4, 7px 6px 1px #5dabcd, 7px 8px 0px #378ab4,
    8px 7px 0px #5dabcd;
}

#main-section {
  background-image: url("./assets/new-year.png");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  height: 100vh;
}
#countdown {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

/* Animations Sections */
#main-section:before {
  content: "";
  height: 100vh;
  width: 100vw;
  position: absolute;
  top: 0;
  left: 0;
  background: url("./assets/pattern.png");
  opacity: 0.5;
  animation: animate 10s linear infinite;
  z-index: 2;
}
@keyframes animate {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 0 550px;
  }
}
#countdown .countdown-lists {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 1rem;
  margin-top: 3rem;
}

@media screen and (max-width: 780px) {
  #countdown .countdown-lists {
    grid-template-columns: 1fr 1fr;
    grid-gap: unset;
  }
  .heading {
    padding: 0;
    font-size: 3rem;
    text-align: center;
  }
  .brithdayYear {
    padding: 0;
  }
}
</style>
