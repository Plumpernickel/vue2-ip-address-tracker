<template>
  <div>
    <div class="form-group">
      <input v-model.lazy="searchValue" placeholder="Search for any IP address or domain" />
      <button :disabled="asyncState === 'LOADING'" @click="fetchIpData">
        <img src="../assets/icon-arrow.svg" alt="Search button icon" />
      </button>
    </div>
    <div class="card-panel" v-if="asyncState === 'IDLE'">
      <div
        v-for="(key, index) in Object.keys(ipData)"
        :key="index"
        :class="{ 'border-right': index < Object.keys(ipData).length - 1 }">
        <p class="title-secondary">{{key.toUpperCase()}}</p>
        <h3>{{ipData[key]}}</h3>
      </div>
    </div>
    <div class="card-panel error" v-if="asyncState === 'ERROR'">
      <span>An error has occured: {{ipData}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IpForm',
  data() {
    return {
      asyncState: 'IDLE',
      ipData: {},
      searchValue: '',
    };
  },
  methods: {
    async fetchIpData() {
      this.asyncState = 'LOADING';
      const resolvedIp = this.searchValue.length
        ? this.searchValue
        : await fetch('https://api.codetabs.com/v1/proxy?quest=http://ip-api.com/json')
          .then((res) => res.json())
          .then((jsonRes) => jsonRes?.query)
          .catch((error) => {
            this.ipData = error.toString();
            this.asyncState = 'ERROR';
          });

      if (this.asyncState !== 'ERROR') {
        await fetch(`https://cors-anywhere.herokuapp.com/https://geo.ipify.org/api/v1?apiKey=${process.env.VUE_APP_IPIFY_TOKEN}&ipAddress=${resolvedIp}`)
          .then((res) => res.json())
          .then((jsonRes) => {
            this.$emit('update:latlng', [jsonRes.location?.lat, jsonRes.location?.lng]);
            this.ipData = this.mapIpResponse(jsonRes);
            this.asyncState = 'IDLE';
          })
          .catch((error) => {
            // eslint-disable-next-line no-console
            console.log(error);
            this.ipData = error.toString();
            this.asyncState = 'ERROR';
          });
      }
    },
    mapIpResponse(ipResponse = {}) {
      return {
        'ip address': ipResponse.ip,
        location: `${ipResponse.location?.city}, ${ipResponse.location?.country} ${ipResponse.location?.postalCode}`,
        timezone: `UTC ${ipResponse.location?.timezone}`,
        isp: ipResponse.isp,
      };
    },
  },
  mounted() {
    this.fetchIpData();
  },
};
</script>

<style lang="scss">
.card-panel {
  background: white;
  border: none;
  border-radius: 12px;
  width: 50vw;
  display: flex;
  position: relative;
  margin: 30px auto;
  z-index: 1000;

  @media screen and (max-width: 667px) {
    flex-direction: column;
    width: 80vw !important;

    div {
      border: none !important;
      margin: 0 !important;
      padding: 0 !important;
      width: 100% !important;
    }
  }

  .border-right {
    border-right: 1px solid lightgrey;
  }

  div {
    margin: 25px 0;
    padding: 0 25px;
    width: 25%;

    .title-secondary {
      font-size: 12px;
      letter-spacing: 1.5px;
      font-weight: 700;
      color: grey;
    }

    h3 {
      font-weight: 500;
    }
  }
}

.error {
  padding: 10px 0;
  color: orangered;
  display: block;
  text-align: center;
}

.form-group {
  button, input {
    border: none;
    padding: 15px 20px;
  }

  button {
    background: black;
    border-top-right-radius: 12px;
    border-bottom-right-radius: 12px;
    cursor: pointer;
  }

  input {
    border-top-left-radius: 12px;
    border-bottom-left-radius: 12px;
    width: 25vw;

    @media screen and (max-width: 667px) {
      width: 55vw;
    }
  }
}
</style>
