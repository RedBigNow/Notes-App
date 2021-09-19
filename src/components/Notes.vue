<template>
    <div class="notes">
        <div class="note" :class="[{ full : !grid}, note.priority ]" v-for="(note, index) in notes" :key="index">
            <div class="note-header">
                <p>{{ note.title }}</p>
                <p class="close" @click="removeNote(index)">&#10006;</p>
            </div>
            <div class="note-body">
                <p>{{ note.descr }}</p>
                <span>{{ note.date }}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        notes: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    },
    methods: {
        removeNote (index) {
            this.$emit('remove', index)
        }
    }
}
</script>

<style lang="scss">
.notes {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    max-width: 760px;
    padding: 40px 0;
    margin: 0 auto;
}

.note {
    width: 48%;
    padding: 18px 20px;
    margin-bottom: 20px;
    background-color: #fff;
    transition: 0.25s;

    &:hover {
        box-shadow: 0 30px 30px rgba(0,0,0,0.04);
        transform: translate(0, -6px);
    }

    &.standart {
        border: 4px solid #fff,
    }

    &.important {
        border: 4px solid rgba(255, 255, 0, 0.3),
    }

    &.very-important {
        border: 4px solid rgba(255, 0, 0, 0.3),
    }

    &.full {
        width: 100%;
        text-align: center;

        .note-header {
            justify-content: center;

            p {
                margin-right: 16px;
            }
        }
    }
}

.note-header {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    max-width: 760px;
    margin: 0 auto;

    h1 {
        font-size: 32px;
    }

    p {
        font-size: 22px;
        color: #494ce8;
    }

    p.close {
        cursor: pointer;
        font-size: 16px;
        color: #000;
    }

    svg {
        margin-right: 12px;
        color: #999;
        cursor: pointer;

        &.active {
            color: #494ce8;
        }

        &:last-child {
            margin-right: 0px;
        }
    }
}

.note-body {
    p {
        margin: 20px 0;
    }

    span {
        font-size: 14px;
        color: #999;
    }
}

@media screen and (max-width: 768px) {
    .note-header {
        flex-flow: column;
        align-items: center;
        justify-content: center;
    }

    .icons {
        display: none;
    }

    .note {
        width: 100%;

        .note-header {
            flex-flow: wrap;
            align-items: center;
            justify-content: space-between;
        }
    }
}
</style>