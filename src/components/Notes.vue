<template>
    <div class="notes">
        <div class="note" :class="{ full : !grid }" v-for="(note, index) in notes" :key="index">
            <div class="note-header">
                <p>{{ note.title }}</p>
                <p style="cursor: pointer;" @click="removeNote(index)">x</p>
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
        padding: 40px 0;
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

        h1 {
            font-size: 32px;
        }

        p {
            font-size: 22px;
            color: #494ce8;
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
</style>