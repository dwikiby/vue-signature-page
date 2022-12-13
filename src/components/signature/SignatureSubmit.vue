<template>
  <section>
    <base-card>
      <h2>Submitted Signature</h2>
      <ul>
        <signature-result
          v-for="result in results"
          :key="result.id"
          :signature="result.signature"
          :hashsignature="result.hashsignature"
        ></signature-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SignatureResult from "./SignatureResult.vue";
export default {
  props: ["results"],
  components: {
    SignatureResult,
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
