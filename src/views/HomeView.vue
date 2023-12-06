<template>
  <div>
    <i>{{ quote }}</i>
    <p>Kanye West</p>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const quote = ref("");

    const apiUrl = "https://api.kanye.rest/";
    onMounted(() => {
      fetch(apiUrl)
        .then((response) => {
          if (!response.ok) {
            throw new Error(`Network response was not ok: ${response.status}`);
          }
          return response.json();
        })
        .then((data) => {
          quote.value = data.quote;
        })
        .catch((error) => {
          console.error("Error fetching data:", error.message);
        });
    });
    return {
      quote,
    };
  },
};
</script>
