<template>
    <el-aside width="30vw">
        <div>
            <el-main class="search-question">
                <el-input placeholder="搜索你的问题" v-model="question">
                    <i slot="suffix" class="el-input__icon el-icon-search" @click="search" style="cursor: pointer"></i>
                </el-input>
            </el-main>
            <el-main class="hots">
                <h1 style="margin-top: 0">大家都在看：</h1>
                <div class="hot" v-for="(question, index) in hots.slice(0, 10)">
                    {{ index + 1 }}.
                    <span class="title" @click="goToDetail(question.id)">
                    {{ question.title }}
                </span>
                </div>
            </el-main>
        </div>
        <el-main class="info">
            <span>AIApe</span>
            <span>京ICP备 2021007509号-1</span>
            <span>
                联系我们 @2021软件工程DQSJ
            </span>
        </el-main>
    </el-aside>
</template>

<script>
import marked from "marked";

export default {
    data() {
        return {
            question: '',
            hots: []
        }
    },
    methods: {
        search() {
            this.$search(this.question);
        },
        goToDetail(qid) {
            this.$store.commit('setQuestionID', qid);
            this.$changePage(3);
        },
        getArrRandomly(arr) {
            var len = arr.length;
            for (var i = len - 1; i >= 0; i--) {
                var randomIndex = Math.floor(Math.random() * (i + 1));
                var itemIndex = arr[randomIndex];
                arr[randomIndex] = arr[i];
                arr[i] = itemIndex;
            }
            return arr;
        }
    },
    created() {
        this.hots = this.getArrRandomly(this.$store.state.hots);
    },
    computed: {
    }
}
</script>

<style scoped>
.el-aside {
    flex-direction: column;
    height: 95vh;
    overflow: visible;
    justify-content: space-between;
}

.el-main {
    box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.1);
    margin: 10px 10px 0;
    background-color: white;
    border-radius: 2px;
}

.search-question {
    flex: 0 0 auto;
    box-shadow: 0 0 0 0;
    border-radius: 4px;
    margin-top: 0;
}

.info {
    box-shadow: 0 0 0 0;
    background-color: rgba(0, 0, 0, 0);
    flex-direction: column;
    align-items: center;
    flex-grow: 0;
}

.hots {
    flex-direction: column;
    padding: 20px;
    flex-grow: 0;
}

.el-tag {
    margin-top: 10px;
    margin-right: 10px;
    cursor: pointer;
}

i {
    color: #409eff;
}

i:hover {
    color: #6dfff3;
}

.hot {
    width: 25vw;
    white-space: nowrap;
    overflow-x: hidden;
    text-overflow: ellipsis;
    margin-bottom: 10px;
}

.title {
    cursor: pointer;
}

.title:hover {
    color: #409EFF;
}
</style>
