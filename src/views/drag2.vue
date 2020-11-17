<template>
    <div class="wrap">
        <div>
            <div>产品概览 <span @click="addAll(myArray)">全部添加</span></div>
            <Draggable
                class="cards-group"
                v-model="myArray"
                :animation="200"
                :options="{
                    sort: false,
                    group: { name: 'group', pull: 'clone', put: false },
                }"
                ghostClass="ghost1"
                @end="end1"
            >
                <transition-group>
                    <div v-for="element in myArray" :key="element.id" class="draggable-item">
                        {{ element.name }}
                        <el-button circle @click="addItem(element)">+</el-button>
                    </div>
                </transition-group>
            </Draggable>
            <div>基金经理1 <span @click="addAll(manager1)">全部添加</span></div>
            <Draggable
                class="cards-group"
                v-model="manager1"
                :animation="200"
                :options="{
                    sort: false,
                    group: { name: 'group', pull: 'clone', put: false },
                }"
                ghostClass="ghost1"
                @end="end1"
            >
                <transition-group>
                    <div v-for="element in manager1" :key="element.id" class="draggable-item">
                        {{ element.name }}
                        <el-button circle @click="addItem(element)">+</el-button>
                    </div>
                </transition-group>
            </Draggable>
            <div>基金经理2 <span @click="addAll(manager2)">全部添加</span></div>
            <Draggable
                class="cards-group"
                v-model="manager2"
                :animation="200"
                :options="{
                    sort: false,
                    group: { name: 'group', pull: 'clone', put: false },
                }"
                ghostClass="ghost1"
                @end="end1"
            >
                <transition-group>
                    <div v-for="element in manager2" :key="element.id" class="draggable-item">
                        {{ element.name }}
                        <el-button circle @click="addItem(element)">+</el-button>
                    </div>
                </transition-group>
            </Draggable>
        </div>

        <!-- 右边
        handle=".handle"
        draggable=".item"
        filter=".forbid"
        :move="onMove"
        -->
        <div>
            <Draggable
                class="empty-group"
                v-model="myArray2"
                :animation="200"
                :options="{
                    group: { name: 'group', fallbackTolerance: 0 },
                    scroll: true,
                    scrollSpeed: 2,
                }"
                ghostClass="ghost2"
                chosen-class="chosen"
                handle=".handle"
            >
                <transition-group>
                    <div v-for="(element, index) in myArray2" :key="element.id" :class="[element.delete ? 'to-right' : '', element.choosed ? 'border' : '', 'list-group-item', 'my-list-group-item', 'cursor-auto']" @click="chooseItem(element, index)">
                        <div v-show="element.choosed" class="edit">
                            <span @click.stop="unChoosed(element, index)">取消选中</span>
                            <span @click.stop="moveUp(element, index)">上移</span>
                            <span @click.stop="moveDown(element, index)">下移</span>
                            <span @click.stop="copyItem(element, index)">复制</span>
                            <span @click.stop="deleteItem(element, index)">删除</span>
                            <span @click.stop="addArticle(element, index)">添加文案</span>
                        </div>
                        <i v-show="element.choosed" class="el-icon-s-unfold handle move-icon"></i>
                        <i v-show="element.choosed" @click.stop="clickMove(element)" class="el-icon-s-unfold move-icon"></i>
                        {{ element.name }}
                        <!-- <el-button circle @click.stop="deleteItem(element, index)">×</el-button> -->
                        <component :is="allComponents[element.component]"></component>
                        <div v-show="element.articlelist && element.articlelist.length > 0" @click.stop class="textarea-wrap">
                            <!-- <textarea>我是一个文本框。</textarea> -->
                            <div v-for="(item, index2) in element.articlelist" :key="index2">
                                <!-- 文案个数 -->
                                <div v-show="element.choosed">文字颜色<el-color-picker v-model="item.color" size="mini"></el-color-picker></div>
                                <div :contenteditable="element.choosed" @focus="articleFocus(item, index, index2, $event)" @blur="articleBlur(item, index, index2, $event)" :style="{ color: item.color }" class="custom-article">
                                    这是一个文案，点击可以编辑
                                </div>
                            </div>
                        </div>
                    </div>
                </transition-group>
            </Draggable>
        </div>
    </div>
</template>

<script>
import Draggable from 'vuedraggable'
import allComponents from '@/components/dragItems/exportComponent'
// import item_6 from '@/components/dragItems/item_6'

