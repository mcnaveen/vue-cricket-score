<template>
  <div class="container">
    <div>
      <br />
      <br />
      <section class="section">
        <div class="container">
          <div class="columns is-centered">
            <div class="column is-half">
              <h1 class="title has-text-warning has-text-centered">
                Live Score 🏏
              </h1>
              <p
                class="has-text-success has-text-weight-bold has-text-centered"
              >
                Click Refresh Button to Get Real-time Live Cricket Score
                Updates.
              </p>
              <br />
              <div
                class="content table table is-bordered table is-striped table is-narrow table is-hoverable"
              >
                <table v-if="results.current !== 'Data Not Found'">
                  <tbody>
                    <tr>
                      <th>🏏</th>
                      <td v-if="results.title === 'Data Not Found'">
                        {{ loading ? "Loading Match data" : "No Live Match" }}
                      </td>
                      <td v-else>
                        {{ loading ? "Loading Match data" : results.title }}
                      </td>
                    </tr>
                    <tr>
                      <th>📊</th>
                      <td v-if="results.update === 'Data Not Found'">
                        {{ loading ? "Loading Match data" : "No Live Match" }}
                      </td>
                      <td v-else>
                        {{ loading ? "Loading Match data" : results.update }}
                      </td>
                    </tr>
                    <tr>
                      <th>🔴</th>
                      <td v-if="results.current === 'Data Not Found'">
                        {{ loading ? "Loading Match data" : "No Live Match" }}
                      </td>
                      <td v-else>
                        {{ loading ? "Loading Match data" : results.current }}
                      </td>
                    </tr>
                    <tr>
                      <th>📉</th>
                      <td v-if="results.runrate === 'Data Not Found'">
                        {{ loading ? "Loading Match data" : "No Live Match" }}
                      </td>
                      <td v-else>
                        {{ loading ? "Loading Match data" : results.runrate }}
                      </td>
                    </tr>
                    <tr>
                      <th>✊</th>
                      <td v-if="results.batsman === 'Data Not Found'">
                        {{ loading ? "Loading Match data" : "No Live Match" }}
                      </td>
                      <td v-else>
                        {{ loading ? "Loading Match data" : results.batsman }}
                        {{
                          loading ? "" : "\t" + "-" + "\t" + results.batsmanrun
                        }}{{ loading ? "" : results.ballsfaced }}
                      </td>
                    </tr>
                    <tr>
                      <th>✊</th>
                      <td v-if="results.bowler === 'Data Not Found'">
                        {{ loading ? "Loading Match data" : "No Live Match" }}
                      </td>
                      <td v-else>
                        {{ loading ? "Loading Match data" : results.bowler }}
                        {{
                          loading ? " " : "\t" + "-" + "\t" + results.bowlerover
                        }}
                        {{ loading ? " " : "Over" + "\t" + results.bowlerruns }}
                        {{
                          loading
                            ? " "
                            : "Run and" +
                              "\t" +
                              results.bowlerwickets +
                              "\t" +
                              "Wicket"
                        }}
                      </td>
                    </tr>
                    <tr>
                      <th>😳</th>
                      <td v-if="results.lastwicket === 'Data Not Found'">
                        {{ loading ? "Loading Match data" : "No Live Match" }}
                      </td>
                      <td v-else>
                        {{
                          loading ? "Loading Match data" : results.lastwicket
                        }}
                      </td>
                    </tr>
                  </tbody>
                </table>
                <table v-else-if="results.current === 'Data Not Found'">
                  <tbody>
                    <tr>
                      <td>
                        <p class="has-text-centered">
                          {{
                            loading
                              ? "Loading Match data"
                              : "🔴 Sorry Currently No Live Match"
                          }}
                        </p>
                      </td>
                    </tr>
                  </tbody>
                </table>
                <table v-else>
                  <tbody>
                    <tr>
                      <td>
                        <p class="has-text-centered">
                          {{
                            loading
                              ? "Loading Match data"
                              : "🔴 No Live Match Data"
                          }}
                        </p>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <div class="buttons is-centered">
                <button
                  class="button is-warning pwa-button"
                  @click.prevent="getResult"
                >
                  {{ loading ? "🔄 Updating Score" : "🔄 Refresh Score" }}
                </button>
              </div>
              <br />
              <br />
              <div class="notification is-warning">
                <br />
                <p class="has-text-weight-bold has-text-centered">
                  Our Free Telegram Bot Just start and Get Live Score Update.
                  <br />
                  <br />
                  <span class="buttons is-centered">
                    <a
                      href="https://telegram.me/livecriscore_bot"
                      class="button is-danger read-random"
                      target="_blank"
                      rel="nofollow noopener"
                      >🤖 Start Bot</a
                    >
                  </span>
                  <br />
                  This Web App was Dedicated to Cricket Lovers 💚<br />
                  Scores are Fetched from Cricbuzz - Unofficial API Data.
                </p>
                <br />
                <div class="buttons is-centered">
                  <a
                    href="https://github.com/mskian/vue-cricket-score"
                    class="button is-success read-random"
                    target="_blank"
                    rel="nofollow noopener"
                    >📦 Souce Code</a
                  >
                  <a
                    href="https://github.com/mskian/cricket-api"
                    class="btn button is-link read-random"
                    target="_blank"
                    rel="nofollow noopener"
                    >🗃 API Data</a
                  >
                </div>
                <br />
              </div>
              <br />
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Score",
  data() {
    return {
      results: {},
      loading: false,
      info: null,
    };
  },
  mounted() {
    this.getResult();
  },
  methods: {
    getResult() {
      this.loading = true;
      axios
        .get(
          "https://cricket-api.vercel.app/cri.php?url=https://m.cricbuzz.com/live-cricket-scores/" +
            this.$route.query.match
        )
        .then((response) => {
          this.results = response.data.livescore;
          this.loading = false;
        });
    },
  },
};
</script>

