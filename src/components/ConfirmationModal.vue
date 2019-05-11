<template>
    <div class="modal">
        <div class="modal-window">
            <p>Do you really want to remove this comment?</p>
            <div class="actions">
                <button class="cancel" @click="onCancel">No</button>
                <button class="confirm" @click="onConfirm">Yes</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ConfirmationModal",
        methods: {
            onConfirm() {
                this.$emit("confirm");
            },
            onCancel() {
                this.$emit("cancel");
            }
        }
    }
</script>

<style scoped lang="scss">
    .modal {
        position: fixed;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        background: rgba(0, 0, 0, .5);

        .modal-window {
            position: absolute;
            top: 50%;
            left: 50%;
            transition: .5s;
            min-width: 400px;
            max-width: 90vw;
            background: white;
            box-shadow: 0 0 10px rgba(0, 0, 0, .5);
            transform: translate(-50%, -50%);
            padding: 1em;
            color: black;
            text-align: center;

            .actions {
                display: flex;
                justify-content: flex-end;

                button {
                    user-select: none;
                    color: black;
                    background-color: transparent;
                    border: 1px solid grey;
                    display: inline-block;
                    text-decoration: none;
                    font-weight: bold;
                    padding: 5px 10px;
                    white-space: nowrap;
                    text-transform: capitalize;

                    &:last-of-type {
                        margin-left: 10px;
                    }
                }

                .cancel {
                    color: red;
                }

                .confirm {
                    color: black;
                }
            }
        }
    }
</style>