<script>
import InputBox from './InputBox.vue';

    export default {
    name: "InputArea",
    data() {
        return {
            content1: null,
            content2: null,
            p1: 'none',
            p2: 'none',
            p3: 'none'
        };
    },
    components: { InputBox },
    methods: {
        updateContent1(val) {
            this.content1 = val;
        },
        updateContent2(val) {
            this.content2 = val;
        },
        solve() {
            if(this.content1 !== null && this.content2 !== null)
            {
                this.content1 = parseInt(this.content1);
                this.content2 = parseInt(this.content2);

                if(this.content2 > this.content1)
                {
                    this.$refs.start.innerText = this.content1;
                    this.$refs.end.innerText = this.content2;
                    this.$refs.result.innerText = this.content2 - this.content1;

                    [this.p1, this.p2, this.p3] = ['block', 'none', 'none'];
                }
                else 
                {
                    [this.p1, this.p2, this.p3] = ['none', 'none', 'block'];
                }
            }
            else
            {
                [this.p1, this.p2, this.p3] = ['none', 'block', 'none'];
            }
        }
    }
}
</script>

<template>
    <div class="box">
        <div>
            <InputBox msg="Enter starting point" @content-update="updateContent1" />
            <InputBox msg="Enter ending point" @content-update="updateContent2" />
        </div>
        <div class="box">
            <button class="solve-btn" @click="solve">Solve</button>
            <p class="result" :style="{ display: p1 }">
                The distance between 
                the starting point (at <span ref="start">1300</span>) 
                and ending point (at <span ref="end">5000</span>)
                <br> is <span ref="result">result</span> 
            </p>
            <p class="warning" :style="{ display: p2 }">
                Input fields aren't filled in correctly!
            </p>
            <p class="warning" :style="{ display: p3 }">
                Ending point has to be bigger than the starting point!
            </p>
        </div>
    </div>
</template>

<style scoped>
    .box{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    p {
        color: white;
        font-size: 25px;
        text-align: center;
    }

    .warning {
        color: hsl(0, 100%, 60%);
    }

    .solve-btn {
        margin-bottom: 15px;
        width: 100px;
        height: 30px;
        background-color: white;
        border: 3px solid hsl(0, 0%, 90%);
        border-radius: 5px;
        font-size: 16px;
    }

    .solve-btn:hover {
        cursor: pointer;
        box-shadow: 0px 0px 5px hsl(0, 0%, 90%);
    }

    .solve-btn:active {
        box-shadow: 0px 0px 15px hsl(0, 0%, 90%);
    }
</style>
