<template>
  <div id="hw">
    <header>
      <h1> {{ titel }} </h1>
      <h2>{{ currDate }}</h2>
    </header>
    <section>

        <ul v-if="kurse && kurse.length">
          <li v-for="kurs in kurse" :key="kurs.id">
            <span id="kurs-time">{{ kurs[0] }} Uhr, {{ kurs[1].replaceAll("/", ".") }}</span><br>
            <h3 id="kurs-titel">{{ kurs[2] }}</h3>
            <span id="kurs-desciption">{{ kurs[3] }}</span>
          </li>
        </ul>

        <h4 v-else>Zur Zeit Keine Events vorhanden</h4>
    </section>
    <div>
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
    </div>
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
import axios from "axios";

export default {
  data() {
    return {
      titel: 'Welcome to Opportunity',
      currDate: '',
      kurse: [],
      sheet_id: "1lXd4Bc_SZcN-UfVhg9eBiLQ2VyXGkQ-rxjsbnIbKwqQ",// Chris 1CR1UKN0LAPNs6lWbfA2gBI2FazmWdVSFIzIwi5TG5Z4
      api_token: "AIzaSyBGazIHrv6U6W3nIx-B4TMXW3puAi6DNrY",// Chris AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU
    }
  },
  computed: {
    // computed properties are like data properties, but with a method combined and it gets executed automatically, instead of calling a function explicitly
    gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
    },
  },
  methods: {
    getData() {
      axios.get(this.gsheet_url).then((response) => {
            // Erhalte die Zeilen aus der Antwort des API-Aufrufs
            const rows = response.data.valueRanges[0].values;
            // Erhalte das aktuelle Datum
            const currentDate = new Date();
            // Filtere die Zeilen, die ein Datum haben, das heute oder sp??ter ist
            const filteredRows = rows.filter(row => {
              // Zerlege das Datum in seine Teile
              const dateParts = row[1].split("/");
              // Erstelle ein neues Datum aus den Datumsteilen
              const rowDate = new Date(`${dateParts[2]}-${dateParts[1]}-${dateParts[0]}`);
              // Vergleiche das neue Datum mit dem aktuellen Datum und gib das Ergebnis zur??ck
              return rowDate >= currentDate;
            });
             // Sortiere die gefilterten Zeilen nach Datum
            this.kurse = filteredRows.sort((row1, row2) => {
              // Zerlege die Datumsteile des ersten Datums (uhr Zeit)in row1
              const dateParts1 = row1[1].split("/");
              // Zerlege die Datumsteile des zweiten Datums (Kalender) in row2
              const dateParts2 = row2[1].split("/");
              // Erstelle neue Datumobjekte aus den Datumsteilen beider Zeilen
              const date1 = new Date(`${dateParts1[2]}-${dateParts1[1]}-${dateParts1[0]}`);
              const date2 = new Date(`${dateParts2[2]}-${dateParts2[1]}-${dateParts2[0]}`);
              // Vergleiche die Datumobjekte und gib das Ergebnis zur??ck
              return date1 - date2;
            });
          });
      /*this.kurse = [
        ["14:00", "01.02.2012", "Kurs1", "beschreibung1"],
        ["14:00", "01.02.2012", "Kurs2", "beschreibung1"],
        ["14:00", "01.02.2012", "Kurs3", "beschreibung1"],
      ],*/
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
    setInterval(this.refreshData, 18000000);
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
  left: 80px 0 20px 0;

  color: #323D4A;
}

h2 {
  margin-left: 60px;
  text-align: left;
  font-weight: 500;
  font-size: 62px;

  color: #9AA7B1;

}

h4 {
  margin-left: 60px;
  text-align: left;
  font-weight: 500;
  font-size: 62px;

  color: #0F05A0;
}

ul {
  list-style-type: none;
}

li {
  padding: 37px 40px;
  margin: 40px 0;

  font-weight: 900;
  font-size: 28px;
  line-height: 1.3;

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
  margin: 0;
}

.footer-item {
  flex-basis: calc(33.33% - 20px);
  text-align: center;
}

.footer-item img {
  max-width: 100%;
}
</style>