export default {
    data() {
        return {
            allComponents: allComponents,
            myArray: [
                { id: 1, name: 'a', delete: false, component: 'item_1' },
                { id: 2, name: '??', delete: false, component: 'item_2' },
                { id: 3, name: 'c', delete: false, component: 'item_3' },
                { id: 4, name: 'd', delete: false, component: 'item_4' },
                { id: 5, name: 'e', delete: false, component: 'item_5' },
                { id: 6, name: 'f', delete: false, component: 'item_6' },
            ],
            manager1: [
                {
                    id: 1,
                    name: 'manager1 a1111111111111',
                    delete: false,
                    component: 'item_1',
                    manager_id: 1,
                },
                {
                    id: 2,
                    name: 'manager1 b',
                    delete: false,
                    component: 'item_2',
                    manager_id: 1,
                },
                {
                    id: 3,
                    name: 'manager1 c',
                    delete: false,
                    component: 'item_3',
                    manager_id: 1,
                },
                {
                    id: 4,
                    name: 'manager1 d',
                    delete: false,
                    component: 'item_4',
                    manager_id: 1,
                },
                {
                    id: 5,
                    name: 'manager1 e',
                    delete: false,
                    component: 'item_5',
                    manager_id: 1,
                },
                {
                    id: 6,
                    name: 'manager1 f',
                    delete: false,
                    component: 'item_6',
                    manager_id: 1,
                },
            ],
            manager2: [
                {
                    id: 1,
                    name: 'manager2 a',
                    delete: false,
                    component: 'item_1',
                    manager_id: 2,
                },
                {
                    id: 2,
                    name: 'manager2 b',
                    delete: false,
                    component: 'item_2',
                    manager_id: 2,
                },
                {
                    id: 3,
                    name: 'manager2 c',
                    delete: false,
                    component: 'item_3',
                    manager_id: 2,
                },
                {
                    id: 4,
                    name: 'manager2 d',
                    delete: false,
                    component: 'item_4',
                    manager_id: 2,
                },
                {
                    id: 5,
                    name: 'manager2 e',
                    delete: false,
                    component: 'item_5',
                    manager_id: 2,
                },
                {
                    id: 6,
                    name: 'manager2 f',
                    delete: false,
                    component: 'item_6',
                    manager_id: 2,
                },
            ],
            myArray2: [
                {
                    id: 7,
                    name: 'g',
                    delete: false,
                    component: 'item_1',
                    articleNum: 0,
                },
            ],
            options: {
                animation: 2,
            },
        }
    },
    components: {
        Draggable,
        // item1,item2,item3,item4,item5,item6
    },
    mounted() {
        console.log(this.myArray2)
    },
    methods: {
        ///添加按钮  *****  add
        addItem(ele) {
            let choosed_index = this.myArray2.findIndex((item) => item.choosed)
            let obj = Object.assign({}, ele)
            obj.id = new Date().getTime() + 'id'
            obj.articleNum = 0
            obj.articlelist = []
            choosed_index === -1 ? this.myArray2.push(obj) : this.myArray2.splice(choosed_index + 1, 0, obj) // 添加到选中元素后面
        },
        //拖拽结束  *****  add
        end1(ev) {
            if (ev.pullMode === 'clone') {
                console.log('clone !! newDraggableIndex = ', ev.newDraggableIndex, ev.newIndex)
                // console.log(this.myArray2.length);
                let obj = Object.assign({}, this.myArray2[ev.newDraggableIndex])
                obj.id = new Date().getTime() + 'id'
                obj.articleNum = 0
                obj.articlelist = []
                this.myArray2[ev.newDraggableIndex] = Object.assign({}, obj)
            } else {
                console.log('not clone')
            }
        },
        //全部添加  *****  add
        addAll(arr) {
            let choosed_index = this.myArray2.findIndex((item) => item.choosed)
            arr = arr.map((item, index) => {
                item.id = new Date().getTime() + 'id' + index
                // item.choosed = false
                return item
            })
            let newarr = JSON.parse(JSON.stringify(arr))
            this.myArray2 = choosed_index === -1 ? [...this.myArray2, ...arr] : [...this.myArray2.slice(0, choosed_index + 1), ...arr, ...this.myArray2.slice(choosed_index + 1)]
        },
        //删除
        deleteItem(ele, index) {
            let obj = Object.assign({}, ele)
            obj.delete = true
            obj.choosed = false
            this.$set(this.myArray2, index, obj)
            setTimeout(() => {
                this.myArray2.splice(index, 1)
            }, 200)
        },

        //选中（双击）
        chooseItem(ele, index) {
            if (!ele.choosed) {
                this.myArray2 = this.myArray2.map((item) => {
                    item.choosed = false
                    return item
                })
                let obj = Object.assign({}, ele)
                obj.choosed = true
                // this.$set(this.myArray2[index],'choosed',true)
                this.myArray2[index] = obj
            } else {
                let obj = Object.assign({}, ele)
                obj.choosed = false
                this.$set(this.myArray2, this.myArray2[index], obj)
                this.myArray2[index] = obj
            }
        },
        //选中状态才可以拖动
        onMove(ev) {
            console.log(ev)
            return ev.relatedContext.element.choosed ? true : false
        },
        //上移一个
        moveUp(ele, index) {
            let obj = Object.assign({}, ele)
            obj.choosed = true
            this.myArray2.splice(index, 1)
            this.myArray2.splice(index - 1, 0, obj)
            this.$set(this.myArray2, this.myArray2[index - 1], obj)
        },
        //下移一个
        moveDown(ele, index) {
            let obj = Object.assign({}, ele)
            obj.choosed = true
            this.myArray2.splice(index, 1)
            this.myArray2.splice(index + 1, 0, obj)
            this.$set(this.myArray2, this.myArray2[index + 1], obj)
            console.log(this.myArray2)
        },
        //复制一个到后面
        copyItem(ele, index) {
            let obj = Object.assign({}, ele)
            obj.id = new Date().getTime() + 'id'
            obj.articleNum = 0
            obj.articlelist = []
            obj.choosed = false
            this.myArray2.splice(index + 1, 0, obj)
            this.$set(this.myArray2, this.myArray2[index + 1], obj)
        },
        //添加文案
        addArticle(ele, index) {
            console.log(this.myArray2)
            let obj = Object.assign({}, ele)
            obj.articleNum = ele.articleNum + 1
            obj.articlelist.push({ color: '#333', focus: false })
            obj.choosed = true
            this.$set(this.myArray2, index, obj)
            console.log(this.myArray2)
            // this.$set(this.myArray2[index], 'choosed',true)

            // console.log(obj,this.myArray2)
        },
        //取消选中
        unChoosed(ele, index) {
            let obj = Object.assign({}, ele)
            obj.choosed = false
            this.$set(this.myArray2, index, obj)
        },
        //文案编辑聚焦 (原定：聚焦的时候才能改变颜色)
        articleFocus(ele, index, index2, ev) {
            let obj = Object.assign({},this.myArray2[index])
            obj.articlelist[index2].focus = true
            this.$set(this.myArray2, index, obj)
            console.log('聚焦', ev)
        },
        //文案编辑失焦
        articleBlur(ele, index, index2, ev) {
            let obj = Object.assign({},this.myArray2[index])
            obj.articlelist[index2].focus = false
            this.$set(this.myArray2, index, obj)
            console.log('失焦', ev)
        },
        clickMove(ele) {
            console.log('click move', ele)
        },
    },
}
</script>

