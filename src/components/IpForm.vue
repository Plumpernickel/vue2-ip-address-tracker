<template>
  <div>
    <div class="form-group">
      <input v-model.lazy="searchValue" placeholder="Search for any IP address or domain" />
      <button @click="searchIp">
        <img src="../assets/icon-arrow.svg" alt="Search button icon" />
      </button>
    </div>
    <div class="card-panel">
      <div class="border-right">
        <p class="title-secondary">{{'ip address'.toUpperCase()}}</p>
        <h3>192.212.174.101</h3>
      </div>
      <div class="border-right">
        <p class="title-secondary">{{'location'.toUpperCase()}}</p>
        <h3>Brooklyn, NY 10001</h3>
      </div>
      <div class="border-right">
        <p class="title-secondary">{{'timezone'.toUpperCase()}}</p>
        <h3>UTC -05:00</h3>
      </div>
      <div>
        <p class="title-secondary">{{'isp'.toUpperCase()}}</p>
        <h3>SpaceX Starlink</h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IpForm',
  data() {
    return {
      searchValue: '',
    };
  },
  methods: {
    searchIp() {
      // eslint-disable-next-line no-console
      console.log('yo', this.searchValue);
    },
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
.border-right {
  border-right: 1px solid lightgrey;
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
  }
}
</style>
