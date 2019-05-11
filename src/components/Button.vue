<template>
    <div class="button" :style="{'color': bgColor}" :class="{disabled:!isActive}">{{buttonName}}</div>
</template>

<script>
    export default {
        name: "Button",
        props: {
            buttonName: {
                type: String,
                default: ''
            },
            bgColor: {
                type: String,
                default: 'grey'
            },
            isActive: {
                type: Boolean,
                default: true
            }
        }
    }
</script>

<style scoped lang="scss">
    .button {
        cursor: pointer;
        user-select: none;
        color: black;
        background-color: transparent;
        border: 1px solid grey;
        display: inline-block;
        text-decoration: none;
        padding: 5px 10px;
        white-space: nowrap;
        text-transform: capitalize;
        margin: 0 5px;
        transition: all 0.5s;

        &.disabled {
            cursor: none;
        }

        &:hover {
            background: #00000008;
            box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.19);
        }
    }
</style>