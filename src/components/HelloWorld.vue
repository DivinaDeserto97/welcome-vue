<template>
  <div id="hw">
    <header>
      <h1> {{ titel }} </h1>
      <h2>{{ currDate }}</h2>
    </header>
    <section>
      <ul v-if="kurse">
        <li v-for="kurs in kurse" :key="kurs.id">
          <span id="kurs-time">{{ kurs[1] }} - {{ kurs[0] }} Uhr</span><br>
          <h3 id="kurs-titel">{{ kurs[2] }}</h3>
          <span id="kurs-desciption">{{ kurs[3] }}</span>
        </li>
      </ul>
    </section>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <footer>
      <div class="footer-wrapper">
        <div class="footer-item">
          <img src="./../assets/drive-download-20230301T081902Z-001/STZH_SEB_Logo.png" alt="Image 1">
        </div>
        <div class="footer-item">
          <img src="./../assets/drive-download-20230301T081902Z-001/Opportunity.png" alt="Image 2">
        </div>
        <div class="footer-item">
          <img src="./../assets/drive-download-20230301T081902Z-001/SAG_Logo_De.png" alt="Image 3">
        </div>
      </div>
    </footer>
  </div>
</template>

<script>

export default {
  data() {
    return {
      titel: 'Welcome to Opportunity',
      currDate: '00.00.1234',
      kurse: [
        ['1', '2', '3', '4'],
        ['a', 'b', 'c', 'd']
      ]
    }
  },
  methods: {
    getData() {
      this.kurse = null,/* [
        ['14:00', '0.1.2030', 'Basisbeschaftigung Besuch', 'intressierte für den zweiten Kurs werden uns besuchen'],
        ['14:00', '0.1.2030', 'Basisbeschaftigung Besuch', 'intressierte für den zweiten Kurs werden uns besuchen'],
      ] */
    },
    currentDate() {
      const current = new Date();
      const d = current.getDate();
      const m = current.getMonth() + 1;
      const year = current.getFullYear();
      const min = current.getMinutes();
      const h = current.getHours();


      let day;
      let month;
      let minuten;
      let stunden;

      if (d < 10) {
        day = '0' + d;
      } else {
        day = d;
      }
      if (m < 10) {
        month = '0' + m;
      } else {
        month = m;
      }
      if (min < 10) {
        minuten = '0' + min;
      } else {
        minuten = min;
      }
      if (h < 10) {
        stunden = '0' + h;
      } else {
        stunden = h;
      }

      this.currDate = day + '.' + month + '.' + year + ' - ' + stunden + ':' + minuten;
    },
    refreshData() {
      this.getData();
      this.currentDate();
    }
  },
  mounted() {
    this.refreshData();
    setInterval(this.refreshData, 1000);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap%22");

#hw {
  font-family: "Inter", Arial, Helvetica, sans-serif;

}

body {
  color: #E5E5E5;
}

h1 {
  margin-left: 60px;

  text-align: left;
  font-weight: 900;
  font-size: 62px;
  left: 60px;

  color: #323D4A;
}

h2 {
  margin-left: 60px;
  text-align: left;
  font-weight: 500;
  font-size: 62px;

  color: #9AA7B1;
}

ul {
  list-style-type: none;
}

li {
  width: 900px;
  height: 112px;

  padding: 37px;
  margin: 20px;

  font-weight: 900;
  font-size: 28px;
  line-height: 10px;

  text-align: left;
  background-color: #0F05A0;
}

#kurs-time {
  color: #EB5E00;
}

#kurs-titel {
  color: #FFBFAB;
}

#kurs-desciption {
  color: #FFBFAB;
}

footer {
  background-color: white;
  padding: 20px;
  position: fixed;
  bottom: 0;
  z-index: 1;
}

.footer-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 100%;
  margin: 0 auto;
}

.footer-item {
  flex-basis: calc(33.33% - 20px);
  text-align: center;
}

.footer-item img {
  max-width: 100%;
}
</style>
