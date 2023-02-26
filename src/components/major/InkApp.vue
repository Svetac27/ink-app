<template>
    <div class="app-wrapper">
        <header>
            <img class="logo" :src="getImgUrl(logo)" alt="Ink Logo">
            <div class="settings">
                <button @click="openSettings()" class="sett blank-btn">
                    <GearIcon/>
                </button>
            </div>
        </header>
        <div class="body">
            <MainComponent/>
        </div>
        <FormComponent v-if="open_form" :content="form_content" @closeForm="closeForm"></FormComponent>
    </div>
</template>
<script>
// icons
import GearIcon from '../../assets/icons/gearIcon.vue';
// components
import FormComponent from '../_basic/FormComponent.vue';
import MainComponent from '../major/MainComponent.vue';
// data
import identification from '../../assets/ident/ident.json';
import msg from '../../assets/data/language_data.json';

export default {
  name: 'InkApp',
  components: {
    GearIcon,
    FormComponent,
    MainComponent
  },
  props: {
    content: String
  },
  data() {
    return {
      ident: identification,
      msg: msg.en,
      logo: identification.logo,
      open_form: false,
      form_content: {
        type: Object,
      }
    }
  },
    methods: {
        getImgUrl(logo) {
            return require("../../assets/ident/" + logo);
        },
        openSettings() {
            this.open_form = true;
            this.form_content = {
                form_name: "Settings"
            }
        },
        closeForm(data) {
            this.open_form = data;
        }
    }
}
</script>
<style lang="scss" scoped>
    @import '../../assets/ident/ident.scss';
    .app-wrapper {
        width: 100%;
        height: 100%;
        padding: 0 10px;
        header {
            height: 50px;
            padding: 0;
            .logo {
                height: 100%;
                float: left;
            }
            .settings {
                height: 100%;
                float: right;
                display: flex;
                align-items: center;
                svg {
                    height: 30px;
                    fill: $primary-color;
                }
            }
        }
        .body {
            height: calc(100% - 50px);
        }
    }
</style>