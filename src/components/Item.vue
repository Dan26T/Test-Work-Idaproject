<template>
    <li class="itemCard">
        <div class="itemContainer">
            <div class="itemImg">
                <img :src="item.imgSrc" >
            </div>
            <div class="itemInfo">
                <div class="itemName">{{item.name}}</div>
                <div class="itemDescription">{{item.description}}</div>
                <div class="itemPrice">{{item.price}} руб.</div>
            </div>
            <button v-on:click="$emit('delete-item', item.id)" class="icon-bin">&times;</button>
        </div>
    </li>
</template>

<script>
    export default {
        props: {
            item:{
                type: Object
            }
        },
        name: "Item"
    }
</script>

<style lang="scss" scoped>
    .itemCard{
        justify-self: center;
        text-decoration: none;
        width: 332px;
        height: 423px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
    }
.itemImg img{
    width: 332px;
    height: 200px;
    border-radius: 4px;
}
    .itemContainer {
        display: flex;
        flex-direction: column;
        width: 100%;
        transition: all 0.5s ease 0s;
    }
    .itemInfo {
        width: 100%;

    }
    .itemName{
        font-family: $font1;
        font-style: normal;
        font-weight: 600;
        font-size: 20px;
        line-height: 25px;
        color: #3F3F3F;
        padding: 16px 0px 0px 16px;
    }
    .itemDescription {
        padding: 16px 16px 16px 16px;
        font-family: Source Sans Pro;
        font-style: normal;
        font-weight: normal;
        font-size: 16px;
        line-height: 20px;
        color: #3F3F3F;
    }
    .itemPrice {
        padding-left: 16px;
        padding-top: 16px;
        font-family: Source Sans Pro;
        font-style: normal;
        font-weight: 600;
        font-size: 24px;
        line-height: 30px;
        color: #3F3F3F;
    }
    button{
        display: none;;
    }
    .itemCard:hover{
        button{
            display:block;
            position: relative;
            left: 316px;
            top: -420px;
            width: 32px;
            height: 32px;
            background: #FF8484;
            box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            border:0;
            font-size: 20px;
            transition: all 0.5s ease 0s;
        }
        button:hover{
            cursor: pointer;
            background: #EEEEEE;
        }
    }


    @media(max-width: 1209px){
        .itemCard{width: 302px;}
        .itemImg img{width: 302px;}
        button{
            left: 286px;
            top: -420px;
        }
    }

</style>