<style lang="scss" scoped>
.wrap {
    display: flex;
    justify-content: space-between;
    width: 95%;

    & > div:first-child {
        width: 30%;
        height: 700px;
        margin-right: 15px;
    }
    & > div:last-child {
        width: 70%;
        height: 700px;
        padding-top: 20px;
        overflow-y: auto;
    }
}
.draggable-item {
    height: 50px;
    // width: 500px;
    border: 1px solid #000000;
    margin-bottom: 5px;
    cursor: pointer;
}
.cards-group {
}
.empty-group {
    width: 90%;
    height: 100%;
    border: 1px solid blueviolet;
    // overflow-y: auto;

    & > span {
        display: block;
        height: 300px;
        width: 100%;
        border: 1px solid red;
    }
}
.to-right {
    transform: translateX(100%);
    transition: all 0.3s;
}
.cursor-auto {
    cursor: auto;
}
.handle {
    cursor: move;
}
//选中边框
.border {
    border: 2px solid rgb(133, 174, 228);
}
//可拖动元素
// .list-group-item{
//     position: relative;
//     z-index: 100;
// }
// .move-icon{
//     position: relative;
//     z-index: 101
// }
//占坑元素
.ghost2 {
    background-color: #000;
    transform: translateX(20px);
    height: 0px;
    overflow: hidden;
    margin: 0;
    padding-top: 1px;
}
.ghost1 {
    background: #ffffff;
}
//拖动时 //选中时
.chosen {
    transform: translateX(20px);
    background-color: #999;
    padding: 0;
    // height: auto;
    // opacity: 0.5;
    // overflow: hidden;
}
//选中元素
.my-list-group-item {
    height: auto;
    position: relative;
    .edit {
        padding: 3px 10px;
        background-color: rgba($color: #9cccec, $alpha: 0.8);
        position: absolute;
        top: -15px;
        right: -15px;

        & > span {
            cursor: pointer;
            margin-right: 3px;
        }
    }
}
.textarea-wrap {
    height: auto;
    width: auto;
    border: 1px dashed fuchsia;
    padding: 5px;
    .custom-article {
        outline: none;
        border: 1px solid #dddddd;
        padding: 5px 10px;
        margin-bottom: 5px;
    }
}
</style>
