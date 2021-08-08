<template>
    <div>
    <form @submit.prevent="onSubmit" @click="$emit('newArr-item')">
        <div>
            <label for="name">Название товара <span>*</span></label>
            <br/>
            <input id='name' @blur="blurName" type="name" v-model="newItemData.name"
                   :class="$v.newItemData.name.$error ? 'required' : '' "/>
            <span v-if="$v.newItemData.name.$dirty && $v.newItemData.name.$error" class="req">Это поле является обязательным</span>
        </div>
        <div>
            <label for="description">Описание товара</label>
            <br/>
            <textarea id='description' type="description" v-model="newItemData.description"/>
        </div>
        <div>
            <label for="imgUrl">Ссылка на изображение товара <span>*</span></label>
            <br/>
            <input id='imgUrl' @blur="blurImg" type="text" v-model="newItemData.imgUrl"
                   :class="$v.newItemData.imgUrl.$error ? 'required' : '' "/>
            <span v-if="$v.newItemData.imgUrl.$dirty && $v.newItemData.imgUrl.$error" class="req">Это поле является обязательным, введите URL-адрес</span>
        </div>
        <div>
            <label for="price">Цена товара <span>*</span></label>
            <br/>
            <input id='price' @blur="blurPrice" type="text" v-model="newItemData.price"
                   :class="$v.newItemData.price.$error ? 'required' : '' "/>
            <span v-if="$v.newItemData.price.$dirty && $v.newItemData.price.$error" class="req">Это поле является обязательным</span>
        </div>
        <button type="submit" :class="!isFormValid || !isFormUntouched ? 'DisabledBtn btn' : 'SubmitBtn btn'" :disabled="!isFormValid || !isFormUntouched">Добавить товар</button>
    </form>
    </div>
</template>

<script>
    import {validationMixin} from 'vuelidate'
    import {required, url} from 'vuelidate/lib/validators'
    export default {
        mixins: [validationMixin],
        name: "Form",
        props: ['toggle'],
        mounted() {
            this.$v.$reset()
        },
        computed: {
            isFormValid () {
                return !this.$v.newItemData.$error
            },
            isFormUntouched () {
                return this.newItemData.name && this.newItemData.imgUrl && this.newItemData.price
            }
        },
        methods: {
            onSubmit() {
                this.$v.newItemData.$touch()
                if (!this.$v.newItemData.$error) {
                    const newItem = {
                        id: Date.now(),
                        name: this.newItemData.name,
                        imgSrc: this.newItemData.imgUrl,
                        description: this.newItemData.description,
                        price: this.newItemData.price
                    }
                    this.$emit('add-item', newItem)
                    this.newItemData.name = ''
                    this.newItemData.description = ''
                    this.newItemData.imgUrl = ''
                    this.newItemData.price = ''
                    this.$v.$reset()
                }
            },
            blurName() {
                this.$v.newItemData.name.$touch()
            },
            blurImg() {
                this.$v.newItemData.imgUrl.$touch()
            },
            blurPrice() {
                this.$v.newItemData.price.$touch()
            }
        },
        data() {
            return {
                num:'',
                newItemData: {
                    name: '',
                    description: '',
                    imgUrl: '',
                    price: ''
                }

            }

        },
        validations: {
            newItemData: {
                name: {required},
                imgUrl: {required, url},
                price: {required}
            }
        }

    }
</script>

<style lang="scss" scoped>
    input.required {
        border: 1px solid #FF8484;
        margin: 5px 24px 0px 24px;
    }

    span {
        font-size: 8px;
        color: red;
    }

    .req {
        font-family: Source Sans Pro;
        font-style: normal;
        font-weight: normal;
        font-size: 8px;
        line-height: 10px;
        margin: 0px 24px 2px 24px;
    }

    textarea {
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        height: 108px;
        width: 284px;
        margin: 0 24px;
        border: none;
    }

    .DisabledBtn {
        background: #EEEEEE;
        color: #B4B4B4;
    }
    .SubmitBtn {
        background: #7BAE73;
        color: #FFFFFF;
    }
    .SubmitBtn:hover {
        cursor: pointer;
        background: #EEEEEE;
    }

    @media(max-width: 1209px) {
        label {
            font-size: 15px;
            line-height: 15px;
        }
    }
    @media(max-width: 1209px) {
        label {
            font-size: 13px;
            line-height: 13px;
        }
    }

    @media(max-width: 321px) {
        form {
            width: 292px;
            height: 410px;
        }
        label {
            font-size: 13px;
            line-height: 13px;
        }
        input {
            height: 36px;
            width: 244px;
        }
        textarea {
            width: 244px;
        }
        .btn{
            padding: 12px 80px 12px 80px;
        }
    }
</style>