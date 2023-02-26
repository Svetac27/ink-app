<template>
    <div class="menu-wrapper">
        <button class="menu-view">
            <LeftArrow @click="changeMenuView" class="icon" v-if="view==='full'"/>
            <RightArrow @click="changeMenuView" class="icon" v-if="view==='short'"/>
        </button>
        <ul class="menu">
            <li :class="[`menu-item ${item.active_tab ? 'active' : 'inactive'}`]" v-for="item in getMenuItem()" :key="item.order">
                <button @click="activateTab(item.key)" class="[`item blank-btn ${view}`]">
                    <h4 :class="[`item-title ${view}`]">{{ getTranslation(item.key) }}</h4>
                    <StudentIcon v-if="item.key==='students'" class="icon"/>
                    <SchoolIcon v-if="item.key==='groups'" class="icon"/>
                    <PaymentsIcon v-if="item.key==='payments'" class="icon"/>
                    <DemandsIcon v-if="item.key==='demands'" class="icon"/>
                    <DebtsIcon v-if="item.key==='debts'" class="icon"/>
                    <InvoicesIcon v-if="item.key==='invoices'" class="icon"/>
                    <WithdrawsIcon v-if="item.key==='withdraws'" class="icon"/>
                </button>
            </li>
        </ul>
    </div>
</template>
<script>
    // icons
    import LeftArrow from '../../assets/icons/left-arrow.vue';
    import RightArrow from '../../assets/icons/right-arrow.vue';
    import StudentIcon from '../../assets/icons/student-icon.vue';
    import SchoolIcon from '../../assets/icons/school-icon.vue';
    import PaymentsIcon from '../../assets/icons/payments-icon.vue';
    import DemandsIcon from '../../assets/icons/demands-icon.vue';
    import DebtsIcon from '../../assets/icons/debts-icon.vue';
    import InvoicesIcon from '../../assets/icons/invoices-icon.vue';
    import WithdrawsIcon from '../../assets/icons/withdraws-icon.vue';
    // data
    import lang from '../../assets/data/language_data.json';
    import menu from '../../assets/data/menu.json';

    export default {
        name: 'MenuComponent',
        components: {
            LeftArrow,
            RightArrow,
            StudentIcon,
            SchoolIcon,
            PaymentsIcon,
            DemandsIcon,
            DebtsIcon,
            InvoicesIcon,
            WithdrawsIcon
        },
        props: {
            content: String
        },
        data() {
            return {
                lang: lang.en,
                menu: menu.main,
                school: SchoolIcon,
                view: 'full', // full / short
                active_tab: String
            }
        },
        methods: {
            // remove inactive menu items
            removeElement(menu) {
                for (var i = 0; i < menu.length; i++) {
                    if (menu[i].active === false) {
                        this.recipes = menu[i].sub;
                        menu.splice(i, 1);
                    }
                    if(menu[i].active_tab === true) {
                        this.active_tab = menu[i].key;
                    }
                }
                return menu;
            },
            // sort by order all menu items
            sortedArray(menu){
                this.removeElement(menu);
                return menu.sort((a, b) => a.order - b.order );
            },
            // get menu items from JSON
            getMenuItem() {
                var menu = this.menu;
                this.sortedArray(menu);
                return menu;
            },
            // get translation for menu item
            getTranslation(key) {
                return this.lang[key];
            },
            changeMenuView() {
                if (this.view === 'full') {
                    this.view = 'short';
                } else {
                    this.view = 'full';
                }
            },
            activateTab(key) {
                for (var i = 0; i < this.menu.length; i++) {
                    if(this.active_tab === key) {
                        return;
                    }
                    if (this.menu[i].key === key) {
                        this.menu[i].active_tab = true;
                    } else {
                        this.menu[i].active_tab = false;
                    }
                }
                this.active_tab = key;
                this.$emit('changeTab', this.active_tab);
            }
        }
    }
</script>
<style lang="scss" scoped>
    @import '../../assets/ident/ident.scss';

    .menu-wrapper {
        margin-right: 10px;
        .menu-view {
            height: 50px;
            width: 100%;
            border: 0;
            display: flex;
            align-items: center;
            justify-content: flex-end;
            .icon {
                padding: 12px 20px;
                cursor: pointer;
                width: 15px;
                height: 15px;
                fill: $border-color;
            }
        }
        .menu {
            margin: 0;
            padding: 0;
            // width: 90%;
            .menu-item {
                list-style: none;
                border-bottom: 1px solid $border-color;
                border-top: 1px solid transparent;
                border-left: 1px solid $border-color;
                border-right: 5px solid transparent;
                height: 50px;
                &.active {
                    border-color: $tab-color;
                    border-left: 5px solid $tab-color;
                    border-right: 1px solid transparent;
                    transition: border-left 0.2s linear;
                }
                button.\[\`item.blank-btn.\$\{view\}\`\] {
                    font-size: 16px;
                    height: 100%;
                    border: 0;
                    padding: 0 20px;
                    margin: auto;
                    display: flex;
                    align-items: center;
                    justify-content: space-between;
                    transition: width 0.3s linear;
                    .full {
                        display: block;
                        width: 100px;
                        min-width: 100px;
                    }
                    .short {
                        display: none;
                        width: 30px;
                    }
                    .item-title {
                        margin: 0;
                    }
                }
            }
        }
    }
</style>