<template>
  <signature-form @signature-submit="storeSignature"></signature-form>
  <signature-submit :results="savedSignatureResult"></signature-submit>
</template>

<script>
import SignatureForm from "./components/signature/SignatureForm.vue";
import SignatureSubmit from "./components/signature/SignatureSubmit.vue";
export default {
  components: {
    SignatureForm,
    SignatureSubmit,
  },
  data() {
    return {
      savedSignatureResult: [],
    };
  },
  methods: {
    storeSignature(signatureData) {
      const signatureResult = {
        signature: signatureData.signature,
        id: new Date().toISOString(),
      };
      this.savedSignatureResult.unshift(signatureData);
      console.log(signatureResult);
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}
</style>
