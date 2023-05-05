<template>
<div class="home">
    <v-container>
        <div class="box">
            <img src="https://assets-global.website-files.com/616d24eebbeca651471d975d/616d24eebbeca66b551d98ab_youtap%2520logo_103x83-01-p-500.png" alt="" class="logo-brand">
            <div class="content">
                <div class="text-center">
                    <h2>Check String</h2>
                </div>
                <v-text-field placeholder="Input text" v-model="stringData" @input="validateInput" class="text-center"></v-text-field>
                <div class="validate" v-if="isValidate">invalid input, input can only contain characters "(" or ")"</div>
                <v-btn :disabled="!stringData" @click="seeResult()" :loading="isLoading" color="#1BAED4">See Result</v-btn>
                <div class="result" v-if="isResult">
                    the result of the string above is: <span>{{ checkString(stringData) }}</span>
                </div>
            </div>
        </div>
    </v-container>
</div>
</template>

<script>
// @ is an alias to /src
export default {
    name: 'HomeView',
    data() {
        return {
            isLoading: false,
            stringData: '',
            result: '',
            isResult: false,
            isValidate: false
        }
    },
    watch: {
        stringData(val) {
            this.isResult = false;
        }
    },
    methods: {
        validateInput() {
            const pattern = /^[()]*$/
            if (!pattern.test(this.stringData)) {
                this.stringData = this.stringData.replace(/[^()]/g, '')
                this.isValidate = true
            } else {
                this.isValidate = false
            }
        },
        
        seeResult() {
            this.isLoading = true;
            setTimeout(() => {
                this.isResult = true;
                this.isLoading = false;
            }, 1000)
        },
        checkString(text) {
            let arrayString = [];
            for (let i = 0; i < text.length; i++) {
                if (text[i] === '(') {
                    arrayString.push(text[i]);
                } else if (text[i] === ')') {
                    if (arrayString.length === 0) {
                        return false;
                    }
                    arrayString.pop();
                }
            }
            return arrayString.length === 0;
        }
    },
    mounted() {}
}
</script>

<style lang="scss" scoped>
.logo-brand {
    position: absolute;
    top: 70px;
    left: 50%;
    transform: translateX(-50%);
    width: 150px;
}

.box {
    height: calc(100vh - 50px);
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;

    .content {
        border-radius: 8px;
        border: 1px solid #ccc;
        padding: 40px;
        box-shadow: 0px 0px 10px #ccc;
        width: 400px;

        .validate {
            margin-top: -12px;
            margin-bottom: 12px;
            color: #dd3131;
            font-size: 11px;
        }

        .result {
            margin-top: 20px;
            padding: 8px;
            background-color: #1bafd474;
            border-radius: 8px;

            span {
                font-weight: bold;
            }
        }
    }
}
</style>

<style>
.text-center input[type="text"] {
    text-align: center;
}
</style>
