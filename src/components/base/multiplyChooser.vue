<template>
    <div class="chooser-component">
        <ul class="chooser-list">
            <li v-for="(item, index) in selections" :title="item.label" :class="{active: checkActive(index)}" @click="toggleSelection(index)">{{ item.label }}</li>
        </ul>
    </div>
</template>

<script>
import _ from 'lodash'
export default {
    props: {
        selections: {
            type: Array,
            default: [{
                label: 'test',
                value: 0
            }]
        }
    },
    data() {
        return {
            nowIndexes: [0]
        }
    },
    methods: {
        toggleSelection(index) {
            if (this.nowIndexes.indexOf(index) === -1) {
                this.nowIndexes.push(index)
            }
            else {
                this.nowIndexes = _.remove(this.nowIndexes, (ind) => {
                    return ind !== index
                })
            }
            let nowObjArray = this.nowIndexes.map((ind) => {
                return this.selections[ind]
            })
            this.$emit('on-change', nowObjArray)
        },
        checkActive(index) {
            if (this.nowIndexes.indexOf(index) === -1) {
                return false
            }
            else {
                return true
            }
        }
    }
}
</script>

<style scoped>
.chooser-component {
    position: relative;
    display: inline-block;
}

.chooser-list li {
    display: inline-block;
    border: 1px solid #e3e3e3;
    height: 25px;
    line-height: 25px;
    padding: 0 8px;
    margin-right: 5px;
    border-radius: 3px;
    text-align: center;
    cursor: pointer;
}

.chooser-list li.active {
    border-color: #4fc08d;
    background: #4fc08d;
    color: #fff;
}
</style>
