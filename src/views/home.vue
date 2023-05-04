<template>
    <div id="home">
        <div class="left">
            <el-menu
                default-active="1"
                class="el-menu-vertical-demo"
                @open="handleOpen"
                @close="handleClose"
                background-color="#545c64"
                text-color="#fff"
                active-text-color="#ffd04b">
                <template v-for="(item, i) in navList">
                    <el-submenu :index="item.index" :key="index">
                        <template slot="title">
                            <i :class="item.icon"></i>
                            <span>{{ item.name }}</span>
                        </template>
                        <template v-for="(subItem, j) in item.subMenu">
                            <el-menu-item :index="subItem.index" :key="subItem.key" @click="switchTab(subItem.key, subItem.name)">{{ subItem.name }}</el-menu-item> 
                        </template>
                    </el-submenu>
                </template>
            </el-menu>
        </div>
        <div class="right">
            <el-container>
                <el-header>{{ navContent.title }}</el-header>
                <el-main>
                    <div class="filter-header">
                        <el-input placeholder="请输入客户名称" style="margin-right: 20px;"></el-input>
                        <el-button style="margin-right: 300px;">搜索</el-button>
                        <el-button type="primary">刷新</el-button>
                        <el-button type="primary">添加</el-button>
                    </div>
                    <div class="data-table">
                        <el-table
                            :data="tableData"
                            style="width: 100%">
                            <el-table-column
                            label="日期"
                            width="180">
                            <template slot-scope="scope">
                                <i class="el-icon-time"></i>
                                <span style="margin-left: 10px">{{ scope.row.date }}</span>
                            </template>
                            </el-table-column>
                            <el-table-column
                            label="姓名"
                            width="180">
                            <template slot-scope="scope">
                                <el-popover trigger="hover" placement="top">
                                <p>姓名: {{ scope.row.name }}</p>
                                <p>住址: {{ scope.row.address }}</p>
                                <div slot="reference" class="name-wrapper">
                                    <el-tag size="medium">{{ scope.row.name }}</el-tag>
                                </div>
                                </el-popover>
                            </template>
                            </el-table-column>
                            <el-table-column label="操作">
                            <template slot-scope="scope">
                                <el-button
                                size="mini"
                                @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
                                <el-button
                                size="mini"
                                type="danger"
                                @click="handleDelete(scope.$index, scope.row)">删除</el-button>
                            </template>
                            </el-table-column>
                        </el-table>
                        <el-pagination
                            background
                            layout="prev, pager, next"
                            :total="1000"
                        ></el-pagination>
                    </div>
                </el-main>
            </el-container>
        </div>
    </div>
</template>
  
<script>
  export default {
    name: 'home',
    data: () => ({
        navList: [
            {
                name: '销售管理',
                index: '1',
                icon: 'el-icon-menu',
                subMenu: [
                    {
                        name: '客户信息管理',
                        index: '1-1',
                        key: 'customInfo',
                        icon: ''
                    },
                    {
                        name: '代理商管理',
                        index: '1-2',
                        key: 'agent'
                    },
                    {
                        name: '销售订单',
                        index: '1-3',
                        key: 'sale'
                    },
                ]
            },
            {
                name: '计划管理',
                index: '2',
                icon: 'el-icon-s-flag',
                subMenu: [
                    {
                        name: '指定计划',
                        index: '2-1',
                        key: 'makePlan'
                    }
                ]
            },
            {
                name: '财务管理',
                index: '3',
                icon: 'el-icon-s-custom',
                subMenu: [
                    {
                        name: '客户结算',
                        index: '3-1',
                        key: 'customPay'
                    },
                    {
                        name: '代理商结算',
                        index: '3-2',
                        key: 'agentPay'
                    },
                    {
                        name: '报销结算',
                        index: '3-3',
                        key: 'submitPay'
                    }
                ]
            },
            {
                name: '库存管理',
                index: '4',
                icon: 'el-icon-house',
                subMenu: [
                    {
                        name: '原材料',
                        index: '4-1',
                        key: 'material '
                    },
                    {
                        name: '库存管理',
                        index: '4-2',
                        key: 'inventory'
                    }
                ]
            },
            {
                name: '系统管理',
                index: '5',
                icon: 'el-icon-setting',
                subMenu: [
                    {
                        name: '用户管理',
                        index: '5-1',
                        key: 'user '
                    },
                    {
                        name: '系统管理',
                        index: '5-2',
                        key: 'system'
                    }
                ]
            },
            {
                name: '退出系统',
                index: '6',
                icon: 'el-icon-switch-button'
            }
        ],
        tableData: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },{
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },{
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }],
        navContent: {
            title: '',
            tableHeaders: [],
            tableBtn: [],
            tableData: []
        }
    }),
    methods: {
      handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      switchTab(tab, name) {
        console.log(tab)
        this.navContent.title = name
      },
      handleEdit(index, row) {
        console.log(index, row);
      },
      handleDelete(index, row) {
        console.log(index, row);
      }
    }
  }
</script>
  
<style scoped lang="scss">
    #home{
        width: 100vw;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        .left{
            width: 15%;
            height: 100%;
            background-color: #545c64;
        }
        .right{
            width: 85%;
            height: 100%;
            background-color: #fff;
            ::v-deep .el-container{
                width: 100%;
                height: 100%;
                .el-header{
                    background-color: #B3C0D1;
                    color: #333;
                    height: 10%;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    font-size: 22px;
                    font-weight: bold;
                }
                .el-main {
                    background-color: #E9EEF3;
                    color: #333;
                    height: 90%;
                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    justify-content: center;
                }
            }
            .filter-header{
                width: 90%;
                height: 60px;
                display: flex;
                align-items: center;
                justify-content: flex-start;
                padding-left: 10px;
                padding-right: 10px;
                box-sizing: border-box;
                background-color: #B3C0D1;
            }
            .data-table{
                width: 90%;
                height: 500px;
                background-color: rgba(255, 255, 255, 0.7);
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;
            }         
        }
    }
</style>
  