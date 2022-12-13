<template>
  <li>
    <p>
      Fullstring:<span class="highlight">{{ signature }}</span>
    </p>
    <p>
      Hash Signature: <span class="highlight">{{ hashsignature }}</span>
    </p>
  </li>
</template>

<script>
export default {
  props: ["signature", "hashsignature"],
};
</script>

<style scoped>
li {
  margin: 1rem 0;
  border: 1px solid #ccc;
  padding: 1rem;
}

h3,
p {
  font-size: 1rem;
  margin: 0.5rem 0;
}

.highlight {
  font-weight: bold;
}
</style>
