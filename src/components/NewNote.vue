<template>
    <div class="new-note">
        <div class="new-note__item">
            <label>Title</label>
            <input v-model="note.title" type="text">
        </div>
        <div class="new-note__item">
            <label>Priority</label>
            <select v-model="prioritySelected">
                <option v-for="(priority, id) in priorityList" :key="id" :value="priority.value">{{ priority.title }}</option>
            </select>
        </div>
        <div class="new-note__item new-note__item--full">
            <label>Description</label>
            <textarea v-model="note.descr"></textarea>
        </div>
        <button class="btn btnPrimary" @click="addNote">New note</button>
    </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        },
        priorityList: {
            type: Array,
            required: true
        },
        prioritySelected: {
            type: String,
            required: true
        }
    },
    methods: {
        addNote () {
            this.note.priority = this.prioritySelected //Записываем значение селекта с выбором приоритета в объект "note"
            this.$emit('addNote', this.note)
        }
    }
}
</script>

<style lang="scss">
    .new-note {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        align-items: center;
        text-align: center;
        margin-bottom: 80px;

        button {
            margin: 0 auto;
        }
    }

    .new-note__item {
        width: 48%;
        margin-bottom: 20px;

        select {
            width: 100%;
            border-radius: 20px;
            padding: 16px 26px;
            margin-bottom: 30px;
            cursor: pointer;
        }
    }

    .new-note__item--full {
        width: 100%;
    }
</style>