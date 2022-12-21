<template>
    <div class="animations">
        <div class="animations__search">
            <SearchInput v-model="search"/>
        </div>
        <div class="animations__list">
            <p class="animations__header">Анімації</p>
            <div class="animations__cards__container" >
                <AnimCard v-for="anim in filteredList" 
                    :key="anim.animId"
                    :id="anim.animId" 
                    :animCategory="anim.animCategory" 
                    :animName="anim.animName" 
                    draggable="true">
                    <img class="animations__list__item-image" src="../assets/dance.svg" draggable="false">
                </AnimCard>
            </div>
        </div>
        <div class="animations__quick-access">
            <p class="animations__header">Швидкий доступ</p>
            <p class="animations__quick-access__help">Для додавання анімації в швидкий доступ - зажміть ЛКМ та перетягніть анімацію в потрібний слот</p>
            <div class="animations__quick-cards__container" id="quick-anim-container">
                <QuickCard v-for="card in quickList"
                    :key="card.number"
                    :number="card.number"
                    :id="card.id"
                    :animId="card.animId"
                    :animCategory="card.animCategory" 
                    :animName="card.animName"
                    :iconId="card.iconId"
                    @dragover.prevent
                    @drop.prevent="drop"
                    @sync="syncList">
                </QuickCard>
            </div>
            <p class="animations__close-help"><span class="animations__close-help__key">ESC</span> - Закрити вікно</p>
        </div>
    </div>
</template>

<script>
import AnimCard from './AnimCard.vue'
import QuickCard from './QuickCard.vue'
import SearchInput from './SearchInput.vue'

export default {
    name: 'AnimList',
    components: {
        AnimCard,
        QuickCard,
        SearchInput
    },
    data(){
        return{
            search: '',
            animList: [
                {
                    iconId: '../assets/dance.svg',
                    animId: '1',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '2',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '3',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '4',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '5',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '6',
                    animCategory: 'Танець',
                    animName: 'Майкл Джексон'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '7',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '8',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '9',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '10',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '11',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '12',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '13',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '14',
                    animCategory: 'Танець',
                    animName: 'Робот'
                },
                {
                    iconId: '../assets/dance.svg',
                    animId: '15',
                    animCategory: 'Танець',
                    animName: 'Робот'
                }
            ],
            quickList: [
                {
                    number: 1,
                    id: 'qacess-1',
                    iconId: '',
                    animId: '',
                    animCategory: '',
                    animName: ''
                },
                {
                    number: 2,
                    id: 'qacess-2',
                    iconId: '',
                    animId: '',
                    animCategory: '',
                    animName: ''
                },
                {
                    number: 3,
                    id: 'qacess-3',
                    iconId: '',
                    animId: '',
                    animCategory: '',
                    animName: ''
                },
                {
                    number: 4,
                    id: 'qacess-4',
                    iconId: '',
                    animId: '',
                    animCategory: '',
                    animName: ''
                },
                {
                    number: 5,
                    id: 'qacess-5',
                    iconId: '',
                    animId: '',
                    animCategory: '',
                    animName: ''
                },
                {
                    number: 6,
                    id: 'qacess-6',
                    iconId: '',
                    animId: '',
                    animCategory: '',
                    animName: ''
                }
            ]
        }
    },
    methods: {
        syncList(){
            if(localStorage.getItem('quickAnims')){
                this.quickList = JSON.parse(localStorage.getItem('quickAnims'))
            }
        },
        saveQuickAnim(){
            localStorage.setItem('quickAnims', JSON.stringify(this.quickList))
        },
        drop(e){
            const card_id = e.dataTransfer.getData('card_id')
            const card = document.getElementById(card_id)
            const animName = card.querySelector(':scope > .animations__list__item-name').innerText
            const animCategory = card.querySelector(':scope > .animations__list__item-category').innerText
            const iconId = card.querySelector(':scope > .animations__list__item-backdrop > .animations__list__item-image').src
            const parent = e.target.parentNode.parentNode
            this.quickList.forEach((card, index) => {
                if(card.id === parent.id) {
                    this.quickList[index].animId = card_id;
                    this.quickList[index].animName = animName;
                    this.quickList[index].animCategory = animCategory;
                    this.quickList[index].iconId = iconId;
                }
            });
            this.saveQuickAnim()
            this.syncList()
        }
    },
    computed: {
        filteredList() {
        return this.animList.filter(anim => {
            return anim.animName.toLowerCase().includes(this.search.toLowerCase())
            })
        }
    },
    mounted(){
        this.syncList()
    }
}
</script>

