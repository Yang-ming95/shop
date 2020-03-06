<template>
    <el-container class="home-container">
        <!-- 头部区域 -->
        <el-header>
            <div>
                <img src="../assets/logo.png" alt="">
                <span>电商后台管理系统</span>
            </div>
            <el-button type="info" @click="logout">退出</el-button>
        </el-header>
            <!-- 页面主体区域 -->
        <el-container>
            <!-- 侧边栏 -->
          <el-aside :width="isCollapse ? '64px' : '200px'">
              <div class="toggle-button" @click="toggleCollapse">|||</div>
            <el-menu
            background-color="#333744"
            text-color="#fff"
            active-text-color="#409EFF"
            :collapse="isCollapse"
            :collapse-transition="false"
            unique-opened
            :default-active="activePath"
            router>

            <!-- 一级菜单 -->
            <el-submenu :index="menulists.id + '' " v-for="(menulists,index) in menulist" :key="index">
                <!-- 一级菜单的模板区域 -->
              <template slot="title">
                  <!-- 图标 -->
                <i :class=menulists.icons></i>
                <!-- 文本 -->
                <span>{{  menulists.authName  }}</span>
              </template>

              <!-- 二级菜单 -->
              <el-menu-item :index="item.id + '' " @click="saveNavState(item.id + '')"  v-for="(item,index) in menulists.children" :key="item.id">
                <template slot="title">
                    <!-- 图标 -->
                  <i class="el-icon-menu"></i>
                  <!-- 文本 -->
                  <span>{{  item.childrenName  }}</span>
                </template>
              </el-menu-item>
            </el-submenu>
          </el-menu>
          </el-aside>
          <!-- 右侧内容主体 -->
          <el-main>
              <router-view></router-view>
          </el-main>
        </el-container>
      </el-container>
</template>

<script>
    export default {
        data () {
            return {
                //左侧菜单数据
                menulist:[
                    {
                        "id":101,
                        "icons":"el-icon-user-solid",
                        "authName":"用户管理",
                        "path":null,
                        "children":[
                            {
                                "id":110,
                                "childrenName":"用户列表",
                            }

                        ]
                    },
                    {
                        "id":102,
                        "icons":"el-icon-s-tools",
                        "authName":"权限管理",
                        "path":null,
                        "children":[
                            {
                                "id":120,
                                "childrenName":"用户列表",
                            },
                            {
                                "id":130,
                                "childrenName":"用户列表",
                            }

                        ]
                    },
                    {
                        "id":103,
                        "icons":"el-icon-s-shop",
                        "authName":"商品管理",
                        "path":null,
                        "children":[
                            {
                                "id":140,
                                "childrenName":"用户列表",
                            },
                            {
                                "id":150,
                                "childrenName":"用户列表",
                            }

                        ]
                    },
                    {
                        "id":104,
                        "icons":"el-icon-s-order",
                        "authName":"订单管理",
                        "path":null,
                        "children":[
                            {
                                "id":160,
                                "childrenName":"用户列表",
                            },
                            {
                                "id":170,
                                "childrenName":"用户列表",
                            }

                        ]
                    },
                    {
                        "id":109,
                        "icons":"el-icon-s-marketing",
                        "authName":"数据统计",
                        "path":null,
                        "children":[
                            {
                                "id":180,
                                "childrenName":"用户列表",
                            },
                            {
                                "id":190,
                                "childrenName":"用户列表",
                            }

                        ]
                    }
                ],
                isCollapse:false,
                activePath:[]
            }
        },
        created () {
          this.activePath = window.sessionStorage.getItem('activePath')  
        },
        methods: {
            // 退出按钮
            logout() {
                this.$router.push("/login");
            },
            // 点击按钮，切换菜单的折叠与展开
            toggleCollapse(){
                this.isCollapse = !this.isCollapse
            },
            // 保存链接的激活状态
            saveNavState(activePath){
                window.sessionStorage.setItem('activePath',activePath)
                this.activePath = activePath
            }

           
        }

    };
</script>



<style lang="less" scoped>
.el-header{
    background-color: #373D41;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 20px;
    > div {
        display: flex;
        align-items: center;
        color: #fff;
        >img{
            width: 40px;
            height: 40px;
            margin-right:20px;
        }
    }
}
.el-aside{
    background-color: #333744;
    .el-menu{
        border-right: none;
    }
}
.el-main{
    background-color: #EAEDF1;
}
.home-container{
    height: 100%;
}
.toggle-button{
    background-color: #4A5064;
    font-size: 10px;
    line-height: 24px;
    text-align: center;
    letter-spacing: 0.2em;
    color: #fff;
    cursor: pointer;
}

</style>