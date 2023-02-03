<template>
  <div class="text-center">

    <h1 class="m-4">{{ tag.name }}</h1>

  </div>
</template>

<script>
export default {
  name: "TagCard",
  components: {},
  data() {
    return {
      tag: null,
    };
  },
  mounted() {
    this.getTag();
  },
  methods: {
    getTag() {
      axios
        .get("http://localhost:8000/api/tags/" + this.$route.params.name)
        .then((res) => {
          console.log(res);
          this.tag = res.data;

        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped lang="scss">
</style>