<style lang="scss">
@use './src/variables.scss' as v;
.animations{
    padding: 20px;
    width: 330px;
    height: 100vh;
    border-left-width: 3px;
    border-left-style: solid;
    border-image: linear-gradient(to bottom, #E5FFFF00, #E5FFFF1A, #E5FFFF00) 1 100%;
}
.animations__header{
    margin: 10px 0 5px 0;
    text-align: center;
    color: v.$white-color;
    font-size: 14px;
}
.animations__cards__container, .animations__quick-cards__container{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-right: -12px;
}
.animations__cards__container{
    height: 442px;
    overflow-y: scroll;
}
::-webkit-scrollbar {
    width: 2px;
}
::-webkit-scrollbar-track{
    background: v.$white-color-7-op;
}
::-webkit-scrollbar-thumb{
    background: v.$aquamarin-color;
}
.animations__quick-access{
    text-align: center;
}
.animations__quick-access__help, .animations__close-help{
    font-size: 12px;
    color: v.$white-color-20-op;
}
.animations__quick-access__help{
    margin: 0 0 5px 0;
    padding: 0 10px;
}
.animations__close-help{
    margin: 7px 0 0 0;
    font-style: italic;
}
.animations__close-help__key{
    color: v.$white-color-40-op;
    font-style: normal;
}

// cards common styles

.animations__list__item{
    margin: 0;
    width: 76px;
    text-align: center;
    position: relative;
    &:not(:nth-last-child(-n+3)){
        margin-bottom: 10px;
    }
    &:nth-child(3n){
        margin-right: 12px;
    }
}
.animations__list__item-backdrop, .animations__list__item-backdrop-hover{
    width: 76px;
    height: 76px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.animations__list__item-backdrop{
    position: relative;
    background: v.$black-color;   
}
.animations__list__item-image{
    opacity: 0.25;
    filter: invert(93%) sepia(15%) saturate(284%) hue-rotate(128deg) brightness(104%) contrast(105%);
}
.animations__list__item-category{
    color: v.$white-color;
    font-size: 10px;
    margin-top: 5px;
}
.animations__list__item-name{
    color: v.$white-color-40-op;
    font-size: 8px;
}
.bgradient{
    background-image: radial-gradient(circle at 100% 100%, transparent 0px, #2bd9d900 0px, #2bd9d900 1px, transparent 1px), linear-gradient(to right, #2bd9d900, #2BD9D940), radial-gradient(circle at 0% 100%, transparent 0px, #2BD9D940 0px, #2BD9D940 1px, transparent 1px), linear-gradient(to bottom, #2BD9D940, #2bd9d900), radial-gradient(circle at 0% 0%, transparent 0px, #2bd9d900 0px, #2bd9d900 1px, transparent 1px), linear-gradient(to left, #2bd9d900, #2BD9D940), radial-gradient(circle at 100% 0%, transparent 0px, #2BD9D940 0px, #2BD9D940 1px, transparent 1px), linear-gradient(to top, #2BD9D940, #2bd9d900);
    background-size: 1px 1px, calc(100% - 2px) 1px, 1px 1px, 1px calc(100% - 2px);
    background-position: top left,top center,top right,center right, bottom right,bottom center,bottom left,center left;
    background-repeat: no-repeat;
}


@media screen and (max-height: 800px) {
    .animations__cards__container{
        height: 336px;
    }
}
</style>