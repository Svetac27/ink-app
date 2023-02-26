<template>
    <section class="pagination-wrapper">
        <div class="left">
            <button @click="changePage('<')" :class="[`arrow-btn left ${page == 1 ? 'disabled' : 'clickable' }`]"><LeftArrow type="button" class="icon"/></button>
            <button v-for="n in last_page" :key="n" @click="changePage(n)" class="blank-btn">
                <h3 :class="[`btn-text ${checkPage(n)}`]">{{n}}</h3>
            </button>
            <button @click="changePage('>')" :class="[`arrow-btn right ${page == last_page ? 'disabled' : 'clickable'}`]"><RightArrow class="icon"/></button>
        </div>
        <div class="right">
            <DropDown :perPage="limit" @changePerPage="changePerPage"/>
        </div>
    </section>
</template>

<script>
//icons
import LeftArrow from '../../assets/icons/left-arrow.vue';
import RightArrow from '../../assets/icons/right-arrow.vue';
import DropDown from '../../components/_minor/DropDown.vue';

 export default {
    name: 'PaginationComponent',
    components: {
        LeftArrow,
        RightArrow,
        DropDown
    },
    props: {
        number: Number,
        limit: Number,
    },
    data() {
        return {
            page: 1,
            last_page: Number,
            new_page: Number,
            disabled: false,
            number_of_pages: Number
        }
    },
    beforeMount() {
        this.last_page = Math.ceil(this.number / this.limit);
    },
    methods: {
        checkPage(page) {
            this.disabled = page === this.page ? 'disabled' : 'clickable';
            return this.disabled;
        },
        changePage(page) {
            var old = this.new_page;
            switch(page) {
                case '<':
                    if(this.page != 1) {
                        this.page -= 1;
                        this.new_page = this.page;
                        break;
                    }
                    else break;
                case '>':
                    if(this.page != this.last_page) {
                        this.page += 1;
                        this.new_page = this.page;
                        break;
                    }
                    else break;
                default:
                    this.page = page;
                    this.new_page = this.page;
                    break;
            }
            if(old != this.new_page)
                this.$emit('changePage', this.new_page);
        }
    }
 }
</script>

<style lang="scss" scoped>
    @import '../../assets/ident/ident.scss'; 
    .pagination-wrapper {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
        .left {
            display: flex;
            align-items: center;
            .disabled {
                cursor: text;
            }
            .blank-btn {
                .btn-text {
                    padding: 5px;
                    height: 18px;
                    width: 18px;
                    border-radius: 50%;
                }
                .disabled {
                    background-color: $secondary-color;
                    border: 1px solid $secondary-color;
                    opacity: 0.9;
                    color: white;
                    font-size: 16px;
                }
                .clickable {
                    border: 1px solid $btn-hover;
                }
            }
        }
    }
</style>