<style>
h1 {
  font-weight: 700;
  font-size: 23px;
}
h2 {
  font-weight: 700;
  font-size: 21px;
}
h3 {
  font-weight: 700;
  font-size: 20px;
}
h4 {
  font-weight: 700;
  font-size: 18px;
}
h5 {
  font-weight: 700;
  font-size: 18px;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  color: #050505;
  word-wrap: break-word;
  -webkit-hyphens: auto;
  -moz-hyphens: auto;
  -ms-hyphens: auto;
  -o-hyphens: auto;
  hyphens: auto;
}
.title {
  color: #d9ee1c;
  font-weight: 700;
}
a:hover,
a:focus,
a:active {
  color: #010508;
}
.content a {
  color: #ffffff;
}
.notice {
  max-width: 25rem;
}
.input-box,
textarea,
.sign-button {
  width: 45rem !important;
  min-height: 3rem;
}
button {
  max-width: 100%;
}
.pwa-button {
  font-family: "Fira Code", monospace;
  font-weight: 700;
  font-size: 14px;
  text-transform: uppercase;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  border-radius: 32px;
  padding: 12px;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased !important;
  -moz-font-smoothing: antialiased !important;
  text-rendering: optimizelegibility !important;
  width: 12rem !important;
  min-height: 2.2rem;
}
.pwa-buttons {
  font-family: "Fira Code", monospace;
  font-weight: 700;
  font-size: 14px;
  text-transform: uppercase;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  border-radius: 32px;
  padding: 12px;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased !important;
  -moz-font-smoothing: antialiased !important;
  text-rendering: optimizelegibility !important;
  width: 10rem !important;
  min-height: 2.2rem;
}
table {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  padding: 12px;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased !important;
  -moz-font-smoothing: antialiased !important;
  text-rendering: optimizelegibility !important;
  border-bottom: 2px solid #bbb !important;
  background-color: #d3d3d3;
}
th {
  white-space: nowrap;
}
.cooked table thead,
.d-editor-preview table thead {
  border-bottom: 2px solid #bbb !important;
  background-color: #d3d3d3;
}
.cooked table tr,
.d-editor-preview table tr {
  border-bottom: 1px solid #bbb;
}
.is-horizontal-center {
  justify-content: center;
}
.buttonpwa {
  display: inline-flex;
  margin: 4px 0;
  padding: 8px 16px;
  border-radius: 4px;
  background-color: rgb(253, 98, 37);
  color: #fff;
  font-size: 18px;
  cursor: pointer;
  align-items: center;
  justify-content: center;
  flex-grow: 1;
}
.buttonpwa:hover {
  background-color: rgb(248, 221, 68);
}
.content h1 {
  font-size: 21px;
  font-weight: 700;
}
.content h2 {
  font-size: 21px;
  font-weight: 700;
}
.content h3 {
  font-size: 20px;
  font-weight: 700;
}
.content h4 {
  font-size: 18px;
  font-weight: 700;
}
.read-random {
  display: flex;
  flex-grow: 0.3;
  font-family: "Fira Code", monospace;
  font-weight: 800;
  font-size: 13px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  border-radius: 32px;
  padding: 10px;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased !important;
  -moz-font-smoothing: antialiased !important;
  text-rendering: optimizelegibility !important;
}
</style>
