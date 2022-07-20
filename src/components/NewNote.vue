<template>
    <div class="new-note">
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
</style>