<template>
    <div class="Calculator">
        <div class="basic-calculator">
            <div></div>
            <div class= "display">{{current || '0'}}</div>
            <div @click= "clear" class="btn remove">C</div>
            <div @click= "remove" class="btn delete">Del</div>
            <div @click= "division" class="btn operator">/</div>
            <div @click= "append('7')" class="btn">7</div>
            <div @click= "append('8')" class="btn">8</div>
            <div @click= "append('9')" class="btn">9</div>
            <div @click= "multiplication" class="btn operator">x</div>
            <div @click= "append('4')" class="btn">4</div>
            <div @click= "append('5')" class="btn">5</div>
            <div @click= "append('6')" class="btn">6</div>
            <div @click= "subtraction" class="btn operator">-</div>
            <div @click= "append('1')" class="btn">1</div>
            <div @click= "append('2')" class="btn">2</div>
            <div @click= "append('3')" class="btn">3</div>
            <div @click= "addition" class="btn operator">+</div>
            <div @click= "append('0')" class="btn">0</div>
            <div @click= "dot" class="btn">.</div>
            <div @click= "percent" class="btn">%</div>
            <div @click= "equal" class="btn operator">=</div>
        </div>
    </div>  
</template>

<script>
export default{
    data() {
        return{
            prevNum: '',
            current:'',
            operator: false,
            operatorClicked: false
        }
    },
    methods: {
        clear() {
            this.current='';
        },
        remove() {
            this.current = this.current.slice(0, -1);
        },
        percent(){
            this.current = `${parseFloat(this.current) / 100}`;
        },
        append(number){
            if (this.operatorClicked){
                this.current='';
                this.operatorClicked = false;
            }
            this.current= `${this.current}${number}`;
        },
        setprevNum(){
            this.prevNum= this.current;
            this.operatorClicked = true;
        },
        dot(){
            if (this.current.indexOf('.') === -1) {
            this.append('.');
            }
        },
        addition(){
            this.operator = (a, b) => a + b;
            this.setprevNum ();
        },
        subtraction(){
            this.operator = (a, b) => a - b;
            this.setprevNum();
        },
        multiplication(){
            this.operator = (a, b) => a * b;
            this.setprevNum();
        },
        division(){
            this.operator = (a, b) => a / b;
            this.setprevNum();
        },
        equal(){
            this.current = `${this.operator(
                parseFloat(this. prevNum),
                parseFloat(this.current)
            )}`;
            this.prevNum= '';
        }
    }


}
</script>

<style scoped>
.basic-calculator{
    display:grid;
    grid-template-columns: repeat (5, 1fr);
    grid-auto-rows: minmax(50px, auto);
    margin: 0 auto;
    width: 400px;
    height: 300px;
    font-size: 40px;
}
.display{
    grid-column: 1/5;
    background-color: black !important;
    color: #fff;
    text-align: right;
}
.remove{
    grid-column: 1/2;
}
.delete{
    grid-column: 2/4;
}
.btn{
    background-color: gray;
    border: 1px solid #999;
    cursor: pointer;
    color: white;
    text-align: center;
}
.operator{
    background-color: orange;
    color: #fff;
}
</style>