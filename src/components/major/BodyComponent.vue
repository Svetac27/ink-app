<template>
    <div class="body-wrapper">
        <Debts v-if="content === 'debts'"/>
        <Demands v-if="content === 'demands'"/>
        <Groups v-if="content === 'groups'"/>
        <Invoices v-if="content === 'invoices'"/>
        <Payments v-if="content === 'payments'"/>
        <Students v-if="content === 'students'"/>
        <Withdraws v-if="content === 'withdraws'"/>
    </div>
</template>
<script>
    // components
    import Debts from '../_minor/DebtsComponent.vue';
    import Demands from '../_minor/DemandsComponent.vue';
    import Groups from '../_minor/GroupsComponent.vue';
    import Invoices from '../_minor/InvoicesComponent.vue';
    import Payments from '../_minor/PaymentsComponent.vue';
    import Students from '../_minor/StudentsComponent.vue';
    import Withdraws from '../_minor/WithdrawsComponent.vue';

    export default {
        name: 'BodyComponent',
        components: {
            Debts,
            Demands,
            Groups,
            Invoices,
            Payments,
            Students,
            Withdraws
        },
        props: {
            content: String
        },
        data() {
            return {
            }
        }
    }
    </script>
    <style lang="scss" scoped>
        @import '../../assets/ident/ident.scss';
    </style>