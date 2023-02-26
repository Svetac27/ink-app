<template>
    <div class="main-wrapper">
        <MenuComponent @changeTab="changeTab" class="menu-comp"/>
        <BodyComponent :content="active_tab" class="body-comp"/>
    </div>
</template>
<script>
    import MenuComponent from '../major/MenuComponent.vue';
    import BodyComponent from '../major/BodyComponent.vue';
    export default {
        name: 'MainComponent',
        components: {
            MenuComponent,
            BodyComponent
        },
        props: {
            content: String
        },
        data() {
            return {
                active_tab: 'students'
            }
        },
        methods: {
            changeTab(tab) {
                this.active_tab = tab;
            }
        }
    }
</script>
<style lang="scss" scoped>
    @import '../../assets/ident/ident.scss';
    .main-wrapper {
        height: 100%;
        background-color: rgba(255, 255, 255, 0.9);
        display: flex;
        margin-top: 10px;
        .menu-comp {
            width: 12%;
        }
        .body-comp {
            height: 100%;
            width: 88%;
        }
    }
</style>