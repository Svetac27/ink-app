<template>
    <div type="button" @click="openDropDown" class="chosen-number">
        {{perPage}}
        <ArrowUp v-if="opened" class="icon"/>
        <ArrowDown v-else class="icon"/>
        <ul v-if="!opened" class="dropdown-toggle">
            <li v-for="n in chose" :key="n" @click="changePerPage(n)">{{n}}</li>
            <div :class="[`dot ${mark ? mark : perPage}`]"></div>
        </ul>
    </div>
</template>
<script>
//icons
import ArrowUp from '../../assets/icons/arrow-up.vue';
import ArrowDown from '../../assets/icons/arrow-down.vue';

export default {
    name: 'DropDown',
    components: {
        ArrowUp,
        ArrowDown
    },
    props: {
        perPage: Number,
        selected: Number
    },
    data() {
        return {
            opened: false,
            mark: this.perPage,
            chose: Array
        }
    },
    beforeMount() {
        this.chose= [
            this.perPage,
            this.perPage *2,
            this.perPage *4,
        ]
    },
    methods: {
        openDropDown() {
            this.opened = !this.opened;
            console.log('open');
        },
        changePerPage(nm) {
            this.mark = nm;
            this.$emit('changePerPage', this.selected);
        }
    }
}
</script>
<style lang="scss" scoped>
    @import '../../assets/css/style.scss';
    .chosen-number {
        position: relative;
        padding: 5px 10px;
        border: 1px solid $border-color;
        border-radius: 5px;
        color: $text-color;
        font-size: 16px;
        cursor: pointer;
        .icon {
            width: 12px;
            height: 12px;
            margin-left: 5px;
        }
        .dropdown-toggle {
            border: 1px solid $border-color;
            position: absolute;
            top: 12px;
            left: 0;
            width: 100%;
            padding: 0;
            li {
                padding: 3px 0;
                margin-right: 20px;
            }
        }
    }
</style>