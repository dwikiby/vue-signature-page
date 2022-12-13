<template>
  <section>
    <base-card>
      <h2>Signature Testing</h2>
      <form @submit.prevent="submitForm">
        <div class="form-control">
          <label for="merchant-key">Merchant Key</label>
          <input
            type="text"
            id="merchant-key"
            name="merchant-key"
            v-model.trim="enteredMerchantKey"
          />
        </div>
        <div class="form-control">
          <label for="merchant-code">Merchant Code</label>
          <input
            type="text"
            id="merchant-code"
            name="merchant-code"
            v-model.trim="enteredMerchantCode"
          />
        </div>
        <div class="form-control">
          <label for="payment-id">Payment ID</label>
          <input
            type="text"
            id="payment-id"
            name="payment-id"
            v-model.trim="enteredPaymentId"
          />
        </div>
        <div class="form-control">
          <label for="ref-no">Ref No</label>
          <input
            type="text"
            id="ref-no"
            name="ref-no"
            v-model.trim="enteredRefNo"
          />
        </div>
        <div class="form-control">
          <label for="amount">Amount</label>
          <input
            type="number"
            id="amount"
            name="amount"
            v-model.trim="enteredAmount"
          />
        </div>
        <h2>Currency</h2>
        <div class="form-control">
          <input
            type="radio"
            id="currecy-myr"
            value="MYR"
            name="currency"
            v-model="chosenCurrency"
          />
          <label for="currency-myr">MYR</label>
        </div>
        <div class="form-control">
          <input
            type="radio"
            id="currecy-idr"
            value="IDR"
            name="currency"
            v-model="chosenCurrency"
          />
          <label for="currency-idr">IDR</label>
        </div>
        <div class="form-control">
          <input
            type="radio"
            id="currecy-usd"
            value="USD"
            name="currency"
            v-model="chosenCurrency"
          />
          <label for="currency-usd">USD</label>
        </div>
        <div class="form-control">
          <label for="status">Status</label>
          <input
            type="number"
            id="status"
            name="status"
            v-model.trim="enteredStatus"
          />
        </div>
        <p v-if="invalidInput">
          One or more input fields are invalid. Please check your provided data.
        </p>
        <div>
          <base-button>Submit</base-button>
        </div>
      </form>
    </base-card>
  </section>
</template>

<script>
import * as crypto from "crypto";
export default {
  data() {
    return {
      invalidInput: false,
      error: null,
      enteredMerchantKey: "",
      enteredMerchantCode: "",
      enteredPaymentId: "",
      enteredRefNo: "",
      enteredAmount: null,
      chosenCurrency: null,
      enteredStatus: null,
      signature: "",
      hashSignature: "",
    };
  },
  emits: ["signature-submit"],
  methods: {
    submitForm() {
      if (this.enteredMerchantKey === "" || !this.chosenCurrency) {
        this.invalidInput = true;
        return;
      }
      this.invalidInput = false;

      this.signature =
        this.enteredMerchantKey +
        this.enteredMerchantCode +
        this.enteredPaymentId +
        this.enteredRefNo +
        this.enteredAmount +
        this.chosenCurrency +
        this.enteredStatus;

      console.log(this.signature);

      this.hashSignature = crypto
        .createHash("sha256")
        .update(this.signature)
        .digest("hex");

      console.log(this.hashSignature);
      this.error = null;
      //   fetch("http://localhost:3000/signature", {
      //     method: "POST",
      //     headers: {
      //       "Content-Type": "application/json",
      //     },
      //     body: JSON.stringify({
      //       fullstring: this.signature,
      //     }),
      //   })
      //     .then((response) => {
      //       if (response.ok) {
      //         this.hashSignature = response.json();
      //         console.log(this.hashSignature);
      //       } else {
      //         throw new Error("Could not hash signature data!");
      //       }
      //     })
      //     .catch((error) => {
      //       console.log(error);
      //       this.error = error.message;
      //     });

      this.$emit("signature-submit", {
        signature: this.signature,
        hashsignature: this.hashSignature,
      });

      this.enteredMerchantKey = "";
      this.enteredMerchantCode = "";
      this.enteredPaymentId = "";
      this.enteredRefNo = "";
      this.enteredAmount = null;
      this.chosenCurrency = null;
      this.enteredStatus = null;
      this.signature = "";
      this.hashSignature = "";
    },
  },
};
</script>

<style scoped>
.form-control {
  margin: 0.5rem 0;
}

input[type="text"],
input[type="number"] {
  display: block;
  width: 20rem;
  margin-top: 0.5rem;
}
</style>
