<template>
    <el-container>
        <el-header style="background: #fff; padding: 0; height: 50px">
            <home-header></home-header>
        </el-header>
        <div class="content-box">
            <el-container>
                <el-aside style="width: 160px">
                    <home-side></home-side>
                </el-aside>
                <el-container>
                    <el-header style="height: 30px;">
                      <home-tags></home-tags>
                    </el-header>
                    <el-main>
                    <router-view></router-view>
                    </el-main>
                </el-container>
            </el-container>
        </div>
    </el-container>


</template>

<script>
    import HomeTags from './components/Tags';
    import bus from './components/bus';
    import HomeHeader from './components/Header'
    import HomeSide from './components/Side'

    export default {
        name: "Home",
        components: {
            HomeHeader,
            HomeSide,
            HomeTags
        },
        data(){
            return{
              tagsList: [],
              collapse: false
            }
        },
        created() {
            bus.$on('collapse-content', msg => {
                this.collapse = msg;
            });

            // 只有在标签页列表里的页面才使用keep-alive，即关闭标签之后就不保存到内存中了。
            bus.$on('tags', msg => {
                let arr = [];
                for (let i = 0, len = msg.length; i < len; i++) {
                    msg[i].name && arr.push(msg[i].name);
                }
                this.tagsList = arr;
            });
        }
    }
</script>

<style scoped>
    .el-main {
        padding: 0px;
    }
    .el-header{
        padding: 0;
    }

</style>
