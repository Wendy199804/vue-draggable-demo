<template>
    <div class="wrap">
        <div>
            <div>产品概览</div>
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
            <div>manager1</div>
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
                    <div v-for="element in myArray" :key="element.id" class="draggable-item">
                        {{ element.name }}
                        <el-button circle @click="addItem(element)">+</el-button>
                    </div>
                </transition-group>
            </Draggable>
            <div>manager2</div>
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
                    <div v-for="element in myArray" :key="element.id" class="draggable-item">
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
                            <span>编辑</span><span @click="moveUp(element, index)">上移</span><span @click="moveDown(element, index)">下移</span><span @click="unChoosed(element, index)">×</span>
                        </div>
                        <i v-show="element.choosed" @click="clickMove(element)" class="el-icon-s-unfold handle move-icon"></i>
                        {{ element.name }}
                        <el-button circle @click.stop="deleteItem(element, index)">×</el-button>
                        <component :is="allComponents[element.component]"></component>
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
                { id: 2, name: 'b', delete: false, component: 'item_2' },
                { id: 3, name: 'c', delete: false, component: 'item_3' },
                { id: 4, name: 'd', delete: false, component: 'item_4' },
                { id: 5, name: 'e', delete: false, component: 'item_5' },
                { id: 6, name: 'f', delete: false, component: 'item_6' },
            ],
            manager1: [
                {
                    id: 1,
                    name: 'manager1 a',
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
            myArray2: [{ id: 7, name: 'g', delete: false, component: 'item_1' }],
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
        console.log(this.allComponents)
    },
    methods: {
        ///添加按钮  *****  add
        addItem(ele) {
            let choosed_index = this.myArray2.findIndex((item) => item.choosed)
            let obj = Object.assign({}, ele)
            obj.id = new Date().getTime() + 'id'
            choosed_index === -1 ? this.myArray2.push(obj) : this.myArray2.splice(choosed_index + 1, 0, obj) // 添加到选中元素后面
        },
        //拖拽结束  *****  add
        end1(ev) {
            if (ev.pullMode === 'clone') {
                console.log('clone !! newDraggableIndex = ', ev.newDraggableIndex, ev.newIndex)
                // console.log(this.myArray2.length);
                let obj = Object.assign({}, this.myArray2[ev.newDraggableIndex])
                obj.id = new Date().getTime() + 'id'
                this.myArray2[ev.newDraggableIndex] = Object.assign({}, obj)
            } else {
                console.log('not clone')
            }
        },
        //删除
        deleteItem(ele, index) {
            this.myArray2[index].delete = true
            setTimeout(() => {
                this.myArray2.splice(index, 1)
            }, 200)
        },

        //选中
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
            console.log(ev);
            return ev.relatedContext.element.choosed ? true : false
        },
        //上移一个
        moveUp(ele,index){
            let obj = Object.assign({}, ele)
            obj.choosed = true
            this.myArray2.splice(index,1)
            this.myArray2.splice(index-1,0,obj)
            this.$set(this.myArray2, this.myArray2[index-1], obj)
        },
        //下移一个
        moveDown(ele,index){
            let obj = Object.assign({}, ele)
            obj.choosed = true
            this.myArray2.splice(index,1)
            this.myArray2.splice(index+1,0,obj)
            this.$set(this.myArray2, this.myArray2[index-1], obj)
        },
        //取消选中
        unChoosed(ele,index){
            let obj = Object.assign({}, ele)
            obj.choosed=false
            this.myArray2[index] = obj
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
        margin-right: 15px;
    }
    & > div:last-child {
        padding-top: 20px;
        width: 70%;
        height: 300px;
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
    height: 300px;
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
    position: relative;
    .edit {
        padding: 3px 10px;
        background-color: rgba($color: #9cccec, $alpha: 0.8);
        position: absolute;
        top: -15px;
        right: -15px;
        
        &>span{
            
            cursor: pointer;
            margin-right: 3px;
        }
    }
}
</style>
