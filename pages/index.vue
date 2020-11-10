<template lang="pug">
    section.section
        .container
            .columns.is-multiline
                .column.is-one-quarter(
                    v-for="(article, index) in articles"
                    key="index"
                )
                    a(
                        :href="article.url"
                        target="_blank"
                    )
                        .card
                            .card-image
                                figure.image.is-3by2
                                    img(
                                        :src="article.urlToImage"
                                        :alt="article.title"
                                    )
                            .card-content
                                .content {{ article.title }}
</template>

<script>

export default {
    async asyncData({ app }){
        const { articles } = await app.$axios.$get(
            `https://newsapi.org/v2/top-headlines?sources=cnn&apiKey=${
                    process.env.API_KEY
                }`
        );
        return { articles };
    }
}
</script>
