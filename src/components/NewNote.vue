<template>
    <div class="new-note">

        <div class="priority">
                <label>Priority</label>
                <br>
                <!-- <label for="vh">Very high</label>
                <input id = "vh" class="Priority" type="checkbox">
                <label for = "h">High</label>
                <input id = "h" class="Priority" type="checkbox">
                <label for = "vh">Default</label>
                <input id = "def" class="Priority" type="checkbox">  -->

                <button class="btn btnVeryHighPriority" type="checkbox" @focus="func">Very high</button>
                <button class="btn btnHighPriority" type="checkbox">High</button>
                <button class="btn btnDefaultPriority" type="checkbox">Default</button>

                <br>
            </div>

            <label>Title</label>
            <input type="text" v-model="note.title">
            <label>Discription</label>
            <textarea v-model="note.discr"></textarea>

            <button class="btn btnPrimary" @click="addNote">New note</button>
        </div>

</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        }
    },
    methods: {
        addNote () {
            this.$emit('addNote', this.note)
        }
    }
}
</script>

<style lang="scss">
    .new-note {
        text-align: center;
    }
    .priority {
        display: inline;
    }
</style>