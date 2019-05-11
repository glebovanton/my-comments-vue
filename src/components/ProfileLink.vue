<template>
    <a id="profile_link" class="profile_link" href="#">
        <img class="profile_img" :src="avatarUrl"
             alt="avatar">
        <span class="profile_name">{{nickName}}</span>
    </a>
</template>

<script>
    export default {
        name: "ProfileLink",
        props: {
            nickName: {
                type: String,
                default: 'User'
            },
            avatarUrl: {
                type: String,
                default: 'img/default_avatar.png'
            }
        }
    }
</script>

<style scoped lang="scss">
    .profile_link {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        text-decoration: none;
        width: 100px;

        .profile_img {
            height: 25px;
            border-radius: 50%;
            object-fit: cover;
            width: 25px;
            background-color: white;
            margin-right: 3px;
        }

        .profile_name {
            padding-right: 10px;
            color: #232324;
            overflow: hidden;
        }


    }
</style>