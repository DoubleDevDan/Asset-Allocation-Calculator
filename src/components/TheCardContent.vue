<template>
  <div class="card-content">
    <form @submit.prevent="submitForm">
      <div class="form-row">
        <label for="investable-assets">Investable Assets:</label>
        <input
          id="investable-assets"
          type="text"
          v-model="investableAssets"
          required
          pattern="^\$?[0-9]+(\.[0-9][0-9])?$"
          title="Please enter a valid amount in USD (e.g. $1000.00)"
        />
      </div>
      <div class="form-row">
        <button type="submit">Submit</button>
      </div>
      <div class="form-row">
        <div class="btc-allocation">
          <label for="btc-allocation">70% BTC Allocation:</label>
          <input
            id="btc-allocation"
            type="number"
            v-model="btcAllocation"
            required
            readonly
          />
        </div>
        <div class="eth-allocation">
          <label for="eth-allocation">30% ETH Allocation:</label>
          <input
            id="eth-allocation"
            type="number"
            v-model="ethAllocation"
            required
            readonly
          />
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      investableAssets: null,
      btcAllocation: null,
      ethAllocation: null,
    };
  },
  methods: {
    async submitForm() {
      const response = await fetch(
        'https://api.coinbase.com/v2/exchange-rates'
      );
      const data = await response.json();
      if (this.investableAssets.typeof !== 'number') {
        this.investableAssets = Number(
          this.investableAssets.replace(/[^0-9.-]+/g, '')
        );
      }
      this.btcAllocation = data.data.rates.BTC * (this.investableAssets * 0.7);
      this.ethAllocation = data.data.rates.ETH * (this.investableAssets * 0.3);
    },
  },
};
</script>

<style>
.card-content {
  margin: 20px 10px 40px 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-row {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 10px;
}

.btc-allocation {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-right: 10px;
}

.eth-allocation {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  margin-left: 10px;
}

button {
  margin-top: 10px;
}

input {
  outline: 0;
  border-width: 0 0 2px;
  border-color: 15246D;
  padding: 5px 10px;
}
input:focus {
  border-color: #017a4e;
  outline: 1px dotted #b6e5ff;
}

[placeholder]:focus::-webkit-input-placeholder {
  transition: text-indent 0.4s 0.4s ease;
  text-indent: -100%;
  opacity: 1;
}
</style>
