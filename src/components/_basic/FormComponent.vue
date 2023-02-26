<template>
    <div class="form-wrapper">
        <div @click="closeForm" class="background"></div>
        <div class="form-content">
            <h1 class="form-name">{{content.form_name}}</h1>
            <div class="company input-form">
                <label for="input comp">{{msg.company_name}}</label>
                <input id="input comp" type="text" v-model="company_name">
            </div>
            <div class="logo input-form">
                <label>{{msg.logo}}</label>
                <div class="input_box">
                    <div>{{company_logo}}</div>
                    <input @change="uploadFile" class="attach_input" type="file" ref="file">
                    <AttIcon class="svg"/>
                </div>
            </div>
            <div class="language input-form">
                <label for="input lang">{{msg.language}}</label>
                <select id="input lang" v-model="lang">
                    <option v-for="lan in ident.language" :key="lan.key" :value="lan.key">{{lan.value}}</option>
                </select>
            </div>
            <div class="button-wrapper">
                <button @click="closeForm()" class="btn primary_btn">{{msg.cancel}}</button>
                <button @click="saveChanges()" class="btn primary_btn">{{msg.save}}</button>
            </div>
        </div>
    </div>
</template>
<script>
    import AttIcon from '../../assets/icons/attachmentIcon.vue';

    import identification from '../../assets/ident/ident.json';
    import msg from '../../assets/data/language_data.json';
    
    export default {
        name: 'FormComponent',
        components: {
            AttIcon
        },
        props: {
            content: Object
        },
        data() {
            return {
                ident: identification,
                msg: msg.en,
                company_name: identification.company_name,
                company_logo: identification.logo,
                lang: identification.lang,
                images: null
            }
        },
        methods : {
            closeForm() {
                this.$emit('closeForm', false);
            },
            uploadFile() {
                this.images = this.$refs.file.files[0];
                this.ident.logo = this.images.name;
                console.log('unfinished');
                console.log(this.ident);
                console.log(this.images);
            },
            saveChanges() {
                console.log(this.ident);
                console.log(this.company_name);
                console.log(this.images);
                console.log(this.lang);
                this.closeForm();
            }
        }
    }
</script>
<style lang="scss" scoped>
@import '../../assets/ident/ident.scss';
.form-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    .background {
        position: absolute;
        top: 0;
        left: 0;
        background-color: black;
        opacity: 0.8;
        width: 100%;
        height: 100%;
        z-index: 99;
    }
    .form-content {
        position: relative;
        background: white;
        color: $text-color;
        z-index: 100;
        border-radius: 7px;
        padding: 40px 30px;
        .form-name {
            margin-bottom: 40px;
            margin-top: 0;
        }
        .input-form {
            display: grid;
            align-items: center;
            justify-content: flex-start;
            margin-bottom: 15px;
            label {
                display: flex;
                margin-bottom: 5px;
                opacity: 0.5;
            }
            .input_box,
            input#input\ comp,
            select#input\ lang {
                height: 30px;
                width: 250px;
                border-radius: 5px;
                border: 1px solid $primary-color;
                padding: 5px 10px;
                font-size: 16px;
                color: $primary-color;
                .svg {
                    fill: $primary-color;
                }
            }
            select#input\ lang {
                height: 40px;
                width: 275px;
                option {
                    padding: 3px 0;
                }
            }
            .input_box {
                display: flex;
                align-items: center;
                justify-content: space-between;
                position: relative;
                .attach_input {
                    position: absolute;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    opacity: 0;
                }
            }
        }
        .button-wrapper {
            display: flex;
            align-items: center;
            justify-content: flex-end;
            margin-top: 40px;
            .btn {
                padding: 20px 30px;
                background: $primary-color;
                color: white;
            }
            .btn:hover {
                filter: brightness(170%);
            }
        }
    }
}
</style>