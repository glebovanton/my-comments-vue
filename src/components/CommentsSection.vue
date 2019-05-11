<template>
    <div class="comments-section">
        <transition name="appear">
            <ConfirmationModal v-if='confirmModal' @confirm='removeComment(selectedCommentIndex)'
                               @cancel="cancelRemove"/>
        </transition>
        <form name="comment-form" method="post" action="" v-on:submit.prevent="addComment">
            <input name="add-comment" type="text" v-model.trim="addCommentInput" v-bind:class="{error: hasError}"/>
            <button type="submit" :class="{'hidden':!addCommentInput.length}">Send</button>
        </form>

        <div class="comments-lists" v-if="lists.length">
            <h2>Comments:</h2>
            <ul>
                <li v-for="(list,index) in lists" :key="index">
                    <ProfileLink
                            :nickName="list.user"
                            :avatarUrl="list.avatarUrl"
                    />
                    <span class="comment" contenteditable="false" @keydown.enter="updateComment($event, list)"
                          @blur="updateComment($event, list)" @click="list.isSelect=!list.isSelect"
                          ref="comment">{{list.comment}}</span>
                    <div class="buttons-wrap" v-if="list.isSelect">
                        <Button buttonName="Edit" @click.native="editComment(index)"/>
                        <Button buttonName="delete" bgColor="red" @click.native="confirmRemove(index)"/>
                    </div>

                </li>
            </ul>
        </div>

    </div>
</template>

<script>
    import Button from './Button'
    import ConfirmationModal from './ConfirmationModal.vue'
    import ProfileLink from './ProfileLink.vue'

    export default {
        name: "CommentsSection",
        components: {
            Button,
            ConfirmationModal,
            ProfileLink
        },
        props: {
            currentUser: {
                type: Object,
                default: function () {
                    return {
                        nickName: 'User',
                        avatarUrl: 'img/default_avatar.png'
                    }
                }
            }
        },
        data() {
            return {
                addCommentInput: '',
                lists: [
                    {
                        id: 1,
                        user: 'Alex',
                        avatarUrl: 'img/default_avatar.png',
                        comment: 'Great',
                        isSelect: false
                    }, {
                        id: 2,
                        comment: 'foo..',
                        user: 'Nick',
                        avatarUrl: 'img/default_avatar.png',
                        isSelect: false
                    }, {
                        id: 3,
                        comment: "coooool",
                        user: 'Andrey',
                        avatarUrl: 'img/default_avatar.png',
                        isSelect: false
                    },
                    {
                        id: 4,
                        comment: "coool",
                        user: 'John',
                        avatarUrl: 'img/cat_avatar.png',
                        isSelect: false
                    }
                ],
                hasError: false,
                confirmModal: false,
                selectedCommentIndex: null
            }
        },
        methods: {
            addComment() {
                if (!this.addCommentInput) {
                    this.hasError = true;
                    return;
                }
                this.hasError = false;
                this.lists.push({
                    id: this.lists.length + 1,
                    user: this.currentUser.nickName,
                    avatarUrl: this.currentUser.avatarUrl,
                    comment: this.addCommentInput,
                    isSelect: false
                })
                this.addCommentInput = ''
            },
            editComment(index) {

                const selectedComment = this.$refs.comment[index]
                selectedComment.setAttribute("contenteditable", true);
                selectedComment.focus()
            },
            updateComment(e, list) {
                e.preventDefault()
                list.comment = e.target.innerText
                e.target.setAttribute("contenteditable", false);
                e.target.blur()
            },
            confirmRemove(index) {
                this.selectedCommentIndex = index;
                this.confirmModal = true;
            },
            cancelRemove() {
                this.confirmModal = false;
                this.selectedCommentIndex = null;
            },
            removeComment(index) {
                this.lists.splice(index, 1);
                // e.target.blur()
                this.selectedCommentIndex = null;
                this.confirmModal = false;
            }
        }
    }
</script>

<style scoped lang="scss">
    .comments-section {
        .appear-enter {
            opacity: 0;
        }

        .appear-enter .modal-window {
            transform: translate(-75%, -50%);
        }

        .appear-enter-active {
            transition: .5s;
        }

        .appear-leave-active .modal-window {
            transform: translate(0, -50%);
        }

        .appear-leave-active {
            opacity: 0;
            transition: .5s;
        }

        form {
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;

            input {
                height: 25px;
                width: 300px;
            }

            button {
                background-color: white;
                color: black;
                border: 2px solid #e7e7e7;
                padding: 6px 25px;
                text-align: center;
                text-decoration: none;
                display: inline-block;
                font-size: 16px;
                margin: 0 2px;
                cursor: pointer;
                transition-duration: 0.4s;
                transition: all 0.3s linear;
                visibility: visible;
                opacity: 1;

                &.hidden {
                    visibility: hidden;
                    opacity: 0;
                }

                &:hover {
                    transition: all 0.2s linear;
                    box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.19);
                }
            }
        }

        .comments-lists {

            ul {
                list-style-type: none;

                li {
                    display: flex;
                    align-items: center;
                    height: 35px;
                    margin-bottom: 30px;

                    span.comment {
                        cursor: pointer;
                    }

                    .buttons-wrap {
                        position: relative;
                    }
                }
            }
        }
    }
</style>