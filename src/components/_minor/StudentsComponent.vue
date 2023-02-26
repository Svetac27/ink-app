<template>
    <div class="section-wrapper">
        <div class="section-header">
            <button class="btn secondary-btn">{{msg.new}}</button>
        </div>
        <table class="section-nav" v-if="checkNumberOfElements(all_pupils)">
            <tr v-for="item in students_data" :key="item.key">
                <th type="button" @click="changeOrder(item)" class="section-nav-header">
                    <h6 :class="[`${item.active}`]">{{item.key}}</h6>
                    <div v-if="item.active && item.up"  class="dot up"></div>
                    <div v-if="item.active && !item.up" class="dot down"></div>
                </th>
                <td class="section-body">
                    <div v-for="(pupil, index) in pupils" :key="index">
                        <h6 class="item">{{getData(pupil, item.key)}}</h6>
                    </div>
                </td>
            </tr>
        </table>
        <Pagination :number="nm_pupils" :limit="per_page" @changePage="changePage" @changePerPage="changePerPage"/>
    </div>
</template>
<script>
    // icons
    // data
    import ident from '../../assets/ident/ident.json';
    import msg from '../../assets/data/language_data.json';
    import students from '../../assets/data/students.json';
    import all_pupils from '../../assets/data/pupils.json';
    // components
    import Pagination from '../_minor/PaginationComponent.vue';

    export default {
        name: 'StudentsComponent',
        components: {
            Pagination
        },
        props: {
            content: String
        },
        data() {
            return {
                nm_pupils: 0,
                per_page: ident.elements_per_page,
                msg: msg.en,
                students_data: students,
                all_pupils: all_pupils,
                pupils: [],
                active_tab: "number"
            }
        },
        methods: {
            checkNumberOfElements(pupils) {
                this.nm_pupils = pupils.length;
                var pup = [];
                for(var i=0; i < this.per_page; i++ ) pup.push(pupils[i]);
                this.pupils = pup;
                return true;
            },
            reorderItems(pupils, item) {
                var temp;
                for(var i=0; i<pupils.length; i++) {
                    for(var j=0; j<pupils.length; j++) {
                        if(!item.up) {
                            if(pupils[i][item.key] < pupils[j][item.key]) {
                                temp = pupils[i];
                                pupils[i] = pupils[j];
                                pupils[j] = temp;
                            }
                        }
                        else {
                            if(pupils[i][item.key] > pupils[j][item.key]) {
                                temp = pupils[i];
                                pupils[i] = pupils[j];
                                pupils[j] = temp;
                            }
                        }
                    }
                }
                this.pupils = pupils;
            },
            changeOrder(item) {
                if(item.active)
                    item.up = !item.up;
                else {
                    for(var i = 0; i < this.students_data.length; i++) {
                        this.students_data[i].active = false;
                        if(this.students_data[i].key === item.key) {
                            this.students_data[i].active = true;
                            this.active_tab = item.key;
                        }
                    }
                }
                this.reorderItems(this.pupils, item);
            },
            getData(pupil, key) {
                return pupil[key];
            },
            changePage(page) {
                console.log(page);
            },
            changePerPage(per_page) {
                console.log(per_page);
            }
        }
    }
</script>
<style lang="scss" scoped>
    @import '../../assets/ident/ident.scss';
    .section-wrapper {
        .btn {
            float: right;
        }
        .section-nav {
            width: 100%;
            height: 100%;
            overflow-x: scroll;
            overflow-y: hidden;
            scroll-behavior: smooth;
            tr {
                display: grid;
                grid-template-rows: 50px 1fr;
                align-items: center;
                .section-nav-header {
                    height: 100%;
                    position: relative;
                    border-top: 1px solid $border-color;
                    border-right: 1px solid $border-color;
                    border-bottom: 1px solid $border-color;
                    cursor: pointer;
                    h6 {
                        text-transform: uppercase;
                        margin: auto;
                        height: 100%;
                    }
                    .dot {
                        margin: 5px 0;
                    }
                }
                td {
                    height: 100%;
                    border-right: 1px solid $border-color;
                    .item {
                        height: 30px;
                    }
                }
            }
        }
    }
</style>