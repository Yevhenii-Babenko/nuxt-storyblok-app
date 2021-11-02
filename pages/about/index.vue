<template>
  <section>
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
          console.log(response.data)
        return {
          title: response.data.story.content.title,
          content: response.data.story.content.content,
        };
      });
  },
};
</script>
