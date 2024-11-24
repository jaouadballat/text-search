<template>
    <div id="app">
        <h1>Search</h1>
        <input type="text" v-model="searchQuery" placeholder="Type to search...">
        <p>{{ filtredArticles.length }} posts where found.</p>
        <div v-for="(article, index) in filtredArticles" :key="index">
            <h3 v-html="highlightedText(article.title)"></h3>
            <p v-html="highlightedText(article.content)"></p>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                searchQuery: '',
                articles: [
                    {
                        id: 1,
                        title: 'Article 1',
                        content: 'Content of article 1',
                    },
                    {
                        id: 2,
                        title: 'Article 2',
                        content: 'Content of article 2',
                    },
                    {
                        id: 3,
                        title: 'Article 3',
                        content: 'Content of article 3',
                    },
                ],
            }
        },
        computed: {
            filtredArticles() {
                if(!this.searchQuery) return this.articles;
                const showLower = this.searchQuery.toLowerCase();
                return this.articles.filter((article) => {
                    return article.content.toLowerCase().includes(showLower) || article.title.toLowerCase().includes(showLower);
                });
        }
        },
        methods: {
            highlightedText(text) {
                if (!this.searchQuery) return text;
                const regex = new RegExp((`${this.searchQuery}`), 'gi');
                return text.replace(regex, match => `<mark>${match}</mark>`);
            }
        },
    }
</script>
<style>
mark {
    background-color: yellow;
}
</style>