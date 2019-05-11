<template>
    <div id="app">
        <div class="header-profile">
            <ProfileLink :nickName="currentUser.nickName"
                         :avatarUrl="currentUser.avatarUrl"/>
        </div>
        <CommentsPage :pageData="pageData"/>

        <CommentsSection :currentUser="currentUser"/>
    </div>
</template>

<script>
    import CommentsPage from './components/CommentsPage.vue'
    import CommentsSection from './components/CommentsSection.vue'
    import ProfileLink from './components/ProfileLink.vue'

    export default {
        name: 'app',
        components: {
            CommentsPage,
            CommentsSection,
            ProfileLink
        },
        data() {
            return {
                currentUser: {
                    nickName: "John",
                    avatarUrl: "img/cat_avatar.png"
                },
                pageData: {
                    title: "Beautiful place, isn't it?",
                    imageUrl: "img/сhina.jpg",
                    description: ""
                }
            }
        }
    }
</script>

<style lang="scss">
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
        width: 100vw;

        .header-profile {
            margin-bottom: 10px;
            margin-left: 40px;
        }

    }
</style>
