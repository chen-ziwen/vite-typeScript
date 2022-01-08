<template>
    <div>
        <input type="text" v-model="change" />
        <ul>
            <li v-for="(date,index) in dateArr" :key="index">{{ `${index} :` }}{{ date }}</li>
            <button @click="niu()">点击输入</button>
            <br />
        </ul>
        {{ change }}
    </div>
</template>

<script lang="ts" setup>
import { useSlots, watch, ref, reactive } from "vue";
const slot = useSlots();

type s = string
type ab = {
    features: '性格平淡' //这个数据的类型叫文字类型，如果定义的时候features: '性格平淡'会报错
}
//type 通过&符号来实现继承
type ntype = {
    name: string,
    age: bigint,
    sex: string,
    number: string,
    height: string,
    weight: string
} & ab

type hellotype = {
    (name: string, age: number, sex: string, phone?: [string, number]): void

}
interface fun {
    hello?(hello: string, que: number): string;
    //接口定义函数
    apple?(msg: { name: string, age: number, phone: bigint }): void
}
interface stype {
    car: string,
    carCard: number,
    hello?: string

}
interface sontype {
    carson?: string,
    change: boolean
}
//接口继承通过extends 来继承
interface stype extends sontype { }

//通用接口,可以定义多种类型，俗称泛型接口
interface total<type, type2> {
    hello: type,
    apple: type2
}
let apple1: total<string, number> = {
    hello: '你好，我是string类型',
    apple: 123456
}

let apple2: total<boolean, [string, number]> = {
    hello: true,
    apple: ['我爱你', 520]
}
let objcar: stype = {
    car: '本田',
    carCard: 12345,
    change: false
}

console.log(objcar)
let change = ref<s>('');


const dateArr = reactive<ntype>({
    name: '陈子文',
    age: 22n,
    sex: '男',
    number: '18159388315',
    height: '178cm',
    weight: '80kg',
    features: '性格平淡'

})

// let haha = 'haha' as 'haha'
// haha = 10
// 这样写let 实现了const的功能

let hello: hellotype = function (name, age, sex) {
    let czwname = name + sex;
    let czwage = age - 8
    console.log(czwname, czwage)

}
function niu() {
    throw new Error('这个地方报错')
}
// let newhello  = new hello('陈子文', 22, '男')
let a = <number>10
let b = 10 as number
//a 和b 的两种定义类型等价
watch(change, (newl, oldl) => {
    dateArr.name = change.value
})
function more() {
    console.log(a, b)
}
</script>
<style>
li {
    list-style: none;
}
</style>
