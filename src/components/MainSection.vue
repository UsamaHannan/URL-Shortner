<template>
  <!--TOKEN-->
  <!--pez4ouCIXw5N7dSfsZbM15DGQYBMVBFbWD5qi527WDOkqseeRIzG98dTK1k5-->
  <div>
    <div class="searchbox-wrap">
      <input type="text" placeholder="Shorten Your Link" v-model="url" />
      <button @click="Shorten()">
        <span>Shorten <v-icon color="white">mdi-autorenew</v-icon></span>
      </button>
    </div>
    <v-container>
      <v-alert
        border="left"
        color="red lighten-2"
        dark
        class="mt-5"
        v-show="response"
      >
        {{ response }}
      </v-alert>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "MainSection",

  data() {
    return {
      url: "",
      response: "",
    };
  },

  methods: {
    Shorten() {
      const url = new URL("https://t.ly/api/v1/link/shorten");

      const params = {
        api_token:
          "pez4ouCIXw5N7dSfsZbM15DGQYBMVBFbWD5qi527WDOkqseeRIzG98dTK1k5",
      };
      Object.keys(params).forEach((key) =>
        url.searchParams.append(key, params[key])
      );

      const headers = {
        "Content-Type": "application/json",
        Accept: "application/json",
      };

      let body = {
        long_url: this.url,

        include_qr_code: false,
      };

      fetch(url, {
        method: "POST",
        headers,
        body: JSON.stringify(body),
      })
        .then((response) => response.json())
        .then((data) => {
          this.response = data.short_url;
        });
    },
  },
};
</script>
<style>
* {
  outline: none;
}

body {
  background-color: #607d8b;
}

.searchbox-wrap {
  display: flex;
  width: 500px;
  margin-top: 8%;
  margin-left: auto;
  margin-right: auto;
}
input {
  flex: 1;
  padding: 30px 20px;
  font-size: 1.1em;

  -webkit-border-top-left-radius: 25px;
  -webkit-border-bottom-left-radius: 25px;
  -moz-border-radius-topleft: 25px;
  -moz-border-radius-bottomleft: 25px;
  border-top-left-radius: 25px;
  border-bottom-left-radius: 25px;
  box-shadow: none;
  border: none;
  box-shadow: 2px 4px 6px rgba(0, 0, 0, 0.19);
}

button {
  padding-right: 10px;

  background-color: #fff;
  -webkit-border-top-right-radius: 25px;
  -webkit-border-bottom-right-radius: 25px;
  -moz-border-radius-topright: 25px;
  -moz-border-radius-bottomright: 25px;
  border-top-right-radius: 25px;
  border-bottom-right-radius: 25px;
  box-shadow: 5px 4px 6px rgba(0, 0, 0, 0.19);
  border: none;
  cursor: pointer;
  cursor: hand;
}
span {
  margin-left: 50px;
  padding: 24px 45px;

  font-size: 0.9em;
  text-transform: uppercase;
  font-weight: 300;
  color: #fff;
  background-color: #2a3b4d;

  border-radius: 20px;
  box-shadow: 2px 4px 6px rgba(0, 0, 0, 0.19);
}
</style>
