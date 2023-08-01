<template>
  <form @submit.prevent="submitForm" class="form">
    <div class="form-row investable-assets-row">
      <label for="investable-assets">Investable Assets:</label>
      <div class="input-group flex-nowrap">
        <input
          id="investable-assets"
          type="text"
          v-model="investableAssets"
          required
          pattern="^\$?[0-9]+(\.[0-9][0-9])?$"
          title="Please enter a valid amount in USD (e.g. $1000.00)"
          ref="investableAssetsInput"
          class="investable-assets-input form-control"
        />
        <span class="input-group-text">
          <select
            id="asset-currency"
            v-model="assetCurrency"
            @change="updateCurrencyRates"
            class="form-control"
          >
            <option value="USD">USD</option>
            <option value="BTC">BTC</option>
            <option value="ETH">ETH</option>
          </select>
        </span>
      </div>
    </div>
    <div class="form-row">
      <input
        id="opt1-allocation-percentage"
        type="range"
        min="0"
        max="100"
        v-model="opt1AllocationPercentage"
        required
        class="input-range"
      />
    </div>
    <div class="form-row allocation-row">
      <label id="opt1-allocation">
        {{ opt1AllocationPercentage }}%
        <select v-model="opt1Currency" @change="updateCurrencyRates">
          <option value="BTC">BTC</option>
          <option value="ETH">ETH</option>
          <option value="USD">USD</option>
        </select>
        Allocation</label
      >

      <label id="opt2-allocation">
        {{ opt2AllocationPercentage }}%
        <select v-model="opt2Currency" @change="updateCurrencyRates">
          <option value="BTC">BTC</option>
          <option value="ETH">ETH</option>
          <option value="USD">USD</option>
        </select>
        Allocation
      </label>
    </div>
    <div class="form-row">
      <button type="submit">Submit</button>
    </div>
    <div class="form-row">
      <hr class="divider" />
    </div>
    <div class="form-row allocation-row">
      <div class="opt1-allocation">
        <div class="f">
          <div class="form-row">{{ assetCurrency }} : {{ opt1Currency }}</div>
          <div class="form-row">1 : {{ opt1CurrencyRate }}</div>
        </div>
        <div>
          <div class="form-row">
            {{ opt1AllocationPercentage }}% Allocation:
          </div>
          <div class="form-row">
            <div v-if="!opt1Allocation">
              <p>Awaiting submit...</p>
            </div>
            {{ opt1Allocation }}
          </div>
          <div class="form-row">{{ opt1Currency }}</div>
        </div>
      </div>
      <div class="opt2-allocation">
        <div class="f">
          <div class="form-row">{{ assetCurrency }} : {{ opt2Currency }}</div>
          <div class="form-row">1 : {{ opt2CurrencyRate }}</div>
        </div>
        <div>
          <div class="form-row">
            {{ opt2AllocationPercentage }}% Allocation:
          </div>
          <div class="form-row">
            <div v-if="!opt2Allocation">
              <p>Awaiting submit...</p>
            </div>
            {{ opt2Allocation }}
          </div>
          <div class="form-row">{{ opt2Currency }}</div>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      investableAssets: null,
      opt1AllocationPercentage: 70,
      opt2AllocationPercentage: 30,
      opt1Allocation: null,
      opt2Allocation: null,
      opt1Currency: 'BTC',
      opt2Currency: 'ETH',
      opt1CurrencyRate: null,
      opt2CurrencyRate: null,
      assetCurrency: 'USD',
    };
  },
  methods: {
    async submitForm() {
      const response = await fetch(
        'https://api.coinbase.com/v2/exchange-rates?currency=' +
          this.assetCurrency
      );
      const data = await response.json();

      const opt1AllocationDecimal = this.opt1AllocationPercentage / 100;
      const opt2AllocationDecimal = this.opt2AllocationPercentage / 100;
      this.opt1Allocation =
        this.opt1CurrencyRate * (this.investableAssets * opt1AllocationDecimal);
      this.opt2Allocation =
        this.opt2CurrencyRate * (this.investableAssets * opt2AllocationDecimal);

      // Update opt1CurrencyRate and opt2CurrencyRate
      await this.updateOpt1CurrencyRate();
      await this.updateOpt2CurrencyRate();
    },
    async updateCurrencyRates() {
      const response = await fetch(
        `https://api.coinbase.com/v2/exchange-rates?currency=${this.assetCurrency}`
      ).then((response) => response.json());

      console.log(response);
      this.opt1CurrencyRate = response.data.rates[this.opt1Currency];
      this.opt2CurrencyRate = response.data.rates[this.opt2Currency];
    },
  },
  watch: {
    opt1AllocationPercentage(newVal) {
      this.opt2AllocationPercentage = 100 - newVal;
    },
    opt2AllocationPercentage(newVal) {
      this.opt1AllocationPercentage = 100 - newVal;
    },
  },
  created() {
    this.updateCurrencyRates();
  },
  mounted() {
    this.$refs.investableAssetsInput.focus();
  },
};
</script>

<style>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.form-row {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 10px;
  width: 100%;
}

.investable-assets-row {
  font-size: 24px;
  font-weight: bold;
}

.asset-currency-row {
  font-size: 18px;
}

.allocation-row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-bottom: 20px;
}

.flex-nowrap {
  width: 100%;
}

button {
  margin-top: 10px;
  font-size: 18px;
  font-weight: bold;
  padding: 10px 20px;
  width: 100%;
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

.input-range {
  width: 100%;
}

.investable-assets-input {
  font-size: 24px;
  text-align: center;
}

.divider {
  width: 100%;
  border: 1px solid #8a73e5;
  margin: 20px 0;
}

[placeholder]:focus::-webkit-input-placeholder {
  transition: text-indent 0.4s 0.4s ease;
  text-indent: -100%;
  opacity: 1;
}
</style>
