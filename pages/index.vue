<template>
  <div
    class="container"
    style="
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    "
  >
    <h1>Hello world</h1>
    <NuxtLink
      v-for="post in posts"
      :key="post.id"
      :to="{ name: 'postId', params: { postId: post.slug } }"
    >
      <section>
        <h1>{{ post.title }}</h1>
        <p>{{ post.content }}</p>
        <img
          :src="post.img"
          alt="bunner"
          style="width: 400px; height: 400px; object-fit: contain"
        />
      </section>
    </NuxtLink>
  </div>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "blog/",
      })
      .then((response) => {
        return {
          posts: response.data.stories.map((post) => {
            console.log(post);
            return {
              slug: post.slug,
              id: post.id,
              content: post.content.postBody,
              title: post.content.title,
              img: post.content.imgArea,
            };
          }),
        };
      });
  },
};
</script>