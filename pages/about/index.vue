<template>
  <section v-editable="blok">
    <h2>{{ title }}</h2>
    <p>{{ content }}</p>
  </section>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories/about", {
        version: "draft",
      })
      .then((response) => {
        console.log(response.data);
        return {
          blok: response.data.story.content,
          title: response.data.story.content.title,
          content: response.data.story.content.content,
        };
      });
  },
  mounted() {
    this.$storybridge(() => {
      const storyblokInstance = new StoryblokBridge();

      storyblokInstance.on("input", (event) => {
        if (Object.is(event.story.id, this.story.id)) {
          this.story.content = event.story.content;
        }
      });
      storyblokInstance.on(["published", "change"], (event) => {
        this.$nuxt.$router.go({
          path: this.$nuxt.$router.currentRoute,
          force: true,
        });
      });
    });
  },
};
</script>
