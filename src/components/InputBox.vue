<script>
	export default {
        name: 'InputBox',
        props: ['msg', 'area'],
        data() { 
            return {
                divList: '',
                pList: '',
                inputList: '',

                content: '',

                red: 'hsl(0, 100%, 60%)',
                green: 'hsl(115, 70%, 50%)',
                black: 'hsl(0, 100%, 0%)',
                curColor: this.black
            };
        },
        emits: ['contentUpdate'],
        methods: {
            moveP(){
                if(!this.pList.includes('p-move-up'))
                {
                    this.pList = 'p-move-up';
                    this.inputList = 'input-active';
                    this.divList= 'div-shadow';
                    this.$refs.input.focus();
                }
            },
            removeClass() {
                if(this.content === '')
                {
                    this.pList = '';
                    this.inputList = '';
                    this.divList= '';
                }
            },
            updateContent(e) {
                this.content = e.target.value;
                const regex = /^((-)?[1-9]){1,7}$/;
                
                if(regex.test(this.content))
                {
                    this.curColor = this.green;
                    this.$emit('contentUpdate', this.content);
                }
                else
                {
                    this.$emit('contentUpdate', null);
                    if(this.content !== '')
                    {
                        this.curColor = this.red;
                    }
                    else
                    {
                        this.curColor = this.black;

                    }  
                }
            }
        }
    }
</script>

<template>
    <div :class="divList">
        <p :class="pList" :style="{ color: curColor }" @click="moveP">{{msg}}</p>
        <input :class="inputList" ref="input" @blur="removeClass" @input="updateContent" type="text" maxlength="7">
    </div>
</template>

<style scoped>
    div { 
        display: inline-block;
        margin: 20px;
        width: 200px;
        height: 65px;
        border: 3px solid hsl(0, 0%, 90%);
        border-radius: 5px;
        position: relative;
        background-color: white;
    }

    .div-shadow {
        box-shadow: 0px 0px 15px white;
    }
  
    p {
        width: 100%;
        height: 30%;
        margin: 0;
        padding: 0;
        position: absolute;
        bottom: 12px;
        left: 3px;
        transition: all .5s ease-out;
        z-index: 2;
        font-size: 20px;
        user-select: none;
    }
  
    p:hover {
        cursor: pointer;
    }
    
    .p-move-up {
        bottom: 40px;
        left: 5px;
        font-size: 16px;	
        }
    
    .p-move-up:hover {
        cursor: default;
    }
    
    input {
        border: none;
        outline: none;
        position: absolute;
        padding-left: 5px;
        font-size: 5px;
        width: 95%;
        height: 50%;
        bottom: 2px;
        left: 1px;
        transition: all .5s ease-out;
        }
    
    .input-active {
        font-size: 25px;
    }
</style>