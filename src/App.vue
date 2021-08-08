<template>
    <div id="app">
        <meta name="viewport" content="width=device-width">
        <div :class="this.toggle ? 'container active' : 'container'">
            <div class="header">
                <div class="h1">Добавление товара</div>
                <button class="addItemBtn" :class="this.toggle ? 'addItemBtn active' : 'addItemBtn'"
                        @click="changeToggle">+
                </button>
                <div :class="this.toggle ? 'select active' : 'select'"><Select @chane-select="changeSelect"/></div>
            </div>
            <div class="display">
                <div :class="this.toggle ? 'form active' : 'form'">
                    <Form
                            @add-item="addItem"
                            :toggle="toggle"
                            @newArr-item="newArrItem"
                    />
                </div>
                <div :class="this.toggle ? 'items active' : 'items'">
                    <ItemList v-bind:items="items"
                              @delete-item="deleteItem"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Form from "@/components/page1";
    import ItemList from "@/components/ItemsList";
    import Select from "@/components/Select";

    export default {
        name: 'App',
        mounted() {
            this.newArrItem()
        },
        data() {
            return {
                toggle: false,
                items: [
                    {
                        id: 1,
                        name: "А Новый товар",
                        imgSrc: 'https://avatars.mds.yandex.net/get-mpic/4412310/img_id3030926809666110906.jpeg/13hq',
                        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
                        price: 12000
                    },
                    {
                        id: 2,
                        name: "Б Новый товар",
                        imgSrc: 'https://avatars.mds.yandex.net/get-mpic/4412310/img_id3030926809666110906.jpeg/13hq',
                        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
                        price: 14000
                    },
                    {
                        id: 3,
                        name: "В Новый товар",
                        imgSrc: 'https://avatars.mds.yandex.net/get-mpic/4412310/img_id3030926809666110906.jpeg/13hq',
                        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
                        price: 14000
                    },
                    {
                        id: 4,
                        name: "С Новый товар",
                        imgSrc: 'https://avatars.mds.yandex.net/get-mpic/4412310/img_id3030926809666110906.jpeg/13hq',
                        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
                        price: 10000
                    }
                ],
                filter: 'forName'
            }
        },
        components: {
            Form,
            ItemList,
            Select
        },
        watch: {
            toggle: function () {
                if (this.toggle) {
                    document.documentElement.style.overflow = 'hidden'
                    return
                }

                document.documentElement.style.overflow = 'auto'
            }
        },
        methods: {
            changeToggle() {
                this.toggle = !this.toggle;
            },
            deleteItem(id) {
                this.items = this.items.filter(t => t.id != id)
                const parsed = JSON.stringify(this.items)
                localStorage.setItem('items', parsed)
            },
            addItem(newItem) {
                this.items.push(newItem)
                const parsed = JSON.stringify(this.items)
                localStorage.setItem('items', parsed)
            },
            changeSelect(filter) {
                this.filter = filter
                const temp = JSON.parse(JSON.stringify(this.items))
                if (filter == 'forPriceMin') {
                    this.items = temp.sort((a, b) => a.price > b.price ? 1 : -1);
                } else if (filter == 'forPriceMax') {
                    this.items = temp.sort((a, b) => a.price > b.price ? -1 : 1);
                } else if (filter == 'forName') {
                    this.items = temp.sort((a, b) => a.name.toLowerCase() > b.name.toLowerCase() ? 1 : -1);
                }
            },
            newArrItem() {
                if (localStorage.getItem('items')) {
                    try{
                        this.items = JSON.parse(localStorage.getItem('items'))
                    } catch (e) {
                       localStorage.removeItem('items')
                    }
                }

            }
        }
    }
</script>

<style lang="scss">
    #app {
        margin: 0px auto;
        padding: 0px 10px;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;

    }

    .addItemBtn {
        display: none;
    }

    .container {
        max-width: 1440px;
        margin: 0px auto;
        padding: 0px 10px;
        width: 100%;
    }

    .header {
        width: 100%;
        display: flex;
        justify-content: space-between;
        margin: 0 auto;
    }


    .select {
    }

    .h1 {
        position: relative;
        margin-left: 32px;
        margin-top: 32px;
        width: 50%;
        height: 35px;
        font-family: $font1;
        font-weight: 600;
        font-size: 28px;
        line-height: 35px;
        color: #3F3F3F;
    }

    .items {
        width: 100%;
        margin: 0 auto;
        margin-left: 332px;
    }

    .display {
        display: flex;
        margin: 16px 32px;
        margin-bottom: 0px;
    }

    .form {
        position: fixed;
        z-index: 50;
        transition: all 0.3s ease 0s;
    }

    @media (max-width: 1100px) {
        .form {
            left: 30px
        }
    }

    @media (max-width: 767px) {
        body {
            margin: 0;
        }
        .container {
            margin: 0;
            padding: 0;
        }
        .header {
            margin: 10px auto 20px auto;
        }
        .select {
            margin-top: 10px;
        }
        .h1 {
            display: none;
        }
        .addItemBtn {
            display: flex;
            height: 40px;
            width: 40px;
            background: #FFFEFB;
            box-shadow: 0px 2px 3px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
            border-radius: 50%;
            border: 0;
            align-items: center;
            justify-content: center;
            transition: all 0.7s ease 0s;
        }
        .addItemBtn.active {
            z-index: 4;
            transform: rotate(45deg);
            background-color: #FF8484;
        }

        .display {
            flex-direction: column;
            align-items: center;
            margin: 0px 0px;
        }
        .form {
            width: 100%;
            left: 5%;
            top: -520px;
            margin-right: 0;
            position: fixed;
            z-index: 3;
        }
        .form.active {
            top: 20px;
        }
        .items {
            margin-left: 0px;
        }
        .items.active {
            opacity: 0.6;
        }
        .select.active {
            opacity: 0.6;
        }
    }

</style>