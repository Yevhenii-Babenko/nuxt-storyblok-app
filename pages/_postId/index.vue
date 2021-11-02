<template>
  <div>
      <img :src="img" alt="poster">
    <h2>{{ title }}</h2>
    <p>{{ content }}</p>
  </div>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories/" + context.params.postId, {
        version: "draft",
      })
      .then((response) => {
        console.log("this is a post", response.data);
        return {
          title: response.data.story.content.title,
          content: response.data.story.content.postBody,
          img: response.data.story.content.imgArea
        };
      });
  },
};
</script>
