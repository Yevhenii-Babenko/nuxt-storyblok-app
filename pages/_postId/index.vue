<template>
    <div>
        <h2></h2>
        <p></p>
    </div>
</template>

<script>

export default {
    asyncData(context) {
        return context.app.$storyapi.get('cdn/stories/blog/posts/' + context.params.postId, {
            version: 'draft'
        })
        .then(response => {
            console.log(response.data)
        })
    }
}

</script>
