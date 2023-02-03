<template>
  <div class="d-flex justify-content-center m-5" data-bs-theme="dark">
    <div>
      <LoaderComp v-if="isLoading" />

      <ul v-else-if="tags.length">
        <li v-for="elem in tags" :key="elem.id" class="border-top p-2">
          <router-link :to="`/tags/${elem.name}`">
            {{ elem.name }}
          </router-link>
        </li>
      </ul>
      <p v-else>Non ci sono tags</p>
    </div>
  </div>
</template>

<script>
import LoaderComp from "../LoaderComp.vue";

export default {
  name: "TagsList",
  components: {
    LoaderComp,
  },
  data() {
    return {
      tags: [],
      isLoading: false,
    };
  },
  mounted() {
    this.getTags();
  },
  methods: {
    getTags() {
      this.isLoading = true;
      axios
        .get("http://localhost:8000/api/tags")
        .then((res) => {
          this.tags = res.data;
          console.log(this.tags);
        })
        .catch((err) => {
          console.log(err);
        })
        .then(() => {
          this.isLoading = false;
        });
    },
  },
};
</script>

