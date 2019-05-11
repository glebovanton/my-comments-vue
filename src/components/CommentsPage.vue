<template>
    <div class="comments-page">
        <div class="main-img"  :style="{ backgroundImage: `url('${pageData.imageUrl}')` }"></div>
        <Button buttonName="Donate author" :isActive="false" bgColor="green" />
        <h1>{{ pageData.title }}</h1>
        <p>
            {{pageData.description}}
        </p>
    </div>
</template>

<script>
    import Button from '../components/Button.vue'
    export default {
        name: 'CommentsPage',
        components: {
            Button
        },
        props: {
            pageData: {
                type: Object,
                default: function () {
                    return {
                        imageUrl: "",
                        title: "",
                        description: "Your description"
                    }
                }
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    .comments-page {
        .main-img{
            background-repeat: no-repeat;
            background-position: center center;
            background-attachment: fixed;
            background-size: cover;
            height: 300px;
            width: 100%;
            margin-bottom: 5px;
        }
        h3 {
            margin: 40px 0 0;
        }
    }

</style>
